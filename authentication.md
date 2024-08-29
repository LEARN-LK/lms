<h1> Mirosoft O365  </h1>
To add Microsoft 365 (O365) authentication to Moodle 4.3, you can use OAuth 2 authentication to allow users to log in using their Microsoft accounts. This involves configuring an Azure AD application and setting up Moodle to use it.


### Step 1: Set Up Azure AD Application in Microsoft 365

1. **Access Azure Active Directory:**
   - Go to the [Azure portal](https://portal.azure.com/).
   - Sign in with your Microsoft 365 administrator account.
   - Navigate to `Azure Active Directory` > `App registrations`.
     
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Azure-01.png?raw=true" style="max-width: 100%;width: 100%;"> 

2. **Register a New Application:**
   - Click on `New registration`.
   - Enter a name for your application (e.g., "Moodle O365 Authentication").
   - Choose `Accounts in this organizational directory only` or `Accounts in any organizational directory` depending on your user base.
   - Under `Redirect URI`, select `Web` and enter the following URI:
     ```
     https://yourmoodleurl.com/admin/oauth2callback.php
     ```
     Replace `yourmoodleurl.com` with your actual Moodle site URL.
   - Click `Register`.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-02.png?raw=true" style="max-width: 60%;width: 100%;"> 

3. **Configure API Permissions:**
   - After the app is created, go to `API permissions`.
   - Click on `Add a permission`, select `Microsoft Graph`, and then choose `Delegated permissions`.
   - Add the following permissions:
     - `openid`
     - `profile`
     - `email`
     - `offline_access`
   - Click `Add permissions`.
   - Grant admin consent for your organization.
     
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-03.png?raw=true" style="max-width: 80%;width: 60%;"> 
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-04.png?raw=true" style="max-width: 80%;width: 60%;"> 

4. **Create Client Secret:**
   - Go to `Certificates & secrets`.
   - Click on `New client secret`, provide a description, and set an expiration period.
   - After creating the client secret, copy the value immediately; you will need this for Moodle.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-05.png?raw=true" style="max-width: 80%;width: 60%;"> 


### Step 2: Configure Moodle for O365 Authentication

1. **Login to Moodle as Admin:**
   - Log in to your Moodle site as an administrator.

2. **Enable OAuth 2 Services:**
   - Go to `Site administration` > `Server` > `OAuth 2 services`.
   - Click on `Add a new service`.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m05.1.png?raw=true" style="max-width: 80%;width: 60%;"> 


3. **Add Microsoft as an OAuth 2 Service:**
   - Name the service (e.g., "Microsoft 365").
   - In the `Client ID` field, paste the `Application (client) ID` from Azure AD.
   - In the `Client secret` field, paste the client secret you created in Azure AD.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m06.png?raw=true" style="max-width: 50%;width: 50%;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m07.png?raw=true" style="max-width: 50%;width: 50%;"> 

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

     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m08.png?raw=true" style="max-width: 50%;width: 50%;"> 
     
   - From the list of endpoints copy the OpenID Connect metadata document endpoint URL. It is only necessary to copy the portion up to and including "v2.0". In the example below, the copied URL would be, "https://login.microsoftonline.com/96e0421d-d572-4839-9c32-b8bc00cf250b/v2.0/". Note that it is important to include the trailing slash.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m09.png?raw=true" style="max-width: 50%;width: 50%;"> 
     
- Now return to Moodle and in the newly created OAuth2 Microsoft service, paste the endpoint in the 'Service base URL' field.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m10.png?raw=true" style="max-width: 50%;width: 50%;"> 
  
-  Save your changes.


4. **Enable Microsoft 365 Login:**
   - Go to `Site administration` > `Plugins` > `Authentication` > `Manage authentication`.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m11.png?raw=true" style="max-width: 50%;width: 50%;"> 
     
   - Scroll down to `OAuth 2` and make sure it's enabled.
   - Set `Microsoft 365` as an issuer.
   
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m12.png?raw=true" style="max-width: 50%;width: 50%;"> 
  

### Step 3: Test Microsoft 365 Authentication

1. **Log Out:**
   - Log out of Moodle.

2. **Test the Login:**
   - Go to the Moodle login page.
   - You should now see a "Login with Microsoft" button.

     <img src="https://github.com/LEARN-LK/lms/blob/master/img/azure-m13.png?raw=true" style="max-width: 50%;width: 50%;"> 
     
   - Click on it and log in with a Microsoft 365 account to test.



https://docs.moodle.org/403/en/OAuth_2_Microsoft_service

<h1>Google authentication</h1>

Here is the corrected step-by-step guide:

1. **Login with Google**  
   Go to the Google Cloud Console:  
   [https://console.cloud.google.com](https://console.cloud.google.com)

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-1.png?raw=true" style="max-width: 50%;width: 50%;"> 

2. **Create a New Project or Select an Existing Project**
   **if you select "New Project, add project name and Click Create button"**

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-2.png?raw=true" style="max-width: 50%;width: 50%;"> 

 
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-3.png?raw=true" style="max-width: 50%;width: 50%;"> 
  - Select your newly created project.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-4.png?raw=true" style="max-width: 50%;width: 50%;"> 

4. **Navigate to the API & Services > Credentials section**


<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-5.png?raw=true" style="max-width: 50%;width: 50%;"> 

   - Go to **API & Services** and click on **Credentials**.
     
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-6.png?raw=true" style="max-width: 50%;width: 50%;"> 

6. **Create OAuth 2.0 Client ID**  
   - Click on **Create Credentials** and choose **OAuth client ID**.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-7.png?raw=true" style="max-width: 50%;width: 50%;"> 
     
7. **Configure Consent Screen**
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-8.png?raw=true" style="max-width: 50%;width: 50%;"> 
   
   - Select User Type **External** and click the **Create** button.

       <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-8.1.png?raw=true" style="max-width: 50%;width: 50%;"> 
       
   - Under **Edit app registration > OAuth Consent Screen > App Information**, fill in the required details.
  <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-9.png?raw=true" style="max-width: 50%;width: 50%;"> 
     
   - In the **Authorized domains** section, add the domain of your Moodle site and provide the developer contact information.
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-10.png?raw=true" style="max-width: 50%;width: 50%;"> 
   - Click **Save and Continue**.

9. **Scopes Section**  
   - Click **Save and Continue** in the **Scopes** section.
   - Then, click on the **Back to Dashboard** button.
  
10. **Create OAuth Client ID**  
   - Go to **Credentials** again, then click on **Create Credentials** and choose **OAuth Client ID**.
     
     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-11.png?raw=true" style="max-width: 50%;width: 50%;"> 
     
   - Select **Web Application** as the application type.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-10.1.png?raw=true" style="max-width: 50%;width: 50%;">

11. **Configure Authorized Redirect URLs**  
   - Add the following authorized redirect URL:  
   `https://your-moodle-site.com/admin/oauth2callback.php`

<img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-12.png?raw=true" style="max-width: 50%;width: 50%;"> 

11. **Click Create**  
   - Finally, click the **Create** button to generate your OAuth 2.0 Client ID.

     <img src="https://github.com/LEARN-LK/lms/blob/master/img/Google-13.png?raw=true" style="max-width: 50%;width: 50%;"> 

12 **Configure Moodle for Google Cloud Console Authentication**

i. **Login to Moodle as Admin:**
   - Log in to your Moodle site as an administrator.

ii. **Enable OAuth 2 Services:**
   - Go to `Site administration` > `Server` > `OAuth 2 services`.
   - Click on `Add a new service`.
       

iii . **Add Google as an OAuth 2 Service:**
   - Name the service (e.g., "Google").
   - In the `Client ID` field, paste the `Application (client) ID` from Google Cloud Console.
   - In the `Client secret` field, paste the client secret you created in Google Cloud Console.
 

