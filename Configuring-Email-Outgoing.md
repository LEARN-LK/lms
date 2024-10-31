### Configuring Email Outgoing

To configure outgoing email in Moodle, follow these steps:

### 1. **Access Outgoing Mail Configuration**
   - Log in to Moodle as an administrator.
   - Go to **Site administration > Server > Email > Outgoing mail configuration**.

### 2. **Configure SMTP Settings**
   - **SMTP hosts**: Enter the SMTP server address. For example, for Gmail, it’s `smtp.gmail.com`. For others, use the SMTP details provided by your email service.
   - **SMTP security**: Choose **TLS** or **SSL** if required by your SMTP server (e.g., Gmail requires TLS/SSL).
   - **SMTP port**: Enter the SMTP port number (e.g., **587** for TLS or **465** for SSL).
   - **SMTP username**: Enter the email address you are using to send mail.
   - **SMTP password**: Enter the password for the SMTP email account.

### 3. **Set No-Reply Email Address**
   - **No-reply address**: Enter a no-reply address like `noreply@yourdomain.com`. This address appears as the sender for automated emails where replies are not needed.

### 4. **Additional Settings (Optional)**
   - **SMTP session limit**: Set the number of messages that can be sent per SMTP session (leave blank for default).
   - **Character set**: Use UTF-8 (default for Moodle), but can be changed if required by your email provider.

### 5. **Save Changes**

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/email-configuration.png?raw=true" style="max-width: 100%;width: 60%;">


   - Click **Save changes** to apply your settings.

### 6. **Test Outgoing Email**
   - Scroll to the **Test outgoing mail configuration** section at the bottom of the page.
   - Enter an email address to send a test message and click **Send a test message**.
   - Check the inbox of the test email to confirm the email was received.

After completing these steps, Moodle should be able to send emails for notifications, password resets, and other communications.
