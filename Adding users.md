<h1>Adding users </h1>

This is a two-step process, 

* 01 - Authentication
* 02 - Enrolment

<h3>Authentication</h3>
Everyone using your site is required to have an account. You may allow people to create their own account using email-based self-registration, or you may add new users individually, or you may bulk create accounts via a CSV file, or choose from several other authentication methods.

<h4> 01 Email-based self-registration </h4>
1. Go to Site administration > Plugins > Authentication > Manage authentication.
<img src="https://github.com/LEARN-LK/lms/assets/143775988/b2a3ee94-2452-41fb-a84b-dd02b6bceaf3" alt="image" style="max-width: 100%;width: 500px;">

2. Enable the Email-based self-registration plugin.
<img src="https://github.com/LEARN-LK/lms/assets/143775988/b2b11611-7808-40bf-b19f-f3c64f2bd23c" alt="image" style="max-width: 100%;width: 500px;">

3. Under the Manage authentication page in the common settings section, in the Self-registration dropdown, select Email-based self-registration.
<img src="https://github.com/LEARN-LK/lms/assets/143775988/26ab0238-8cc5-4e3e-bd89-beec49568990" alt="image" style="max-width: 100%;width: 500px;">

4. Configure the following settings:

Allowed email domains: Optionally, you can restrict self-registration to specific email domains.
Email confirmation message: This is the email that will be sent to users to confirm their registration.
Resending the confirmation email: This setting allows users to request a new confirmation email if they do not receive the original one.
Support contact: This is the email address that users can contact if they have problems with self-registration.

5. Click the Save changes button.

<b>Now you can enable it in the "Create new account" link on the login page.</b>

<h4> 02 Add New users individually </h4>

Users with the "Create users" capability (such as administrators, managers, and others) can create new user accounts by going to Site administration > Users > Accounts > Add a new user.

<img src="https://github.com/LEARN-LK/lms/assets/143775988/ca499bf6-cf2c-440a-b6b3-d535ae67cc55" alt="image" style="max-width: 100%;width: 500px;">





Clicking the New user button shows the Browse list of users page.


<h5>General</h5>
* Username :
The user will use this name to log in to Moodle. It should be unique and easy to remember. It can only contain lowercase letters, numbers, hyphens, underscores, periods, or at symbols.

* Authentication method :
This setting determines how Moodle will verify the user's password. There are two options:

* Manual accounts: Accounts created by an administrator.
Email-based self-registration: Accounts created by the user themselves.

* Suspended account
Suspended users cannot log in to Moodle.

* Generate password and notify user
If you select this option, Moodle will generate a temporary password for the user and email them instructions on how to log in and change it.









