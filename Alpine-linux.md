Here's the updated step-by-step guide to install Moodle on Alpine Linux with your provided configuration:

---

### **Step-by-Step Guide to Install Moodle on Alpine Linux**

---

### **Step 1: Update and Prepare Alpine Linux**

1. **Update the package list:**
   ```bash
   apk update
   ```
2. **Upgrade installed packages:**
   ```bash
   apk upgrade
   ```

---

### **Step 2: Install Required Packages**

1. Install necessary packages:
   ```bash
   apk add nginx php82 php82-fpm php82-session php82-opcache php82-gd php82-mysqli php82-pdo_mysql php82-xmlreader php82-ctype php82-zip php82-soap php82-intl php82-xmlrpc php82-mbstring php82-json php82-curl php82-tokenizer mariadb mariadb-client wget
   ```
2. Enable and start services:
   ```bash
   rc-service nginx start
   rc-service php-fpm82 start
   rc-service mariadb start
   rc-update add nginx
   rc-update add php-fpm82
   rc-update add mariadb
   ```

---

### **Step 3: Configure MariaDB**

1. **Secure the MariaDB installation:**
   ```bash
   mysql_secure_installation
   ```
2. **Log in to MariaDB:**
   ```bash
   mysql -u root -p
   ```
3. **Create a database and user for Moodle:**
   ```sql
   CREATE DATABASE moodle CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY 'mdl@123';
   GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```

---

### **Step 4: Download and Set Up Moodle**

1. **Download Moodle:**
   ```bash
   cd /var/www
   wget https://download.moodle.org/stable402/moodle-latest-402.tgz
   ```
2. **Extract Moodle:**
   ```bash
   tar -xvzf moodle-latest-402.tgz
   rm moodle-latest-402.tgz
   ```
3. **Create the Moodle data directory:**
   ```bash
   mkdir /var/www/moodledata
   chown -R nginx:nginx /var/www/moodle /var/www/moodledata
   chmod -R 777 /var/www/moodledata
   ```

---

### **Step 5: Configure Nginx**

1. **Edit the Nginx configuration:**
   ```bash
   nano /etc/nginx/http.d/moodle.conf
   ```
2. **Add the following content:**
   ```nginx
   server {
       listen 80;
       server_name 192.XXX.X.XX
       root /var/www/moodle;
       index index.php index.html index.htm;

       location / {
           try_files $uri $uri/ /index.php?$query_string;
       }

       location ~ [^/]\.php(/|$) {
           fastcgi_split_path_info ^(.+\.php)(/.+)$;
           fastcgi_index           index.php;
           include fastcgi_params;
           fastcgi_pass 127.0.0.1:9000;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           fastcgi_param PATH_INFO $fastcgi_path_info;
       }

       location ~* /\. {
           deny all;
       }
   }
   ```
3. **Test and restart Nginx:**
   ```bash
   nginx -t
   rc-service nginx restart
   ```

---

### **Step 6: Configure PHP-FPM**

1. **Edit the PHP-FPM configuration:**
   ```bash
   nano /etc/php82/php-fpm.d/www.conf
   ```
2. **Set the `user` and `group` to `nginx`:**
   ```ini
   user = nginx
   group = nginx
   ```
3. **Restart PHP-FPM:**
   ```bash
   rc-service php-fpm82 restart
   ```

---

### **Step 7: Configure Moodle**

1. **Edit the Moodle configuration file:**
   ```bash
   nano /var/www/moodle/config.php
   ```
2. **Add the following content:**
   ```php
   <?php
   $CFG->dbtype    = 'mariadb';
   $CFG->dblibrary = 'native';
   $CFG->dbhost    = 'localhost';
   $CFG->dbname    = 'moodle';
   $CFG->dbuser    = 'moodleuser';
   $CFG->dbpass    = 'Passwrd@12';
   $CFG->prefix    = 'mdl_';
   $CFG->wwwroot   = 'http://192.XXX.X.XXX';
   $CFG->dataroot  = '/var/www/moodledata';
   $CFG->directorypermissions = 0777;
   require_once(__DIR__ . '/lib/setup.php');
   ```
3. **Set permissions:**
   ```bash
   chmod -R 777 /var/www/moodledata
   ```

---

### **Step 8: Complete Moodle Installation**

1. **Access Moodle in your browser:**
   - Navigate to `http://192.XXX.X.XXX`.
2. **Follow the Moodle setup wizard:**
   - Confirm database settings:
     - Database: `moodle`
     - User: `moodleuser`
     - Password: `mdl@123`
   - Complete the installation.

---

### **Step 9: Verify Installation**

1. Ensure all required PHP extensions are installed:
   ```bash
   php -m
   ```
   If extensions are missing, install them using:
   ```bash
   apk add php82-<extension_name>
   ```
   Example: `apk add php82-soap`.

2. Restart services:
   ```bash
   rc-service php-fpm82 restart
   rc-service nginx restart
   ```

---

### **Step 10: Share the VM**

1. Export the VM as a `.vdi` file:
   - In VirtualBox, go to **File > Export Appliance** and select your Alpine VM.
2. Share the `.vdi` file via a platform like OneDrive.
   - Example: `https://onedrive.live.com/?id=example`.

---

### **Default VM Credentials**

- **Username**: `moodle`
- **Password**: `mdl@123`

