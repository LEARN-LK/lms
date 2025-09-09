## Here is the complete guide to **installing the language pack** 
---

## Step 1: Install the Sinhala /Tamil Language Pack in Moodle
###  Install via Moodle Web Interface (Recommended)
1. **Login as Admin** to your Moodle site.
2. Go to **Site administration > Language > Language packs**.



3. Find **Sinhala (si) Tamil (ta_lk)** in the available language list.
4. Select it and click **Install selected language pack**.
5. Once installed, go to **Site administration > Language > Language settings**.
6. Set **Default language** to **Sinhala (si) or Tamil (ta_lk)**.
7. Click **Save changes**.
8. Change the **Language**
<img src="https://github.com/LEARN-LK/lms/blob/master/img/lan.png" alt="image" style="max-width: 100%;width: 300px;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/lan2.png" alt="image" style="max-width: 100%;width: 300px;">


---

## **Step 2: Allow Sinhala/Tamil Text Input**
Since Moodle does not translate typed text, you need a **Sinhala/Tamil keyboard**.

### **Enable Sinhala/Tamil Keyboard on Your Computer**
#### **For Windows**
1. Open **Settings > Time & Language > Language & Region**.
2. Click **Add a language**, search for **Sinhala/Tamil**, and install it.
3. Select **Keyboard options** → Choose **Sinhala Wijesekara** or **Sinhala Phonetic**.
4. Switch between English/Sinhala using **Alt + Shift** or **Win + Space**.

#### **For Ubuntu/Linux**
1. Install Sinhala keyboard:
   ```bash
   sudo apt install ibus-m17n
   ```
2. Go to **Settings > Region & Language**.
3. Click **+ Add Input Source**, search for **Sinhala**, and select it.
4. Switch languages with **Super (Windows key) + Space**.

#### **For macOS**
1. Open **System Preferences > Keyboard > Input Sources**.
2. Click **+**, choose **Sinhala/Tamil**, and select a layout.
3. Switch between languages using **Command + Space**.

---

## **Step 3: Clear Moodle Cache**
To apply changes, **purge caches**:
- Go to **Site administration > Development > Purge caches**.
- Click **Purge all caches**.


___
## Troubleshoot options 

###  If `504` error occurs (in the testbed environment), restart services:
   ```bash
   rc-service nginx restart
   rc-service php-fpm82 restart
   ```


### Manual Installation (If the server has no internet)
1. Download the **Sinhala language pack** manually from:  
   👉 [https://download.moodle.org/langpack/4.3/](https://download.moodle.org/langpack/4.3/)  
   (Select `si.zip` for Sinhala)
<!-- 2. Transfer the `si.zip` file to your Moodle server:
   ```bash
   scp si.zip user@your-server:/tmp/
   ```
3. Extract and move it to Moodle’s language directory:
   ```bash
   mkdir -p /var/www/moodledata/lang
   unzip /tmp/si.zip -d /var/www/moodledata/lang/
   chown -R nginx:nginx /var/www/moodledata/lang/
   ```
4. Verify by going to **Site administration > Language packs**. -->

---   

<!-- ## Force Sinhala as Default Language
If the interface is still in English:
1. Open **config.php**:
   ```bash
   nano /var/www/moodle/config.php
   ```
2. Add this line at the end:
   ```php
   $CFG->lang = 'si';
   ```
3. Save and restart services:
   ```bash
   rc-service nginx restart
   rc-service php-fpm82 restart
   ```

--- -->
##  Verify Sinhala Text Rendering in Moodle
If Sinhala text does not display correctly:
1. **Use Google Input Tools**  
   - Visit [Google Input Tools](https://www.google.com/inputtools/try/)
   - Select **Sinhala** and type.

2. **Use Online Sinhala Transliteration Tools**
   - [Google Translate](https://translate.google.com/)
   - [Sinhala Unicode Converter](https://www.ucsc.lk/ltrl/services/feconverter/)

3. **Install Sinhala Unicode Fonts**  
   - **For Alpine Linux**:
     ```bash
     apk add fonts-noto
     ```
   - **For Windows/macOS**:  
     Download Sinhala fonts from [UCSC](https://www.ucsc.lk/).
---
<!-- ### Alternatively, run:
  ```bash
  rm -rf /var/www/moodledata/cache/*
  ```

---  -->
