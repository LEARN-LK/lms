## Workplace Course Certificate

The **Workplace Course Certificate** plugin for Moodle allows organizations to issue digital certificates to participants upon course completion. It works as an activity within Moodle, enabling instructors to create and assign certificates automatically based on specific course requirements. The certificates can display personalized user data such as the student's name and course details.

This plugin is typically paired with the **Certificate Manager**, which provides tools to design reusable certificate templates. Templates can include digital signatures, verification QR codes, and dynamic data. Once the templates are set up in the Certificate Manager, the Workplace Course Certificate module pulls the relevant data to generate certificates when students meet predefined conditions, such as completing a final test.

Participants can access their certificates directly within the course or receive them via email in PDF format. Additionally, QR codes embedded in the certificates allow anyone to validate them even if the Moodle site has restricted guest access.

These tools are especially useful in workplace environments and structured courses, where automated and verifiable certification is required to acknowledge achievements systematically.

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


### Step 5: **Design Certificate Templates**  
1. Go to **Site Administration > Certificate Manager** (provided by the `tool_certificate` plugin).  
2. Create a new template and add dynamic fields like course name, student name, date, and a QR code for verification.


### Step 6: **Add Certificate Activity to a Course**  
1. In the course where you want to issue certificates, click **Add an activity or resource**.  
2. Select **Course Certificate** from the list.  
3. Configure the activity’s settings (e.g., restrict access to students who have completed the course).

### Step 7: **Test the Plugin**  
- Assign the certificate to a test user and verify the PDF download or email functionality.  
- Scan the QR code (if used) to validate the certificate.



