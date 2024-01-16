<h1>Adding users </h1>

This is a two-step process, 

* 01 - Authentication
* 02 - Enrolment

<h3>Authentication</h3>
Everyone using your site is required to have an account. You may allow people to create their own account using email-based self-registration, or you may add new users individually,or you may create bulk  accounts via a CSV file, or choose from several other authentication methods.

<h4> 01 Email-based self-registration </h4>
1. Go to Site administration > Plugins > Authentication > Manage authentication.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/08%20-email-based%20self-registration.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">

2. Enable the Email-based self-registration plugin.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/10-%20enable.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">

3. Under the Manage authentication page in the common settings section, in the Self-registration dropdown, select Email-based self-registration.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/11%20enable%20sett.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">


4. Configure the following settings:

* Allowed email domains: Optionally, you can restrict self-registration to specific email domains.
* Email confirmation message: This is the email that will be sent to users to confirm their registration.
* Resending the confirmation email: This setting allows users to request a new confirmation email if they do not receive the original one.
* Support contact: This is the email address that users can contact if they have problems with self-registration.

5. Click the Save changes button.

<b>Now you can enable it in the "Create new account" link on the login page.</b>

<h4> 02 Add New users individually </h4>

Users with the "Create users" capability (such as administrators, managers, and others) can create new user accounts by going to Site administration > Users > Accounts > Add a new user.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/12%20add%20user.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/13manualreg.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">


Clicking the New user button shows the Browse list of users page.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/14%20users.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">


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

<h4> 03 Create bulk  accounts via a CSV file </h4>

Follow the these steps :
* Log in to Moodle as an administrator.
* Go to Site administration > Users > Accounts > Upload users.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/15%20bulk.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">

* Click the Choose a file button and select the CSV file containing your user data.
<img src="https://github.com/LEARN-LK/lms/blob/master/img/16-nCVS.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">


* Click the Upload users button.
* On the Upload user preview page, review the user data and make any necessary changes.
* Click the Process button to upload the users to Moodle.

<h1>Enrolled in Courses</h1>
Now is the time to give users their student, teacher, or other roles. Once users have an account, they need to be enrolled in courses. This can be done through self-enrollment, manual enrollment by an administrator, or through various other methods.

<h2> 01 - Manual enrolment</h2>

* Step 1: You can log in to your Moodle site as an administrator by entering your username and password in the login form located at the top right of the page.
* Make sure Manual enrolments has its "eye" opened.
 
  <img src="https://github.com/LEARN-LK/lms/blob/master/img/16%20-user%20enroll.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">
   <img src="https://github.com/LEARN-LK/lms/blob/master/img/17-%20plugin%20enable.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">

* Step 2: Editing manual enrolment settings
Managers and users with the capability "enrol/manual:config" can modify manual enrollment settings for a course, including the default enrollment period and default role. To access these settings, click on the "Enrolment methods" link.

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/17-Manual%20enrolments.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">
  
Students and teachers can receive notifications about expiring enrollments. To enable these notifications, select either "Enroller only" or "Enroller and enrolled user" from the "Notify before enrolment expires" dropdown menu.Additionally, specify a time in the "Notification threshold" field. This determines how many days in advance the notifications will be sent.

* Step 3 : Access the Course: Navigate to the course where you want to manually enroll users. Click on the course name to enter thecourse

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/19%20My%20courses%20.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">

 
* step 4 : Enrollment Methods: Once inside the course, click on the "Participants" link in the course administration block
  <img src="https://github.com/LEARN-LK/lms/blob/master/img/20-participants.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">
 
* step 5 :Enroll Users: In the Participants page,  To manually enroll a user, click on the "Enroll users" button at the top right corner of the page.
* steo 6 : Search for the User: In the "Manual enrolment" section, you will need to find the user you want to enroll. You can search for the user by their name or username.

   <img src="https://github.com/LEARN-LK/lms/blob/master/img/21-popup.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">
  
<h2>02 - Self-enrolment</h2>
Self-enrolment empowers users to register themselves in courses. They can do so instantly by clicking "Enroll me in this course" or by entering a provided enrollment key. For this feature to work, the site administrator must enable the enrollment plugin in the Enrolment plugins section, and enable it within the respective course. Additionally, the manual enrollment plugin must be enabled within the same course.

* step :1  In your course, click the Participants link from Course navigation
* step :2  From the dropdown select click Enrolment methods
* step :3  Open the "eye" icon next to the Self enrolment method:
  
  <img src="https://github.com/LEARN-LK/lms/blob/master/img/22-Self%20enrolment%20(Student).png?raw=true" alt="image" style="max-width: 100%;width: 500px;">

<b>Note</b> : When you log in to Moodle as a student, you'll see an "Enroll me" button next to courses you can join

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/23%20selt-enrolment.png?raw=true" alt="image" style="max-width: 100%;width: 500px;">











