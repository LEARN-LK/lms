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

3. **Add Microsoft as an OAuth 2 Service:**
   - Name the service (e.g., "Microsoft 365").
   - In the `Client ID` field, paste the `Application (client) ID` from Azure AD.
   - In the `Client secret` field, paste the client secret you created in Azure AD.
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
   - Click `Save changes`.

4. **Enable Microsoft 365 Login:**
   - Go to `Site administration` > `Plugins` > `Authentication` > `Manage authentication`.
   - Scroll down to `OAuth 2` and make sure it's enabled.
   - Set `Microsoft 365` as an issuer.

### Step 3: Test Microsoft 365 Authentication

1. **Log Out:**
   - Log out of Moodle.

2. **Test the Login:**
   - Go to the Moodle login page.
   - You should now see a "Login with Microsoft" button.
   - Click on it and log in with a Microsoft 365 account to test.

### Step 4: Adjust Permissions and Settings (Optional)

- Return to the Azure portal if you need to adjust application settings or permissions.
- In Moodle, you can configure additional settings for the OAuth 2 service under `OAuth 2 services`.

This setup allows users to authenticate with Microsoft 365 when logging into your Moodle 4.3 site.

https://docs.moodle.org/403/en/OAuth_2_Microsoft_service
