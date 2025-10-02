<h1> Moodle as a Service  </h1>

<h3>Moodle - Open Source Learning Platform</h3> 
 
Moodle is a free and open-source learning management system (LMS) that allows educators to create and deliver online courses. It is a popular choice for schools, universities, and businesses because it is easy to use and customize.

Moodle provides a variety of tools for creating and managing courses, including a course editor, lesson editor, and quiz editor. It also includes a variety of activity modules that can be used to create engaging and interactive learning experiences, such as assignments, quizzes, forums, and wikis.

Moodle is a highly customisable LMS, and there are a variety of plugins and themes available to extend its functionality. It is also relatively easy to learn and use, making it a good choice for organisations of all sizes.

<h4>Here are some of the benefits of using Moodle:</h4>

- Free and open-source, so you can use it without paying any licensing fees.
- Highly customisable, you can tailor it to meet the specific needs of your organization.
- Easy to use and learn, even for users with no prior experience with LMSs.
- Supported by a large and active community of users and developers.
- You can effortlessly localize your Moodle site as the software has been translated into over 95 languages.
- It is a flexible program that supports both 100% online courses and blended learning.
- Moodle constantly updates its security controls to ensure your data is protected from loss, misuse, and unauthorized access.
- It offers cross-browser compatibility and a default mobile-compatible interface.

<h2> In this guide, we will cover the following areas </h2>

 `Note : This guide was prepared for Moodle version  Moodle 4.0.11+ (Build: 20240104).` 

 <!-- > [!NOTE]This content will not appear in the rendered Markdown  -->
 
<h4>   Moodle Admin Guide </h4>

