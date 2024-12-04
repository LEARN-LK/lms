## Practice Moodle in VirtualBox

### Step-by-Step Guide to Share Alpine Linux `.vdi` File with Moodle Preconfigured  

This guide explains how to set up a `.vdi` file with Alpine Linux, configure it for sharing, and provide instructions for others to use it in VirtualBox.

---

### **Part 1: Step-by-Step Instructions for Users**

#### **1. Download and Install VirtualBox**:
1. Visit [VirtualBox’s official site](https://www.virtualbox.org/).
2. Download the latest version for your operating system (Windows/macOS/Linux).
3. Install VirtualBox using the default options.

#### **2. Download the `.vdi` File**:
1. Open the OneDrive link provided:
   ```
   https://onedrive.live.com/?id=examplefilelink
   ```
2. Download the `.vdi` file.

#### **3. Set Up the Virtual Machine**:
1. Open VirtualBox and click **New**.
2. Set the VM Name (e.g., `MoodleAlpine`).
3. Configure the VM:
   - **Type**: Linux
   - **Version**: Other Linux (64-bit)
   - **Memory**: 1 GB (1024 MB)
4. Select **Use an existing virtual hard disk file** and choose the downloaded `.vdi` file.
5. Go to **Settings**:
   - **Storage**: Ensure the `.vdi` file is attached as the primary disk.
   - **Network**: Under **Adapter 1**, select **Bridged Adapter**.

#### **4. Start the Virtual Machine**:
1. Click **Start** in VirtualBox.
2. Log in using:
   - **Username**: `moodle`
   - **Password**: `mdl@123`

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
2. Open Notepad as an administrator and add:
   ```
   192.168.1.10 mymoodle.learn.ac.lk
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
   192.168.1.10 mymoodle.learn.ac.lk
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
   192.168.1.10 mymoodle.learn.ac.lk
   ```

---

### **7. Access Moodle from the Host Machine**:
1. Open a browser on the host machine.
2. Navigate to:
   ```
   http://mymoodle.learn.ac.lk
   ```

---

### Notes for Users:
- Ensure VirtualBox's network settings are set to **Bridged Adapter**.
- Ensure the VM is running before accessing Moodle.
- Default credentials for the VM:
  - **Username**: `moodle`
  - **Password**: `mdl@123`

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

