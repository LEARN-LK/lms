<h1> Mirosoft O365  </h1>
To add Microsoft 365 (O365) authentication to Moodle 4.3, you can use OAuth 2 authentication to allow users to log in using their Microsoft accounts. This involves configuring an Azure AD application and setting up Moodle to use it.


### Step 1: Set Up Azure AD Application in Microsoft 365

1. **Access Azure Active Directory:**
   - Go to the [Azure portal](https://portal.azure.com/).
   - Sign in with your Microsoft 365 administrator account.
   - Navigate to `Azure Active Directory` > `App registrations [1]`.
     
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Azure-01.png" style="max-width: 100%;width: 100%;"> 

2. **Register a New Application:**
   - Click on `New registration`.
   - Enter a name for your application [2](e.g., "Moodle O365 Authentication").
   - Choose `Accounts in this organizational directory only` or `Accounts in any organizational directory`[3] depending on your user base.
   - Under `Redirect URI`, [4] select `Web` and enter the following URI:
     ```
     https://yourmoodleurl.com/admin/oauth2callback.php
     ```
     Replace `yourmoodleurl.com` with your actual Moodle site URL.
   - Click `Register` [5].
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-02.png" style="max-width: 60%;width: 100%;"> 

3. **Configure API Permissions:**
   - After the app is created, go to `API permissions`[6].
   - Click on `Add a permission`[7], select `Microsoft Graph`,[8] and then choose `Delegated permissions`[9].
   - Add the following permissions [10]:
     - `openid`
     - `profile`
     - `email`
     - `offline_access`
   - Click `Add permissions`[11].
   - Grant admin consent for your organization.
     
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-03.png" style="max-width: 80%;width: 90%;"> 
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-04.png" style="max-width: 80%;width: 90%;"> 

4. **Create Client Secret:**
   - Go to `Certificates & secrets`[12].
   - Click on `New client secret`[13], provide a description, and set an expiration period.
   - After creating the client secret, copy the value immediately;[14] you will need this for Moodle.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-05.png" style="max-width: 80%;width: 80%;"> 


### Step 2: Configure Moodle for O365 Authentication

1. **Login to Moodle as Admin:**
   - Log in to your Moodle site as an administrator.

2. **Enable OAuth 2 Services:**
   - Go to `Site administration`[16] > `Server`[17] > `OAuth 2 services`[18].
   - Click on `Add a new service`.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m05.1.png" style="max-width: 80%;width: 80%;"> 
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m06.png" style="max-width: 50%;width: 80%;">

3. **Add Microsoft as an OAuth 2 Service:**
   - Name the service [19] (e.g., "Microsoft 365").
   - In the `Client ID` [20] field, paste the `Application (client) ID` from Azure AD.
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m14.png" style="max-width: 50%;width: 80%;"> 
   - In the `Client secret`[21] field, paste the client secret you(Certification & Secret > Value) created in Azure AD.
   - <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m15.png" style="max-width: 50%;width: 80%;"> 

<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m07.png" style="max-width: 50%;width: 80%;"> 

<!--     
   - Set the `Authorization endpoint URL` to:
     ```
     https://login.microsoftonline.com/common/oauth2/v2.0/authorize
     ```
   - Set the `Token endpoint URL` to:
     ```
     https://login.microsoftonline.com/common/oauth2/v2.0/token
     ```
   - Set the `User info endpoint URL` to:
     ```
     https://graph.microsoft.com/oidc/userinfo
     ```
   - Set the `Resource endpoint URL` to:
     ```
     https://graph.microsoft.com/
     ```
   - Enable the service by checking the `Enabled` box.
   - Click `Save changes`.  -->

  ### Additional Single Tenancy Configuration 
   - Once the above steps have been completed, Moodle O365 Authentication click "Overview" if not already selected and choose "Endpoints"

     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m08.png" style="max-width: 50%;width: 80%;"> 
     
   - From the list of endpoints copy the OpenID Connect metadata document endpoint URL. It is only necessary to copy the portion up to and including "v2.0". In the example below, the copied URL would be, "https://login.microsoftonline.com/96e0421d-d572-4839-9c32-b8bc00cf250b/v2.0/". Note that it is important to include the trailing slash.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m09.png" style="max-width: 50%;width: 80%;"> 
     
- Now return to Moodle and in the newly created OAuth2 Microsoft service, paste the endpoint in the 'Service base URL' field.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m10.png" style="max-width: 50%;width: 80%;"> 
  
-  Save your changes.


4. **Enable Microsoft 365 Login:**
   - Go to `Site administration` > `Plugins` > `Authentication` > `Manage authentication`.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m11.png" style="max-width: 50%;width: 80%;"> 
     
   - Scroll down to `OAuth 2` and make sure it's enabled.
   - Set `Microsoft 365` as an issuer.
   
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m12.png" style="max-width: 50%;width: 80%;"> 
  

### Step 3: Test Microsoft 365 Authentication

1. **Log Out:**
   - Log out of Moodle.

2. **Test the Login:**
   - Go to the Moodle login page.
   - You should now see a "Login with Microsoft" button.

     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m13.png" style="max-width: 50%;width: 80%;"> 
     
   - Click on it and log in with a Microsoft 365 account to test.



https://docs.moodle.org/403/en/OAuth_2_Microsoft_service

<hr>

<h1>Google authentication</h1>

Here is the corrected step-by-step guide:

1. **Login with Google**  
   Go to the Google Cloud Console:  
   [https://console.cloud.google.com](https://console.cloud.google.com)

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-1.png" style="max-width: 50%;width: 80%;"> 

2. **Create a New Project or Select an Existing Project [1]**
   **if you select "New Project [2], add project name and [3] Click Create button [4]"**

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-2.png" style="max-width: 50%;width: 80%;"> 

 
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-3.png" style="max-width: 50%;width: 80%;"> 
  - Select your newly created project [5].

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-4.png" style="max-width: 50%;width: 80%;"> 

4. **Navigate to the API & Services [7] > Credentials section [8]**


<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-5.png" style="max-width: 50%;width: 80%;"> 

   - Go to **API & Services** and click on **Credentials [9]**.
     
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-6.png" style="max-width: 50%;width: 80%;"> 

6. **Create OAuth 2.0 Client ID [10]**  
   - Click on **Create Credentials** and choose **OAuth client ID**.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-7.png" style="max-width: 50%;width: 80%;"> 
     
7. **Configure Consent Screen [12]**
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-8.png" style="max-width: 50%;width: 80%;"> 
   
   - Select User Type **External [13]** and click the **Create [14]** button.

       <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-8.1.png" style="max-width: 50%;width: 80%;"> 
       
   - Under **Edit app registration > OAuth Consent Screen > App Information**, fill in the required details.
  <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-9.png" style="max-width: 50%;width: 80%;"> 
     
   - In the **Authorized domain [16]s** section, add the domain of your Moodle site and provide the developer contact information.
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-10.png" style="max-width: 50%;width: 80%;"> 
   - Click **Save and Continue [17]**.

9. **Scopes Section**  
   - Click **Save and Continue** in the **Scopes** section.
   - Then, click on the **Back to Dashboard** button.
  
10. **Create OAuth Client ID**  
   - Go to **Credentials[18]** again, then click on **Create Credentials[19]** and choose **OAuth Client ID[20]**.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-11.png" style="max-width: 50%;width: 80%;"> 
     
   - Select **Web Application** as the application type [18].
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-10.1.png" style="max-width: 50%;width: 80%;">

11. **Configure Authorized Redirect URLs[21]**  
   - Add the following authorized redirect URL:  
   `https://your-moodle-site.com/admin/oauth2callback.php`

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-12.png" style="max-width: 50%;width: 80%;"> 

11. **Click Create [22]**  
   - Finally, click the **Create** button to generate your OAuth 2.0 Client ID.

     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-13.png" style="max-width: 50%;width: 80%;"> 

<hr>
12 **Configure Moodle for Google Cloud Console Authentication**

i. **Login to Moodle as Admin:**
   - Log in to your Moodle site as an administrator.

      <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-13.png" style="max-width: 50%;width: 80%;"> 

ii. **Enable OAuth 2 Services:**
   - Go to `Site administration` > `Server`[25] > `OAuth 2 services`.
   - Click on `Add a new service`[26].
   - 
        <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-m01.png" style="max-width: 50%;width: 80%;"> 

iii . **Add Google as an OAuth 2 Service:**
   - Name the service[27] (e.g., "Google").
   - In the `Client ID`[28] field, paste the `Application (client) ID` from Google Cloud Console.
   - In the `Client secret`[29] field, paste the client secret you created in Google Cloud Console.
   - 
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-m02.png" style="max-width: 50%;width: 80%;"> 

 
iv . **Enable the Google API in Moodle**
   - In the same “Manage authentication “page look for “OAuth 2” [30]in the list of authentication methods.
   - Enable the OAuth 2 authentication plugin
   - 
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-m03.png" style="max-width: 50%;width: 80%;"> 

   - After performing all the above step, you google will be coming on your loving page (as it is appearing in below screen)
   - 
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-m04.png" style="max-width: 50%;width: 80%;"> 


