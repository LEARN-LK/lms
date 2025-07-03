# LIAF SSO - Auth SAML2 (Recommended)

LIAF SSO facilitates Moodle admins to get rid of need of creating student/staff user account manually. The people can access the Moodle site either by their [eduID](https://eduid.lk/) or their campus credentials.

The document describes the way to implement the [LIAF Single Sign-On (SSO)](https://fds.ac.lk/?entityID=https%3A%2F%2Fmdqtest.learn.ac.lk%2Fmoodle%2Fauth%2Fsaml2%2Fsp%2Fmetadata.php&return=https%3A%2F%2Fmdqtest.learn.ac.lk%2Fmoodle%2Fauth%2Fsaml2%2Fsp%2Fmodule.php%2Fsaml%2Fsp%2FdiscoResponse%3FAuthID%3D_d74a632720fb9ac65e78981fcf2cb59df22ff2e252%253Ahttps%253A%252F%252Fmdqtest.learn.ac.lk%252Fmoodle%252Fauth%252Fsaml2%252Fsp%252Fmodule.php%252Fsaml%252Fsp%252Flogin%252Fmdqtest.learn.ac.lk%253FReturnTo%253Dhttps%25253A%25252F%25252Fmdqtest.learn.ac.lk%25252Fmoodle%25252Fauth%25252Fsaml2%25252Flogin.php%25253Fwants%252526idp%25253Dc20fdc0a583f7d847e917aa67c86089a%252526passive%25253Doff&returnIDParam=idpentityid)   for Moodle.

<!-- The LIAF SSO document describes how to implement Single Sign-On (SSO) for their Learning Management System (LMS). It likely provides instructions on configuring and integrating SSO, enabling users to access the LMS with a single set of login credentials across various systems. This approach improves user convenience and security by minimizing the need to remember multiple passwords and simplifying the authentication process.-->

***Tested and verified on*** 

* OS version : Ubuntu 22.04
* php version : 8.1.2
* Moodle Version : 4.3

## 01 - Installing the auth_saml2 Plugin for Moodle 
Use the following steps for the installation of the auth_saml2 plugin via the Moodle site interface:

<!-- **i.** Take administrative control of your Moodle installation.
* Navigate to Site Administration in the admin menu > click on Plugins, and select the option to install plugins. Next > click on the button labeled "Install plugins from the Moodle plugins directory."
**ii.**  At this moment you might be required to log in to your moodle.org account. Locate the auth_saml2 plugin page and press Install now button.
**iii.**  On the next screen, click I want to install the plugin on the following site (the site with auth_saml2 is required).  -->


#### i. Take Administrative Control:

   - Navigate to Site Administration in the admin menu.
   - Click on Plugins.
   - Select the option to install plugins.
   - Next, click on the button labeled "Install plugins from the Moodle plugins directory."
     
#### ii. Locate and Install the Plugin:

- (Optional) You might be prompted to log in to your moodle.org account.
- Locate the auth_saml2 plugin page and press the Install now button.
  
#### iii. Confirm Installation:

- On the next screen, click I want to install the plugin on the following site (the site with auth_saml2 is required).


#### iv. if you having this kind of error:

> [!NOTE]
> There is a request to install plugin Auth_SAML2 from the Moodle plugins directory on this site. However, the location /var/www/html/moodle/mod is not writable. You need to give write access for the web server user to the location, then press the continue button to repeat the check.


#### v. follow this Step :
<pre><code>sudo chown -R www-data:www-data /var/www/html/moodle/auth
sudo chmod -R 755 /var/www/html/moodle/auth
</code></pre>


<!-- **vi.**  You'll be redirected back to your site; confirm the installation by clicking on "Continue."

**vii.**  Review the installation log and look for any error messages. Afterward, click "Continue" again.
     
**viii.**  You are now on the Plugins check page. Confirm that the Auth_SAML2 plugin status is set to "To be installed." Continue by clicking the button labeled "Upgrade Moodle database now" (Note: This process may take some time).
  
**ix.**  You should now see a message from the Auth_SAML2 plugin. Take note of whether the content types were automatically installed. If not, proceed to the next section on uploading and creating content. Click "Continue" when you are ready to proceed.

**x.**  Verify the Auth_SAML2 Settings and press Save changes. The default settings should be fine for most sites. -->

#### Vi. Confirm Installation: 
- You'll be redirected back to your site.
- Click "Continue."

#### Vii. Review Installation Log:
- Review the installation log for any error messages.
- Click "Continue."

#### Viii .Check Plugin Status:
 - You are now on the Plugins check page.
- Confirm that the Auth_SAML2 plugin status is set to "To be installed."
- Click "Upgrade Moodle database now."

#### ix Note Content Type Installation:
- You should see a message from the Auth_SAML2 plugin.
- Note whether the content types were automatically installed.
- Click "Continue."

#### x Verify Auth_SAML2 Settings:
- Verify the Auth_SAML2 Settings.
- Click "Save changes."



## 02.Configure the Moodle core.

### 02.1 Add following line to the Moodle config.php
  To add the configuration setting `$CFG->auth_saml2_disco_url` in your Moodle configuration file, follow these steps:

#### i. **Access the Moodle Server:**
   - Use SSH or direct access to your Moodle server to open a terminal.

#### ii. **Locate the Moodle Configuration File:**
   - The Moodle configuration file is usually named `config.php` and is located in the root directory of your Moodle installation (typically `/var/www/html/moodle/`).

#### iii. **Edit the Configuration File:**
   - Open the `config.php` file with a text editor such as `nano` or `vim`:

     ```bash
     sudo nano /var/www/html/moodle/config.php
     ```
     or
     ```bash
     sudo vim /var/www/html/moodle/config.php
     ```

#### iv. **Add the Configuration Setting:**
   
   - Add the following line:
     ```php
     $CFG->auth_saml2_disco_url = 'https://fds.ac.lk';
     ```
#### v. **Save and Exit the Editor:**
   - If you are using `nano`, press `CTRL + X`, then `Y` to confirm the changes, and `Enter` to save.
   - If you are using `vim`, press `ESC`, type `:wq`, and press `Enter` to save and exit.

#### vi. **Restart the Web Server (Optional):**
   - Although not always necessary, it's a good idea to restart your web server to ensure all changes are applied:
     ```bash
     sudo systemctl restart apache2
     ```
     or
     ```bash
     sudo systemctl restart httpd
     ```

## 02.2. Edit the `module.php` 
file in your Moodle installation and change the required file path, follow these steps:

#### i. **Access the Moodle Server:**
   - Use SSH or direct access to connect to your Linux server where Moodle is installed.

#### ii.. **Navigate to the SAML2 Plugin Directory:**
   - Use the `cd` command to navigate to the directory where the `module.php` file is located:

     ```bash
     cd /var/www/html/moodle/auth/saml2/sp/
     ```

   - Adjust the path if your Moodle installation is located in a different directory.

#### iii. **Open the `module.php` File:**
   - Open the `module.php` file using a text editor such as `nano` or `vim`:

     ```bash
     sudo nano module.php
     ```
     or
     ```bash
     sudo vim module.php
     ```

#### iv. **Find and Edit the Required Line:**
   - Look for the following line in the `module.php` file:

     ```php
     require($CFG->dirroot.'/auth/saml2/.extlib/simplesamlphp/www/module.php');
     ```
   - Change it to:
     ```php
     require($CFG->dirroot.'/auth/saml2/.extlib/simplesamlphp/public/module.php');
     ```
   - Ensure the change is exact, with no additional spaces or errors.

#### v. **Save and Exit the Editor:**
   - If you are using `nano`, press `CTRL + X`, then `Y` to confirm the changes, and `Enter` to save.
   - If you are using `vim`, press `ESC`, type `:wq`, and press `Enter` to save and exit.
     

### 02.3. EDIT `auth/saml2/config/config.php` file
To add the line `'tempdir' => '/var/moodledata',` to the `auth/saml2/config/config.php` file in your Moodle installation, follow these steps:

#### i. **Navigate to the SAML2 Plugin Configuration Directory:**
   - Use the `cd` command to navigate to the directory where the `config.php` file is located:
     ```bash
     cd /var/www/html/moodle/auth/saml2/config/
     ```
#### ii. **Open the `config.php` File:**
   - Open the `config.php` file using a text editor such as `nano` or `vim`:
     ```bash
     sudo nano config.php
     ```
     or
     ```bash
     sudo vim config.php
     ```
#### iii. **Add the `tempdir` Configuration:**
   - Look through the file to see if the `'tempdir'` setting is already present.
   - If it is not present, add the following line within the array structure (usually within a section defining various settings):

     ```php
     'tempdir' => '/var/moodledata',
     ```

   - Ensure you place this line correctly within the configuration array, following the syntax of the existing entries. Typically, it should be added within the array like so:

     ```php
     return array(
         'setting1' => 'value1',
         'setting2' => 'value2',
         'tempdir'  => '/var/moodledata',
         // Other settings...
     );
     ```
   - If the line already exists, you don't need to add it again.

#### iv. **Save and Exit the Editor:**
   - If you are using `nano`, press `CTRL + X`, then `Y` to confirm the changes, and `Enter` to save.
   - If you are using `vim`, press `ESC`, type `:wq`, and press `Enter` to save and exit.

## 03.Moodle UI Configuration 
### 03.1 enable and configure SAML2 authentication in Moodle:

#### i. **Log in to Moodle as an Administrator:**
   - Open your web browser and log in to your Moodle site using an account with administrative privileges.

#### ii. **Navigate to Manage Authentication:**
   - From the Moodle dashboard, go to:
     ```
     Site Administration -> Plugins -> Manage Authentication
     ```
#### iii. **Enable SAML2 Authentication:**
   - On the "Manage Authentication" page, scroll down to find the "SAML2" authentication method.
   - Click the eye icon (👁️) next to "SAML2" to enable it if it is not already enabled.

#### iv. **Access SAML2 Settings:**
   - After enabling SAML2, click on the "Settings" link next to the SAML2 authentication method to configure its settings.

#### v. **Configure SAML2 Settings:**
   - Set the following values in the SAML2 settings page:
     - **IdP metadata xml:**
       ```
       https://fr.ac.lk/signedmetadata/metadata.xml
       ```
     - **IdP label override:**
       ```
       LEARN SSO
       ```
     - **Federation Discovery Service:**  
       Find the option to make Federation Discovery Service active from the list of available IdPs and ensure it is enabled.
     - **Enable logging to file:**
       - Select `Yes` to enable logging.
     - **Auto create users:**
       - Select `Yes` to allow the automatic creation of users.
     - **Mapping IdP:**
       - Set this to `uid`.
     - **Attempt IdP Signout:**
       - Set this to `No`.

#### vi. **Access Data Mapping Settings:**
   - Scroll down the SAML2 settings page until you find the **Data mapping** section.

#### vii. **Set Data Mapping Fields:**
   - Configure the following mappings:
     - **Username:**
       - Set the field to `uid`.
       - Check the box to lock this field, ensuring it cannot be changed by users.
     - **First name:**
       - Set the field to `givenName`.
       - Check the box to lock this field.
     - **Last name:**
       - Set the field to `sn`.
       - Check the box to lock this field.
     - **Email address:**
       - Set the field to `mail`.
       - Check the box to lock this field.

#### viii. **Save the Configuration:**
   - Once all the settings are configured, scroll down and click the "Save changes" button to apply the changes.
   - 



### 3.2  Generate Moodle SAML2 certificate and register with LIAF
To generate a certificate, download SP metadata, and register it at LIAF for your Moodle site's SAML2 configuration, follow these steps:

#### i. **Navigate to SAML2 Settings:**
   - From the Moodle dashboard, go to:
     ```
     Site Administration -> Plugins -> Authentication -> SAML2
     ```
   - This will take you to the settings page for the SAML2 authentication method.

#### ii. **Generate the Certificate:**
   - In the SAML2 settings page, scroll down to the **Generate Certificate** section.
   - Click the **Generate** button to create the certificate.

#### iii. **Download SP Metadata:**
   - After generating the certificate, locate the option to download the Service Provider (SP) metadata file.
   - Click the link to **Download SP Metadata** and save the file to your computer.

#### iv. **Register at LIAF:**
   - Visit the LIAF (Lanka Identity and Access Federation) registration page:
     ```
     https://liaf.ac.lk/#join
     ```
   - Follow the instructions on the LIAF site to register your Service Provider. This will typically involve:
     - Filling out an application form.
     - Uploading the SP metadata file you downloaded in the previous step.
   - After submitting your registration, your campus will need to sign the LIAF Service Provider application.

##  04 Steps for logging into Moodle using LIAF SSO

   - **Browse to the Moodle URL**: Visit the specified Moodle URL (Your Domain).
   - **Select the Login Button**: Click the login button located in the top right corner of the screen.
   - **Choose LIAF SSO**: You'll be redirected to a login page. Select the "LIAF SSO" login button.
   - **Choose Your Institution**: If your institution is part of a federation, use the dropdown button to select your specific institution.
   - **Enter Credentials**: Enter your institutional username and password.
   - **Login**: Click the "Login" or "Sign In" button. Your institution's authentication system will verify your identity.
   - **Access Moodle**: After successful authentication, you will be logged into your Moodle account.

