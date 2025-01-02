## Practice Moodle in VirtualBox

### Step-by-Step Guide to Share Alpine Linux `.OVA` File with Moodle Preconfigured  

This guide explains how to set up a `.vdi` file with Alpine Linux, configure it for sharing, and provide instructions for others to use it in VirtualBox.

---

### **Part 1: Step-by-Step Instructions for Users**

#### **1. Download and Install VirtualBox**:
1. Visit [VirtualBox’s official site](https://www.virtualbox.org/).
2. Download the latest version for your operating system (Windows/macOS/Linux).
3. Install VirtualBox using the default options.
---
#### **2. Download the `.ova` File**:
1. Open the Google Drive link provided:
   ```
   https://drive.google.com/file/d/1bun_iIx-RaQINks6RFgXBHM8kWDEhaAq/view?usp=sharing
   ```
2. Download the `.ova file.
---
#### **3. Import the .ova File**:

1.	Launch VirtualBox:
	- Open VirtualBox from your Start Menu, Applications, or Dock.
2.	Import the Appliance:
   - Go to File > Import Appliance from the VirtualBox menu bar.
3.	Browse to the .ova File:
   - Click on the folder icon to open the file picker.
   - Locate and select the .ova file you want to import.
4.	Review Appliance Settings:
   - Click Next after selecting the file.
   - Review the virtual machine settings, including CPU, memory, and network.
5.	Import the Appliance:
   - Click Import to start the process.
   - Wait for VirtualBox to import the .ova file. This might take a few minutes.

---
#### **4. Start the Virtual Machine**:
1. Click **Start** in VirtualBox.
2. Log in using:
   - **Username**: `moodle`
   - **Password**: `mdl@123`
---
#### **5. Find the VM IP Address**:
1. Inside the VM, type:
   ```bash
   ip addr
   ```
2. Note the IP address (e.g., `192.168.1.10`).

#### **6. Map Moodle to a Hostname on Host Machine**:
- On the host machine, edit the `hosts` file to map the VM's IP to a hostname.

---

### **Edit Hosts File**

#### **Windows**:
1. Path:  
   `C:\Windows\System32\drivers\etc\hosts`
2. Open Notepad as an administrator and add your VM IP: eg:
   ```
   192.168.1.10 mymoodle.test.learn.ac.lk
   ```

#### **MacOS**:
1. Path:  
   `/private/etc/hosts`
2. Open a terminal and edit the file:
   ```bash
   sudo nano /private/etc/hosts
   ```
3. Add:
   ```
   192.168.1.10 mymoodle.test.learn.ac.lk
   ```

#### **Linux**:
1. Path:  
   `/etc/hosts`
2. Edit the file with:
   ```bash
   sudo nano /etc/hosts
   ```
3. Add:
   ```
   192.168.1.10 mymoodle.test.learn.ac.lk
   ```

---

### **7. Access Moodle from the Host Machine**:
1. Open a browser on the host machine.
2. Navigate to:
   ```
   http://mymoodle.test.learn.ac.lk
   ```

---

### Notes for Users:
- Ensure VirtualBox's network settings are set to **Bridged Adapter**.
- Ensure the VM is running before accessing Moodle.
- Default credentials for the VM:
  - **Username**: `moodle`
  - **Password**: `Mdl@1234`

This guide ensures users can easily import the `.vdi` file, configure the VM, and start practicing Moodle without additional setup.

---

### **Part 2: Troubleshooting**

Site Not Loading Properly:

Verify nginx and php-fpm services are running:
 ``` bash
rc-service nginx restart
rc-service php-fpm82 restart
```
Ensure proper permissions for `moodledata:`
 ``` bash

chmod -R 777 /var/www/moodledata
```
Error Messages:

Check logs:
``` bash

tail -f /var/log/nginx/error.log
```

Renew DHCP Lease on Alpine Linux
``` bash
/etc/init.d/networking restart
```
then follow [Step 5](https://github.com/LEARN-LK/lms/blob/master/Practice-Moodle-VirtualBox.md#5-find-the-vm-ip-address)

#### plugin installation Troubleshooting

Edit config.php in the Moodle directory:
// Add these lines at the end of config.php:
 ``` bash
@error_reporting(E_ALL | E_STRICT);
@ini_set('display_errors', '1');
$CFG->debug = (E_ALL | E_STRICT);
$CFG->debugdisplay = 1;
```

#### 1. Update PHP-FPM User and Group
   Open the PHP-FPM pool configuration file:
 ``` bash
vi /etc/php82/php-fpm.d/www.conf
```
 ``` bash
user = nginx
group = nginx
```
####  Restart PHP-FPM

 ``` bash
rc-service php-fpm82 restart
```
#### Set Permission  "$CFG->directorypermissions = 0777;"
 ``` bash
vi /var/www/moodle/config.php
```
