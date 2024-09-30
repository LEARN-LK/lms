Here’s a step-by-step guide to installing **Moodle** on **Ubuntu 24 Server**:

### 1. **Update Your System**

Before installing anything, ensure your system is up to date:

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. **Install Required Packages**

Moodle requires a web server, PHP, and a database. Install Apache, PHP, and MariaDB (or MySQL) with the necessary extensions:

```bash
sudo apt install apache2 mariadb-server php libapache2-mod-php php-mysql php-xml php-zip php-gd php-intl php-curl php-xmlrpc php-soap php-mbstring php-json -y
```

### 3. **Set Up MariaDB (or MySQL) Database**

1. Secure MariaDB installation:

```bash
sudo mysql_secure_installation
```

2. Log into the MariaDB shell as root:

```bash
sudo mysql -u root -p
```

3. Create the database for Moodle and a database user:

```sql
CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Replace `your_password` with a secure password.

### 4. **Install Moodle**

1. Navigate to the web directory and download Moodle:

```bash
cd /var/www/html
sudo wget https://download.moodle.org/stable400/moodle-latest-400.tgz
```

2. Extract the downloaded Moodle file:

```bash
sudo tar -zxvf moodle-latest-400.tgz
```

3. Move the extracted folder and set permissions:

```bash
sudo mv moodle /var/www/html/
sudo mkdir /var/www/moodledata
sudo chown -R www-data:www-data /var/www/moodledata /var/www/html/moodle
sudo chmod -R 755 /var/www/moodledata /var/www/html/moodle
```

### 5. **Configure Apache for Moodle**

1. Create a new Apache configuration file for Moodle:

```bash
sudo nano /etc/apache2/sites-available/moodle.conf
```

2. Add the following configuration:

```plaintext
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/moodle
    ServerName your-domain.com
    ServerAlias www.your-domain.com

    <Directory /var/www/html/moodle/>
        Options FollowSymlinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/moodle_error.log
    CustomLog ${APACHE_LOG_DIR}/moodle_access.log combined
</VirtualHost>
```

Replace `your-domain.com` with your actual domain name (or use the server's IP address if you don't have a domain).

3. Enable the Moodle site and the `rewrite` module:

```bash
sudo a2ensite moodle.conf
sudo a2enmod rewrite
```

4. Restart Apache:

```bash
sudo systemctl restart apache2
```

### 6. **Configure PHP for Moodle**

Moodle recommends increasing some PHP limits. Edit the PHP configuration file:

```bash
sudo nano /etc/php/8.1/apache2/php.ini
```

Find and modify the following values:

```ini
memory_limit = 256M
max_execution_time = 300
upload_max_filesize = 100M
post_max_size = 100M
```

Then restart Apache to apply the changes:

```bash
sudo systemctl restart apache2
```

### 7. **Complete Moodle Installation Through the Web Interface**

1. Open your browser and go to `http://your-domain.com` (or the server’s IP address if you don't have a domain).
2. Follow the on-screen instructions to configure the database:
   - Database type: **MariaDB**
   - Database name: **moodle**
   - Database user: **moodleuser**
   - Database password: **your_password**
3. Finish the installation and set up your Moodle admin account.

### 8. **Final Steps**

After the installation is completed through the web interface, Moodle should be ready for use.

Let me know if you need help with any specific part of the process!

### 9 . ** Moodle Step WEB UI
type your domain or IP Addresses in to a browser 
then it will show chooce a languagu interface then click next button
then it will rederect installation page , in  this section you shoud chooce the path where data directory located path
then click Next
then it will redirect the database interface
then slelct database type "improved MySQL (native/mysqli)" then click next
then it will redirect database setting interface
add database user , database password here , then click next button
then click installation confirm button
then it will redirect service check interface , 
 You must solve all the environmental problems (errors) found above before proceeding to install this Moodle version!



 Here’s a corrected version of your Moodle web UI configuration step:

---

### 9. **Moodle Web UI Configuration**

1. Open your browser and enter your domain name or server IP address.
2. You will be directed to a language selection page. Choose your preferred language and click the **Next** button.
3. The installation page will appear. In this section, choose the location for your **Data Directory** path and click **Next**.
4. You will then be redirected to the database configuration page.
5. In the **Database Type** section, select **Improved MySQL (native/mysqli)** and click **Next**.
6. On the next screen, enter your **Database Username**, **Database Password**, and other required database settings. After filling in the details, click **Next**.
7. Click the **Install** or **Confirm** button to begin the installation process.
8. The system will perform a server environment check. 
   - If there are any issues or errors with your server environment, resolve all of them before proceeding.
   - Once all environmental problems are resolved, continue with the installation.

---

This version improves readability and corrects typos while keeping the original meaning intact.
 

