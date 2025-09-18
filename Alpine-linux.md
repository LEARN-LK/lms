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
   apk update
   apk add nginx mariadb mariadb-client openrc
   apk add php83 php83-fpm php83-opcache php83-gd php83-mysqli php83-zlib \
   php83-curl php83-xml php83-mbstring php83-zip php83-intl php83-json \
   php83-soap php83-xmlreader php83-xmlwriter php83-tokenizer php83-fileinfo \
   php83-sodium php83-exif php83-iconv php83-session php83-simplexml

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
   wget https://download.moodle.org/download.php/direct/stable405/moodle-latest-405.tgz
   ```
2. **Extract Moodle:**
   ```bash
   tar -xvzf moodle-latest-405.tgz
   rm moodle-latest-405.tgz
   ```
3. **Create the Moodle data directory:**
   ```bash
   mkdir /var/www/moodledata
   chown -R nginx:nginx /var/www/moodle /var/www/moodledata
   chmod -R 777 /var/www/moodledata
   ```

---
### **Step 5: Configure PHP**
 Edit:   **/etc/php83/php.ini:**
  
 ```bash
 upload_max_filesize = 128M
post_max_size = 128M
max_execution_time = 300
memory_limit = 256M
max_input_vars = 5000

   ```








### **Step 6: Configure Nginx**
0. **Move the default config:**
    ```bash
   mv /etc/nginx/http.d/default.conf /etc/nginx/http.d/default.conf.bak
   ```

1. **Edit the Nginx configuration:**
   ```bash
   nano /etc/nginx/http.d/moodle.conf
   ```
2. **Add the following content:**
   ```nginx
    server {
    listen 80;
    listen [::]:80;
    server_name _;
    root /var/www/moodle;
    index index.php index.html index.htm;

    client_max_body_size 128M;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
        autoindex off;
    }

    location ~ [^/]\.php(/|$) {
        fastcgi_split_path_info ^(.+?\.php)(/.*)$;
        fastcgi_pass unix:/run/php-fpm83.sock;
        fastcgi_index index.php;
        include fastcgi.conf;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }

    location /dataroot/ {
        internal;
        alias /var/www/moodledata/;
    }

    location ~* \.(ico|jpg|jpeg|png|gif|svg|css|js|woff|woff2|ttf|eot|map)$ {
        expires max;
        log_not_found off;
        access_log off;
    }

    location ~ /\. {
        deny all;
    }
   } ```


3. **Test and restart Nginx:**

 ```bash
   nginx -t
   rc-service nginx restart
   ```

---

### **Step 7: Configure PHP-FPM**

1. **Edit the PHP-FPM configuration:**
   ```bash
   nano /etc/php82/php-fpm.d/www.conf
   ```

2. **Set the `user` and `group` to `nginx`:**
   ```ini
   user = nginx
   group = nginx
   listen = /run/php-fpm83.sock
   listen.owner = nginx
   listen.group = nginx
   listen.mode = 0660
   ```

3. **Restart PHP-FPM:**

   ```bash
   rc-service php-fpm82 restart
   ```

---

### **Step 8: Configure Moodle**

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

