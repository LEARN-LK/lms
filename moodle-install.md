

` Note: If you are planning to self-host Moodle on your own server, here’s a step-by-step guide to installing Moodle 4.4 on Ubuntu 24 Server.`

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




### 9. **Moodle Web UI Configuration**

i. Open your browser and enter your domain name or server IP address.
ii. You will be directed to a language selection page. Choose your preferred language and click the **Next** button.

<img width="500" alt="image" src="https://github.com/LEARN-LK/lms/blob/master/img/webui01.png">
   
iii. The installation page will appear. In this section, choose the location for your **Data Directory** path and click **Next**.

<img width="500" alt="image" src="https://github.com/LEARN-LK/lms/blob/master/img/webui02.png">
   
iv. You will then be redirected to the database configuration page.
      
v. In the **Database Type** section, select **Improved MySQL (native/mysqli)** and click **Next**.

<img width="500" alt="image" src="https://github.com/LEARN-LK/lms/blob/master/img/webui03.png">
   
vi. On the next screen, enter your **Database Username**, **Database Password**, and other required database settings. After filling in the details, click **Next**.

<img width="500" alt="image" src="https://github.com/LEARN-LK/lms/blob/master/img/webui04.png">
   
vii. Click the **Install** or **Confirm** button to begin the installation process.

<img width="500" alt="image" src="https://github.com/LEARN-LK/lms/blob/master/img/webui05.png">
      
Here’s the corrected version with the additional steps for handling the MariaDB error:
viii. The system will perform a server environment check.

- If there are any issues or errors with your server environment, resolve all of them before proceeding.
- Once all environmental problems are resolved, continue with the installation.  
---
#### **Common Errors and Their Solutions:**

1. **If you encounter the following error:**

   ```
   database mysql (10.11.8-MariaDB-0ubuntu0.24.04.1) must be installed and enabled
   Wrong $CFG->dbtype. You need to change it in your config.php file from 'mysqli' to 'mariadb'.
   ```

   Follow these steps to resolve the error:

   **i. Open the Moodle configuration file:**

   The `config.php` file is located in the root of your Moodle installation. Open it using a text editor like `nano`:

   ```bash
   sudo nano /path/to/moodle/config.php
   ```

   **ii. Locate the `$CFG->dbtype` setting:**

   Look for the line that defines the database type:

   ```php
   $CFG->dbtype = 'mysqli';
   ```

   **iii. Change the database type to `'mariadb'`:**

   Modify the line to:

   ```php
   $CFG->dbtype = 'mariadb';
   ```

   **iv. Save the file and exit:**

   Press `CTRL+O` to save the file, then `CTRL+X` to exit the text editor.

   **v. Test the changes:**

   Refresh your browser and check if the Moodle installation process continues without the database error.

---

2. **If you encounter the following error:**

   ```
   PHP setting max_input_vars must be at least 5000.
   ```

   This error means that the `max_input_vars` PHP configuration value is too low. To resolve it, you need to increase `max_input_vars` to at least 5000.

   ### Steps to increase `max_input_vars` in PHP:

   **i. Locate your PHP configuration file:**

   The `php.ini` file location depends on the PHP version and web server you're using. On Ubuntu, common paths are:

   - For Apache: `/etc/php/{php_version}/apache2/php.ini`
   
   Replace `{php_version}` with your installed PHP version (e.g., `8.3`).

   **ii. Edit the `php.ini` file:**

   Open the `php.ini` file in a text editor. For example, using `nano`:

   For Apache:
   ```bash
   sudo nano /etc/php/{php_version}/apache2/php.ini
   ```

   **iii. Increase the `max_input_vars` value:**

   Find or add the line for `max_input_vars` in the file and set it to at least 5000:

   ```ini
   max_input_vars = 5000
   ```

   **iv. Save and exit the file:**

   Press `CTRL+O` to save the file, then `CTRL+X` to exit.

   **v. Restart your web server:**

   After modifying the `php.ini` file, restart the web server to apply the changes:

   For Apache:
   ```bash
   sudo systemctl restart apache2
   ```
