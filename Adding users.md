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
<img src="https://github.com/LEARN-LK/lms/assets/143775988/74fdbe11-f679-44d9-85d9-fad5cbe1ab18" alt="image" style="max-width: 100%;width: 500px;">

Clicking the New user button shows the Browse list of users page.

<img src="https://github.com/LEARN-LK/lms/assets/143775988/a9a63750-b18c-4ce7-afc8-e32f0174f7f4" alt="image" style="max-width: 100%;width: 500px;">

<h4>General</h4>
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

<h4> 03 Bulk create accounts via a CSV file </h4>

Follow the these steps :
* Log in to Moodle as an administrator.
* Go to Site administration > Users > Accounts > Upload users.

<img src="https://github.com/LEARN-LK/lms/assets/143775988/2cea11c8-2e94-4429-9392-6874a892ba88" alt="image" style="max-width: 100%;width: 500px;">
  
* Click the Choose a file button and select the CSV file containing your user data.
<img src="https://github.com/LEARN-LK/lms/assets/143775988/0de68ed8-24cd-4e6e-9b99-83232a4b38ca" alt="image" style="max-width: 100%;width: 500px;">

* Click the Upload users button.
* On the Upload user preview page, review the user data and make any necessary changes.
* Click the Process button to upload the users to Moodle.

<h1>Enrolled in Courses</h1>
Now is the time to give users their student, teacher, or other roles. Once users have an account, they need to be enrolled in courses. This can be done through self-enrollment, manual enrollment by an administrator, or through various other methods.

<h2>Manual enrolment</h2>

* Step 1: You can log in to your Moodle site as an administrator by entering your username and password in the login form located at the top right of the page.
* Make sure Manual enrolments has its "eye" opened.
 
  <img src="https://github.com/LEARN-LK/lms/assets/143775988/b3aa7df7-3a1f-4491-9e9a-5b6bd50e6c4f" alt="image" style="max-width: 100%;width: 500px;">
   <img src="https://github.com/LEARN-LK/lms/assets/143775988/c692d534-f0a0-4a73-bc69-a0dad589c3fa" alt="image" style="max-width: 100%;width: 500px;">

* Step 2: Editing manual enrolment settings
Managers and users with the capability "enrol/manual:config" can modify manual enrollment settings for a course, including the default enrollment period and default role. To access these settings, click on the "Enrolment methods" link.

  <img src="https://github.com/LEARN-LK/lms/assets/143775988/011296e3-7463-4b84-81fa-a438759b8145" alt="image" style="max-width: 100%;width: 500px;">
  
Students and teachers can receive notifications about expiring enrollments. To enable these notifications, select either "Enroller only" or "Enroller and enrolled user" from the "Notify before enrolment expires" dropdown menu.Additionally, specify a time in the "Notification threshold" field. This determines how many days in advance the notifications will be sent.

* Step 3 : Access the Course: Navigate to the course where you want to manually enroll users. Click on the course name to enter thecourse

  <img src="https://github.com/LEARN-LK/lms/assets/143775988/a7ef05f7-c1cf-4dc8-8c97-d2f6ce6c45ae" alt="image" style="max-width: 100%;width: 500px;">
 
* step 4 : Enrollment Methods: Once inside the course, click on the "Participants" link in the course administration block
  <img src="https://github.com/LEARN-LK/lms/assets/143775988/0dd2927e-e022-45b8-8534-03ba0d2685a4" alt="image" style="max-width: 100%;width: 500px;">
* step 5 :Enroll Users: In the Participants page,  To manually enroll a user, click on the "Enroll users" button at the top right corner of the page.
* steo 6 : Search for the User: In the "Manual enrolment" section, you will need to find the user you want to enroll. You can search for the user by their name or username.

   <img src="https://github.com/LEARN-LK/lms/assets/143775988/45ecf135-e886-4a03-92e1-59a3c0d3924e" alt="image" style="max-width: 100%;width: 500px;">










