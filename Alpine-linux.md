## Moodle installation.

Here is a step-by-step guide to installing Moodle on Alpine Linux running in VirtualBox. The setup includes using Nginx, PHP-FPM, and MariaDB.

---

#### **1. Prepare Virtual Machine in VirtualBox**
- Create a VM with **Alpine Linux** as the operating system.
- Allocate at least **2 GB RAM** and **20 GB disk space**.
- Boot the VM with the Alpine Linux ISO and complete the installation.

---

#### **2. Update and Install Required Packages**
1. Update the system:
   ```bash
   apk update && apk upgrade
   ```
2. Install necessary packages:
   ```bash
   apk add nginx php82 php82-fpm php82-mysqli php82-iconv php82-curl php82-opcache php82-gd php82-xml php82-xmlreader php82-sodium php82-ctype php82-intl php82-zip mariadb mariadb-client curl wget unzip
   ```

---

#### **3. Configure PHP**
1. Edit the PHP configuration:
   ```bash
   nano /etc/php82/php.ini
   ```
2. Update these values:
   ```ini
   max_input_vars = 5000
   memory_limit = 256M
   post_max_size = 100M
   upload_max_filesize = 100M
   ```
3. Restart PHP-FPM:
   ```bash
   rc-service php-fpm82 restart
   ```

---

#### **4. Set Up MariaDB**
1. Start MariaDB:
   ```bash
   rc-service mariadb start
   ```
2. Secure the installation:
   ```bash
   mysql_secure_installation
   ```
   - Remove anonymous users: Yes
   - Disallow root login remotely: Yes
   - Remove test database: Yes
   - Reload privilege tables: Yes
3. Create a Moodle database:
   ```sql
   CREATE DATABASE moodle CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY 'yourpassword';
   GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
   FLUSH PRIVILEGES;
   ```

---

#### **5. Install Moodle**
1. Download Moodle:
   ```bash
   cd /var/www
   wget https://download.moodle.org/stable403/moodle-latest-403.tgz
   tar -xvzf moodle-latest-403.tgz
   ```
2. Set permissions:
   ```bash
   mkdir -p /var/www/moodledata
   chown -R nginx:nginx /var/www/moodle /var/www/moodledata
   chmod -R 775 /var/www/moodledata
   ```

---

#### **6. Configure Nginx**
1. Create a new Nginx configuration file:
   ```bash
   nano /etc/nginx/http.d/moodle.conf
   ```
2. Add the following:
   ```nginx
   server {
       listen 80;
       server_name localhost [VM IP];

       root /var/www/moodle;
       index index.php index.html index.htm;

       location / {
           try_files $uri $uri/ =404;
       }

       location ~ [^/]\.php(/|$) {
           include fastcgi_params;
           fastcgi_split_path_info ^(.+\.php)(/.+)$;
           fastcgi_index index.php;
           fastcgi_pass 127.0.0.1:9000;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
       }

       location ~* \.(?:ico|css|js|gif|jpe?g|png|svg|webp|ttf|woff|woff2|otf|eot)$ {
           try_files $uri /index.php$is_args$args;
           expires max;
           access_log off;
           add_header Cache-Control "public";
       }
   }
   ```
3. Restart Nginx:
   ```bash
   rc-service nginx restart
   ```

---

#### **7. Access the Moodle Installation Wizard**
1. Open a browser and go to:
   ```
   http://<your-VM-IP> (e.g., http://192.168.56.101)
   ```
2. Follow the installation wizard:
   - Select database type: `mariadb`
   - Enter database details:
     - **Host**: `localhost`
     - **Database**: `moodle`
     - **User**: `moodleuser`
     - **Password**: `yourpassword`
   - Complete the installation steps.

---

#### **8. Configure `config.php`**
During the installation, Moodle generates a `config.php` file automatically in `/var/www/moodle/`. If needed, you can manually edit the file:

1. Open the `config.php` file:
   ```bash
   nano /var/www/moodle/config.php
   ```
2. Verify key settings:
   ```php
   $CFG->dbtype    = 'mariadb';
   $CFG->dblibrary = 'native';
   $CFG->dbhost    = 'localhost';
   $CFG->dbname    = 'moodle';
   $CFG->dbuser    = 'moodleuser';
   $CFG->dbpass    = 'yourpassword';
   $CFG->wwwroot   = 'http://<your-VM-IP>';
   $CFG->dataroot  = '/var/www/moodledata';
   ```

---



#### **09. Verify and Finalize**
- Ensure that CSS and JavaScript load correctly.
- If the site still appears without CSS, purge caches:
   ```bash
   php82 admin/cli/purge_caches.php
   ```
- Adjust any additional permissions or configurations as needed.

---
