## Workplace Course Certificate

The **Workplace Course Certificate** plugin for Moodle allows organizations to issue digital certificates to participants upon course completion. It works as an activity within Moodle, enabling instructors to create and assign certificates automatically based on specific course requirements. The certificates can display personalized user data such as the student's name and course details.

This plugin is typically paired with the **Certificate Manager**, which provides tools to design reusable certificate templates. Templates can include digital signatures, verification QR codes, and dynamic data. Once the templates are set up in the Certificate Manager, the Workplace Course Certificate module pulls the relevant data to generate certificates when students meet predefined conditions, such as completing a final test.

Participants can access their certificates directly within the course or receive them via email in PDF format. Additionally, QR codes embedded in the certificates allow anyone to validate them even if the Moodle site has restricted guest access.

These tools are especially useful in workplace environments and structured courses, where automated and verifiable certification is required to acknowledge achievements systematically.

<!--
## installing the **Workplace Course Certificate** plugin in Moodle:

### Step 1: **Download the Plugin**  
1. Visit the Moodle plugin directory:  
   [Workplace Course Certificate](https://moodle.org/plugins/mod_coursecertificate).  
2. Download the latest version of the plugin as a ZIP file.

### Step 2: **Upload the Plugin to Moodle**  
1. Log in to Moodle as an administrator.  
2. Navigate to **Site Administration > Plugins > Install plugins**.  
3. Upload the ZIP file you downloaded by dragging it into the upload box or clicking **Choose a file**.  
4. Click **Install plugin from the ZIP file**.


### Step 3: **Verify and Install**  
1. Moodle will check for dependencies, including the **Certificate Manager** plugin.  
2. If all requirements are satisfied, click **Continue** to begin the installation.  
3. Review the installation log and click **Upgrade Moodle database** to finalize the process.


### Step 4: **Configure Certificate Settings**  
1. Once installed, navigate to **Site Administration > Plugins > Activities > Course Certificate**.  
2. Configure any settings like default email behavior or display options.
-->

### Step 1: **Design Certificate Templates**  
1. Go to **Site Administration > Manage Certificate Template** (provided by the `tool_certificate` plugin).  
2. Create a new template and add dynamic fields like course name, student name, date, and a QR code for verification.
 <img src="https://github.com/LEARN-LK/lms/blob/master/img/2-Certificate-manage.png" alt="image" style="max-width: 100%;width: 800px;">

### Step 2: **Add Certificate Activity to a Course**  
1. In the course where you want to issue certificates, click **Add an activity or resource**.  
2. Select **Course Certificate** from the list.
    <img src="https://github.com/LEARN-LK/lms/blob/master/img/1-Certificate-manage.png" alt="image" style="max-width: 100%;width: 800px;">

4. Configure the activity’s settings (e.g., restrict access to students who have completed the course).
   
### Step 3: **Test the Plugin**  
- Assign the certificate to a test user and verify the PDF download or email functionality.  
- Scan the QR code (if used) to validate the certificate.

Here’s the corrected process for **issuing a certificate to students** using the Moodle Workplace Course Certificate plugin:

---

## **Issuing Certification in Moodle**

1. **Log in as Teacher or Manager:**  
   - Make sure you have the necessary permissions to issue certificates.

2. **Navigate to the Certificate Management Section:**  
   - Go to **Site Administration**.  
   - Under the **Certificates** section, click **Manage Certificate Templates**.
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/01-certification.png" alt="image" style="max-width: 100%;width: 800px;">

3. **Access the Issue Certificate Option:**  
   - Inside the Certificate Manager, click on the **Certificates** button.  
   - From the dropdown, select **Issue Certificate**.
      <img src="https://github.com/LEARN-LK/lms/blob/master/img/02-certification.png" alt="image" style="max-width: 100%;width: 800px;">

4. **Select the Student:**  
   - Choose the name of the student to whom the certificate will be issued.
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/03-certification.png" alt="image" style="max-width: 100%;width: 800px;">
5. **Save and Issue Certificate:**  
   - Click the **Save** button.  

6. **Certificate Delivery:**  
   - The certificate will automatically appear in the student’s **Moodle login** under their course or profile, and it can be downloaded directly.

