## Moodle installation.

Here is a step-by-step guide to installing Moodle on Alpine Linux running in VirtualBox. The setup includes using Nginx, PHP-FPM, and MariaDB.

---

### **Step 1: Prepare VirtualBox Environment**
1. **Create a new VM**:
   - Open VirtualBox and create a new VM.
   - Choose **Alpine Linux** as the OS.
   - Assign at least 1 GB of RAM and 5 GB of disk space.
2. **Attach Alpine Linux ISO**:
   - Download the latest Alpine Linux ISO.
   - Attach the ISO as the boot device for your VM.
3. **Start the VM** and install Alpine Linux:
   - Boot into the Alpine Linux installer.
   - Follow the prompts to install Alpine Linux.

---

### **Step 2: Install Required Packages**
1. **Update the system**:
   ```bash
   apk update && apk upgrade
   ```
2. **Install necessary packages**:
   ```bash
   apk add nginx php82 php82-fpm php82-mysqli php82-iconv php82-curl php82-opcache php82-gd php82-xml php82-xmlreader php82-sodium php82-ctype php82-intl php82-zip mariadb mariadb-client curl wget unzip
   ```

---

### **Step 3: Configure PHP**
1. **Edit the PHP configuration file**:
   ```bash
   vi /etc/php82/php.ini
   ```
2. **Update the following settings**:
   ```ini
   max_input_vars = 5000
   memory_limit = 256M
   post_max_size = 100M
   upload_max_filesize = 100M
   ```
3. **Restart PHP-FPM**:
   ```bash
   rc-service php-fpm82 restart
   ```

---

### **Step 4: Configure MariaDB**
1. **Start MariaDB service**:
   ```bash
   rc-service mariadb start
   ```
2. **Secure MariaDB**:
   ```bash
   mysql_secure_installation
   ```
   - Switch to unix_socket authentication: No
   - Remove anonymous users: Yes
   - Disallow root login remotely: Yes
   - Remove test database: Yes
   - Reload privilege tables: Yes
3. **Create a database and user for Moodle**:
   ```sql
   CREATE DATABASE moodle CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY 'yourpassword';
   GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
   FLUSH PRIVILEGES;
   ```

---

### **Step 5: Install Moodle**
1. **Download Moodle**:
   ```bash
   cd /var/www
   wget https://download.moodle.org/stable403/moodle-latest-403.tgz
   tar -xvzf moodle-latest-403.tgz
   ```
2. **Set permissions**:
   ```bash
   mkdir -p /var/www/moodledata
   chown -R nginx:nginx /var/www/moodle /var/www/moodledata
   chmod -R 775 /var/www/moodledata
   ```
3. **Create a config.php file**:
   Access Moodle via a browser to generate the config.php file (see step 7).

---

### **Step 6: Configure Nginx**
1. **Edit Nginx configuration**:
   ```bash
   nano /etc/nginx/http.d/moodle.conf
   ```
2. **Add the following configuration**:
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
           fastcgi_param  PATH_INFO $fastcgi_path_info;
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
3. **Restart Nginx**:
   ```bash
   rc-service nginx restart
   ```

---

### **Step 7: Access Moodle**
1. **Access the Moodle site**:
   - Open a browser on the host machine and go to:
     ```
     http://<your-VM-IP> (e.g., http://192.168.56.101)
     ```
2. **Follow the installation wizard**:
   - Enter database details:
     - Type: `mariadb`
     - Host: `localhost`
     - Database name: `moodle`
     - User: `moodleuser`
     - Password: `yourpassword`
   - Complete the installation process.

---




