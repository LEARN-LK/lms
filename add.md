<H1> 01 Adding a Course Category </H1>

`Note: Regular teachers cannot add new courses to Moodle. To do this, you need to be log in as an administrator, course creator, or manager.`

<img width="281" alt="image" src="https://github.com/LEARN-LK/lms/blob/master/img/1.png">

Step – 01
From the Site administration link, click Courses>Manage courses and categories

<img width="500" alt="image" src="https://github.com/LEARN-LK/lms/blob/master/img/02%20course%20add.png">

Step – 02
Assume you have to add categories and courses  following like this

<h5>Higher National Diploma in Management</h5>
	
1. Year 01
   - Semester 01
     - Business Management
     - Economics
   - Semester 02
     - Statistics
     - Mathematics
2. Year 02
   - Semester 03
   - Semester 04

Before you create courses, you must add cources categories (main & sub categories). You should follow the following steps:

- Go to the Courses  > Click Manage courses and categories > Click Create new
- Click on the " Click Create new category " button.
- Enter a name for your category and select a parent category.
- Click on the "Create category" button.
- Repeat steps 3 and 4 until you have created all of your categories.
- Once you have created your categories, you can begin creating courses.
  
<h5>Ex : Main Category "Bachelor Degree Program </h5>
      - Sub Category  Year 01
	- Semester 01
  	- Semester 02

 <img width="500" src=" https://github.com/LEARN-LK/lms/blob/master/img/03%20add%20new%20cate.png">

<h5>Ex : Sub Category "Year 01 > Semester 01 , Semester 02 </h5>

sometimes it might be useful to have a sub-category of a course. For example, you might have a category "Bachelor Degree Program " and wish to have sub-categories  "Year 01" and "Year 02”.

You can make one category a subcategory of another by checking the box to the left of its name and then by selecting from the drop down menu 'Move selected categories to' You can create a new, empty sub-category by clicking the actions icon next to its name in Administration>Site administration>Courses>Manage courses and categories. and selecting 'Create new subcategory.'


 <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/04%20sub%20-%20cat.png">



<h1>02 Adding a Course</h1>
Assume that Year 01 > Semester 01 has two courses (Business Management,Economics). Follow these steps to add courses:

Click the category you want your course to be in (Bachelor Degree Program > Year 01 > Semester 01), then click the "Create course" button. Enter the course settings, then choose either "Save and return" to go back to your course, or "Save and display" to go to the next screen.

 <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/05%20-add%20couser%20-%20sem%2001.png">
 
<h1>03 Add Bulk Course </h1>


Creating courses in bulk on Moodle can save you a lot of time and effort. Here's a step-by-step guide to get you started:

1. Prepare your CSV file:
You'll need a comma-separated values (CSV) file containing course information. You can create this in any spreadsheet program like Excel or Google Sheets.

* Required fields:
   - shortname: Unique identifier for the course (lowercase, no spaces).
   - fullname: The course's full name.
   - category: The category where the course will be listed.
     -  **Locate the Category**
        * Click on the **category name** (e.g., `UOP - BSc in IT` or `Semester 01`).
        * **Check the URL for the Category ID**
        * When you click on a category name, the browser URL will change.
        * It will look like this:
  ```
  https://your-moodle-site.com/course/management.php?categoryid=8
  ```
   - The **`categoryid=8`** at the end of the URL is your **Category ID**.

---


* You can use these IDs in your bulk CSV file if you're assigning roles or enrollments.

  <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/001-bulk-courses.png">

     
* Optional fields:
   - course format: Choose a format like "weeks" or "topics".
   - startdate: Course start date (YYYY-MM-DD format).
   - enddate: Course end date (YYYY-MM-DD format).
   - enrolmentmethod: Course enrollment method (manual, self-enrolment, etc.).
   -  Many other options you can find in the Moodle documentation.
   
2. Access the course upload page:
   - Log in to your Moodle site as an administrator [1].
   - Click on the gear icon in the top right corner to access the Site administration panel.
   -  Go to Courses [2] > Upload courses [3].
   -  <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/123%20-bulk.png">
   
3. Upload your CSV file:

    - Drag and drop your CSV file or click the Choose a file button to select it.
    -  Select the appropriate Import options [4]:
    -  Encoding: Choose the character encoding of your CSV file (usually UTF-8) [6].
    -  Field delimiter: Make sure it's comma (",") [5].
    -  Quote character: Usually double quote ("") or single quote (').
    -  Click Preview [7]to see how Moodle will interpret your CSV data. Review the information carefully and ensure everything looks correct.

     <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/124-bulk.png">
4. (Optional) Use a course template:

If you have a pre-existing course setup with settings you want to apply to all new courses, you can use it as a template.
In the Course process section, enter the shortname of your template course.This will copy all settings and activities from the template course to your newly created courses.

5. Apply default course values:

You can define default values for various settings that will apply to all new courses unless overridden in your CSV file.
Click on Default course values and set your preferred options for enrollment methods, format, start date, etc.

6. Upload your courses:

Once you're happy with everything, click the Upload button.
Moodle will process your CSV file and create new courses based on the provided information.

<h1>04 Deleting a course</h1>

Managers and course creators have the ability to delete courses in Moodle. Course creators can only delete courses they have created within the past 24 hours. This allows users to quickly delete courses created in error without having to contact an administrator.

Step: 
To delete a course as a manager:
Log in to Moodle and go to the Site administration page.
Click on Courses > Manage courses and categories.
Select the category that contains the course you want to delete.
Click on the Delete Icon next to the course name.
Click on the Delete button.
Confirm that you want to delete the course


 <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/06%20-%20delete%2001.png">

<h1>05 -Automated Course Backup</h1>

1. Access Backup Settings:
- Navigate to Site administration > Courses > Backups > Automated backup setup.
  <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/125-backup.png">
2. Enable Automated Backups:
- Set the backup_auto_active option to enabled [4].
3. Choose Backup Frequency:
- Select the days of the week on which you want the backups to run [5].
- Set the execution time for the backup process. Consider choosing a time when server activity is low, such as early morning [6].
   <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/126-backup.png"> 
4. Specify Backup Location:

- Set the "Save to..." path to the desired location for storing backups.
Important: Choose a location that is not on the same drive as your Moodle installation. This ensures that backups are preserved even if the main drive fails.
 <img width="500" src="https://github.com/LEARN-LK/lms/blob/master/img/127-path.png"> 

5. Optional: Use Course Names in Filenames:

- Check the "Use course name in backup filename" box if you prefer backups to be named using course shortnames instead of course IDs.

6. Save Settings:

- Click the "Save changes" button to apply the settings.



