## Moodle installation.

Here is a step-by-step guide to installing Moodle on Alpine Linux running in VirtualBox. The setup includes using Nginx, PHP-FPM, and MariaDB.

---

### **Step 1: Prepare Alpine Linux**

1. **Install Alpine Linux in VirtualBox:**
   - Set up a new virtual machine with at least **2GB RAM**, **5GB disk space**, and **bridged adapter or NAT for networking**.
   - Install the CLI-only version of Alpine Linux.

2. **Update Alpine:**
   ```bash
   apk update && apk upgrade
   ```

3. **Install Essential Tools:**
   ```bash
   apk add nano wget curl bash
   ```

---

### **Step 2: Install and Configure MariaDB**

1. **Install MariaDB:**
   ```bash
   apk add mariadb mariadb-client
   ```

2. **Initialize the Database:**
   ```bash
   mysql_install_db --user=mysql --datadir=/var/lib/mysql
   ```

3. **Start and Enable MariaDB:**
   ```bash
   rc-service mariadb start
   rc-update add mariadb
   ```

4. **Secure MariaDB:**
   Run the secure installation:
   ```bash
   mysql_secure_installation
   ```
   - Set a root password.
   - Remove anonymous users: `Y`
   - Disallow root login remotely: `Y`
   - Remove test database: `Y`
   - Reload privilege tables: `Y`

5. **Create Moodle Database and User:**
   Log in to MySQL:
   ```bash
   mysql -u root -p
   ```
   Execute the following SQL commands:
   ```sql
   CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```

---

### **Step 3: Install and Configure PHP**

1. **Install PHP and Extensions:**
   ```bash
   apk add php82 php82-fpm php82-mysqli php82-ctype php82-session php82-dom php82-iconv php82-curl php82-mbstring php82-opcache php82-fileinfo php82-xml php82-tokenizer php82-simplexml php82-intl php82-zip
   ```

2. **Edit PHP-FPM Configuration:**
   Open the PHP-FPM configuration file:
   ```bash
   nano /etc/php82/php-fpm.d/www.conf
   ```
   Set `user` and `group` to `nginx`:
   ```ini
   user = nginx
   group = nginx
   ```

3. **Start and Enable PHP-FPM:**
   ```bash
   rc-service php-fpm82 start
   rc-update add php-fpm82
   ```

---

### **Step 4: Install and Configure Nginx**

1. **Install Nginx:**
   ```bash
   apk add nginx
   ```

2. **Create Moodle Nginx Configuration:**
   Open a new configuration file:
   ```bash
   nano /etc/nginx/http.d/moodle.conf
   ```
   Add the following:
   ```nginx
   server {
       listen 80;
       server_name localhost 192.248.4.212;

       root /var/www/moodle;
       index index.php;

       location / {
           try_files $uri $uri/ /index.php;
       }

       location ~ \.php$ {
           include fastcgi_params;
           fastcgi_pass 127.0.0.1:9000;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
       }
   }
   ```

3. **Test and Restart Nginx:**
   ```bash
   nginx -t
   rc-service nginx restart
   rc-update add nginx
   ```

---

### **Step 5: Install Moodle**

1. **Download Moodle:**
   ```bash
   cd /var/www
   wget https://download.moodle.org/download.php/direct/stable411/moodle-latest-411.tgz
   tar -xvf moodle-latest-411.tgz
   rm moodle-latest-411.tgz
   ```

2. **Set Permissions:**
   ```bash
   mkdir /var/www/moodledata
   chown -R nginx:nginx /var/www/moodle /var/www/moodledata
   chmod -R 0777 /var/www/moodledata
   ```

---

### **Step 6: Configure Moodle**

1. **Visit Moodle in Browser:**
   - If using NAT with port forwarding, open:
     ```
     http://localhost:8080
     ```
   - If using a bridged adapter, use:
     ```
     http://192.248.4.212
     ```

2. **Follow the Installer:**
   - Enter the database details:
     - Database type: MariaDB
     - Host: `localhost`
     - Database name: `moodle`
     - Username: `moodleuser`
     - Password: `password`
   - Complete the installation.

---

### **Step 7: Access Moodle on localhost**

If you want to run Moodle on `localhost` instead of the IP:

1. Update `wwwroot` in the configuration file:
   ```bash
   nano /var/www/moodle/config.php
   ```
   Change:
   ```php
   $CFG->wwwroot = 'http://localhost';
   ```

2. Restart Nginx:
   ```bash
   rc-service nginx restart
   ```

3. Access Moodle via:
   ```
   http://localhost
   ```

---

### **Step 8: Troubleshooting**

1. **CSS Not Loading:**
   - Purge caches:
     ```bash
     php82 admin/cli/purge_caches.php
     ```

2. **Database Errors:**
   Ensure MariaDB is running:
   ```bash
   rc-service mariadb restart
   ```

3. **Permissions Issues:**
   Verify permissions:
   ```bash
   chown -R nginx:nginx /var/www/moodle /var/www/moodledata
   chmod -R 0777 /var/www/moodledata
   ```

Let me know if you encounter any specific issues!