* [Site Admin](/site-admin/)
   * [Site Admin](https://github.com/LEARN-LK/lms/blob/master/site-admin.md)
<!--   * Moodle installation
     - [Linux](https://github.com/LEARN-LK/lms/blob/master/moodle-install.md)
     - [Alpine Linux](https://github.com/LEARN-LK/lms/blob/master/Alpine-linux.md) -->
   * [Practice Moodle in VirtualBox / UTM](https://github.com/LEARN-LK/lms/blob/master/Practice-Moodle-VirtualBox&UTM.md)
   * [Change Moodle Language Pack](https://github.com/LEARN-LK/lms/blob/master/mdl-language-pack.md)
   * [Customize the Moodle themes](https://github.com/LEARN-LK/lms/blob/master/Customize_Moodle_themes.md)
   * [Configuring Email Outgoing](https://github.com/LEARN-LK/lms/blob/master/Configuring-Email-Outgoing.md)
   * <h4>  External Authentication </h4>
   * [LIAF SSO - Auth SAML2](https://github.com/LEARN-LK/lms/blob/master/Learn-SSO.md)
 <!--  * [LIAF SSO - Shiboleth SP](https://github.com/LEARN-LK/lms/blob/master/shiboleth.md)
   * [O365 Authentication](https://github.com/LEARN-LK/lms/blob/master/authentication.md#-mirosoft-o365--)
   * [Google Authentication](https://github.com/LEARN-LK/lms/blob/master/authentication.md#google-authentication) -->
   * <h4>Plugin Installation</h4>

  **Note** If you are facing limitations with upload_max_filesize and post_max_size, please run the following commands in your virtual machine terminal:

```  sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 128M/g' /etc/php82/php.ini```

```  sed -i 's/post_max_size = 8M/post_max_size = 128M/g' /etc/php82/php.ini```

   * [Interactive content](https://github.com/LEARN-LK/lms/blob/master/Install-H5P-plugin.md)
   * [Virtual Programming Lab - VPL](https://github.com/LEARN-LK/lms/blob/master/installVPL.md)
   * [Board](https://github.com/LEARN-LK/lms/blob/master/install-boad.md) 
   * [Workplace Course Certificate](https://github.com/LEARN-LK/lms/blob/master/Workplace-Certificate.md)
   * [Checklist](https://github.com/LEARN-LK/lms/blob/master/Checklist-pluging.md)
   * [Completion Progress](https://github.com/LEARN-LK/lms/blob/master/Progress-plugin.md)
   * [Attendance Activity Plugin](https://github.com/LEARN-LK/lms/blob/master/attendance-plugin.md)
   * [Mass Enrolments](https://github.com/LEARN-LK/lms/blob/master/Mass-enrolments.md)


    
```Note: Enabling Default Moodle Plugins (e.g., “Survey”)If a default plugin (like Survey) is not visible in the “Add an activity or resource” list for teachers, the Moodle administrator should:Navigate to:-Site administration → Plugins → Activity modules → Manage activities```
     

<h4> 02. Moodle Manager/ Faculty Coordinator Guide </h4>

  * [Manager / Faculty Coordinator](https://github.com/LEARN-LK/lms/blob/master/manager.md)
  * Add users [Adding User methods,Enrolling](https://github.com/LEARN-LK/lms/blob/master/Adding%20users.md#adding-users-)
  * Create courses [(Create category,Create courses ,Add bulk course,Delete courses,Automated course backup)](https://github.com/LEARN-LK/lms/blob/master/add.md#-adding-a-course-category-)



<h4> 03. Teachers Guide</h4>

   * [Adding contents/Assignments](https://github.com/LEARN-LK/lms/blob/master/Assignment-activity.md)
   * [Quizzes, Questionnaires](https://github.com/LEARN-LK/lms/blob/master/Quizzes&Questionnaires.md)
   * [Moodle Virtual Class Room (Webinar)](https://github.com/LEARN-LK/lms/blob/master/Moodle%20Virtual%20Class%20Room%20(Webinar)%20.md)
   * [Interactive content](https://github.com/LEARN-LK/lms/blob/master/Interactive-content.md)
   * [Creating and Managing forums](https://github.com/LEARN-LK/lms/blob/master/Forum%20activity.md)
     <!--* [Scheduling activities](https://github.com/LEARN-LK/lms/blob/master/Scheduling-activities.md)-->
   * [Enable Safe Exam Browser](https://github.com/LEARN-LK/lms/blob/master/Enable-Safe-Exam-Browser.md)
   * [SCORM](https://github.com/LEARN-LK/lms/blob/master/SCORM.md)
   * [Feedback](https://github.com/LEARN-LK/lms/blob/master/Feedback.md)
   * [Surveys](https://github.com/LEARN-LK/lms/blob/master/Survey-activity.md)
   * [Attendance/Reports](https://github.com/LEARN-LK/lms/blob/master/Attendance-activity.md)
   * [Grading](https://github.com/LEARN-LK/lms/blob/master/Grading.md)
   * [Virtual Programming Lab - VPL](https://github.com/LEARN-LK/lms/blob/master/VirtualProgrammingLab-VPL.md)
   * [Board - Plugin](https://github.com/LEARN-LK/lms/blob/master/mdl-board.md)
   * [Workplace Course Certificate](https://github.com/LEARN-LK/lms/blob/master/course-certificate.md)
   * [Checklist - Plugin](https://github.com/LEARN-LK/lms/blob/master/Checklist.md)
   * [Completion Progress - plugin](https://github.com/LEARN-LK/lms/blob/master/completion-progress.md)
   * [Bulk Enrolments plugin](https://github.com/LEARN-LK/lms/blob/master/bulk_enrolments.md)
     
<h4> 04. Student Guide</h4>

   <!--[Students Guide](https://github.com/LEARN-LK/lms/blob/master/Student-Guide.md)-->
   * [Getting Started](https://github.com/LEARN-LK/lms/blob/master/getting-started.md)
   * [Navigating Courses,Submit the Assignment,Quiz Submission](https://github.com/LEARN-LK/lms/blob/master/Courses-Assignment-Quiz-Submission.md)
   * [Submit the Forum](https://github.com/LEARN-LK/lms/blob/master/Submit-Forum.md)
   * [feedback activity,Survey Submission](https://github.com/LEARN-LK/lms/blob/master/feedback-Survey-Submission.md)
   * [Join in VCR Class Room](https://github.com/LEARN-LK/lms/blob/master/Join-VCR.md)
   * [Safe Exam Browser](https://github.com/LEARN-LK/lms/blob/master/Safe-Exam-Browser.md)
