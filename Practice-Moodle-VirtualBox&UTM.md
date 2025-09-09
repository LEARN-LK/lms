
# **Practice Moodle in VirtualBox / UTM**

### Step-by-Step Guide to Share Alpine Linux Virtual Machine with Moodle Preconfigured

This guide explains how to set up a preconfigured virtual machine and practice Moodle. Instructions are provided separately for **VirtualBox users (Windows/Linux/macOS Intel/AMD)** and **UTM users (macOS Apple Silicon M1/M2/M3)**.

---

## **Part 1: Step-by-Step Instructions for VirtualBox Users (Intel/AMD)**

### **1. Download and Install VirtualBox**:

1. Visit [VirtualBox’s official site](https://www.virtualbox.org/).
2. Download the latest version for your operating system (Windows/macOS/Linux).
3. Install VirtualBox using the default options.

---

### **2. Download the `.ova` File**:

1. Open the Google Drive link provided:

   ```
   https://drive.google.com/file/d/1AUnJanfNOT-sOQ_8J8ihS8WfgQdSTEVR/view?usp=sharing&hl=en&tab=t.0
   ```
<!-- https://drive.google.com/file/d/1AUnJanfNOT-sOQ_8J8ihS8WfgQdSTEVR/view?usp=sharing-->
   
2. Download the `.ova` file.

---

### **3. Import the `.ova` File**:

1. Launch **VirtualBox**.
2. Go to **File > Import Appliance**.
3. Select the downloaded `.ova` file.
4. Review settings (CPU, memory, network).
5. Click **Import** and wait for the process to complete.

---

### **4. Start the Virtual Machine**:

1. Select the VM in VirtualBox and click **Start**.
2. Log in with:

   * **Username**: `moodle`
   * **Password**: `mdl@123`

---

## **Part 2: Step-by-Step Instructions for UTM Users (Mac Apple Silicon M1/M2/M3)**

### **1. Download and Install UTM**:

1. Visit [UTM’s official site](https://mac.getutm.app/).
2. Download the **macOS (Universal)** version.
3. Open the `.dmg` file and drag **UTM.app** to your Applications folder.

---

### **2. Download the `.utm` File**:

1. Open the Google Drive link provided (UTM version).
 ```
   https://drive.google.com/file/d/1lTmono6KG2KkGD6V8n_4uAZRNrQV-iyo/view?usp=sharing&hl=en&tab=t.0
   ```
<!-- https://drive.google.com/file/d/1lTmono6KG2KkGD6V8n_4uAZRNrQV-iyo/view?usp=sharing-->

2. Download the `.utm` file to your **Downloads** folder.

---

### **3. Import the `.utm` File into UTM**:

1. Launch **UTM.app**.
2. Go to **File > Import Virtual Machine** or click the **+** icon.
3. Browse to the downloaded `.utm` file and import it.
4. The VM will appear in your UTM library.

---

### **4. Start the Virtual Machine**:

1. Select the VM and click **Play ▶**.
2. Log in with:

   * **Username**: `moodle`
   * **Password**: `mdl@123`

---

## **Part 3: Configure Networking and Access Moodle (Both VirtualBox & UTM Users)**

### **5. Find the VM IP Address**:

Inside the VM, run:

```bash
ip addr
```

Note the IP (e.g., `192.168.1.10`).

---

### **6. Map Moodle to a Hostname on Host Machine**:

#### **Windows**:

* Edit file: `C:\Windows\System32\drivers\etc\hosts`
* Add:

  ```
  192.168.1.10 mymoodle.test.learn.ac.lk
  ```

#### **macOS**:

* Edit file: `/private/etc/hosts`

```bash
sudo nano /private/etc/hosts
```

* Add:

  ```
  192.168.1.10 mymoodle.test.learn.ac.lk
  ```

 * Save in nano:
   * **Ctrl + O** → Enter → **Ctrl + X**

#### **Linux**:

* Edit file: `/etc/hosts`

```bash
sudo nano /etc/hosts
```

* Add:

  ```
  192.168.1.10 mymoodle.test.learn.ac.lk
  ```

 * Save in nano:
   * **Ctrl + O** → Enter → **Ctrl + X**

#### How to Save & Exit in Nano Editor

When editing files with nano (like /etc/hosts or config.php):

- Make your changes (type or paste text).
- Press Ctrl + O → Writes (saves) the file.
- It will ask for the filename — just press Enter to confirm.
Press Ctrl + X → Exits Nano.

---

### **7. Access Moodle**:

1. Open a browser on the host machine.
2. Visit:

   ```
   http://mymoodle.test.learn.ac.lk
   ```
3. Default Moodle login:

   * **Username**: `moodle`
   * **Password**: `Mdl@1234`

---

## **Part 4: Troubleshooting**

### **Site Not Loading**

Restart services:

```bash
rc-service nginx restart
rc-service php-fpm82 restart
```

<!-- ### **Permission Issues**

```bash
chmod -R 777 /var/www/moodledata
```

### **Error Logs**

```bash
tail -f /var/log/nginx/error.log
``` -->

### **Renew DHCP Lease**

```bash
/etc/init.d/networking restart 
```

Then recheck the IP (Step 5).

<!-- ### **Plugin Installation Errors**

Edit `config.php`:

```php
@error_reporting(E_ALL | E_STRICT);
@ini_set('display_errors', '1');
$CFG->debug = (E_ALL | E_STRICT);
$CFG->debugdisplay = 1;
```

### **Update PHP-FPM User/Group**

Edit:

```bash
vi /etc/php82/php-fpm.d/www.conf
```

Set:

```
user = nginx
group = nginx
```   -->

Restart PHP-FPM:

```bash
rc-service php-fpm82 restart
```
<!-- 
Set Moodle config directory permissions:

```php
$CFG->directorypermissions = 0777;
```  -->

---

👉 Now your guide supports **both VirtualBox (.ova)** and **UTM (.utm)** users, while keeping the Moodle practice setup steps common.

- Ensure VirtualBox's network settings are set to **Bridged Adapter**.
- Ensure the VM is running before accessing Moodle.
- Default credentials for the Moodle:
  - **Username**: `moodle`
  - **Password**: `Mdl@1234`
