# LEARN SSO - Auth SAML2

## 01 -To install the `auth_saml2` plugin via the Moodle site interface, follow these steps:


* Access your Moodle installation with administrator credentials. Navigate to Site Administration in the admin menu, click on Plugins, and select the option to install plugins. Next, click on the button labeled "Install plugins from the Moodle plugins directory."
  
<img src="https://github.com/LEARN-LK/lms/blob/master/img/78-h5p-plugin1.png?raw=true"  style="max-width: 100%;width: 600px;"><img src="https://github.com/LEARN-LK/lms/blob/master/img/79-h5p-plugin2.png?raw=true"  style="max-width: 100%;width: 600px;">
*  At this point, you may have to log into your moodle.org account. Locate the auth_saml2 plugin page and press the button labelled Install now.
  
<img src="https://github.com/LEARN-LK/lms/blob/master/img/80-h5p-plugin3.png?raw=true"  style="max-width: 100%;width: 600px;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/81-h5p-plugin4.png?raw=true"  style="max-width: 100%;width: 600px;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/82-h5p-plugin5.png?raw=true"  style="max-width: 100%;width: 600px;">
*  On the following screen, click the "Install now" link next to the site on which you want to install auth_saml2.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/83-h5p-plugin6.png?raw=true"  style="max-width: 100%;width: 600px;">  

* if you having this kind of error:

> [!NOTE]
> There is a request to install plugin Auth_SAML2 from the Moodle plugins directory on this site. However, the location /var/www/html/moodle/mod is not writable. You need to give write access for the web server user to the location, then press the continue button to repeat the check.


* follow this Step :
<pre><code>sudo chown -R www-data:www-data /var/www/html/moodle/auth
sudo chmod -R 755 /var/www/html/moodle/auth
</code></pre>


*  You'll be redirected back to your site; confirm the installation by clicking on "Continue."

<img src="https://github.com/LEARN-LK/lms/blob/master/img/84-h5p-plugin7.png?raw=true"  style="max-width: 100%;width: 600px;">       
*  Review the installation log and look for any error messages. Afterward, click "Continue" again.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/85-h5p-plugin8.png?raw=true"  style="max-width: 100%;width: 600px;">
     
*  You are now on the Plugins check page. Confirm that the Auth_SAML2 plugin status is set to "To be installed." Continue by clicking the button labeled "Upgrade Moodle database now" (Note: This process may take some time).
  
<img src="https://github.com/LEARN-LK/lms/blob/master/img/86-h5p-plugin9.png?raw=true"  style="max-width: 100%;width: 600px;">      
*  You should now see a message from the Auth_SAML2 plugin. Take note of whether the content types were automatically installed. If not, proceed to the next section on uploading and creating content. Click "Continue" when you are ready to proceed.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/87-h5p-plugin10.png?raw=true"  style="max-width: 100%;width: 600px;">     
*  Verify the Auth_SAML2 Settings and press Save changes. The default settings should be fine for most sites.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/88-h5p-plugin11.png?raw=true"  style="max-width: 100%;width: 600px;">   


## 02. Add following line to the Moodle config.php
  To add the configuration setting `$CFG->auth_saml2_disco_url` in your Moodle configuration file, follow these steps:

### i. **Access the Moodle Server:**
   - Use SSH or direct access to your Moodle server to open a terminal.

### ii. **Locate the Moodle Configuration File:**
   - The Moodle configuration file is usually named `config.php` and is located in the root directory of your Moodle installation (typically `/var/www/html/moodle/`).

### iii. **Edit the Configuration File:**
   - Open the `config.php` file with a text editor such as `nano` or `vim`:

     ```bash
     sudo nano /var/www/html/moodle/config.php
     ```
     or
     ```bash
     sudo vim /var/www/html/moodle/config.php
     ```

### iv. **Add the Configuration Setting:**
   
   - Add the following line:
     ```php
     $CFG->auth_saml2_disco_url = 'https://fds.ac.lk';
     ```
### v. **Save and Exit the Editor:**
   - If you are using `nano`, press `CTRL + X`, then `Y` to confirm the changes, and `Enter` to save.
   - If you are using `vim`, press `ESC`, type `:wq`, and press `Enter` to save and exit.

### vi. **Restart the Web Server (Optional):**
   - Although not always necessary, it's a good idea to restart your web server to ensure all changes are applied:
     ```bash
     sudo systemctl restart apache2
     ```
     or
     ```bash
     sudo systemctl restart httpd
     ```

  
