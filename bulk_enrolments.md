<h2>Bulk Enrolments plugin</h2>

Bulk enrolments allows you to enrol students and add them to groups in a Moodle course using an excel file containing the students' email address or userid. Before you start, you will require an excel file containing a complete list of the students' email address or userids in the first column. Subsequent columns contain the names of any groups you want to add each student to.

<h4>Create your CSV</h4>

In order to upload your students successfully, you will need to create a CSV file with the students details. CSVs are simple to create - one way is in a spreadsheet package, making sure to save it as a .csv file type. At minimum, your CSV file should contain one column for the main student identifier, usually their email address but it can also be their userid, or student ID number. Ensure you have column labels - this is because Moodle anticipates these and so ignores the first row of CSV file. In other words, don't put any actual student data in your file's top row. If you are using email then put 'email', if you are using user IDs then put 'userid'. If you want to enrol the students into Groups, include a second column which gives the group name for each student. Be careful to type these exactly. Give it a column heading 'group'. You can add subsequent groups in subsequent columns.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/bulk/bulk_upload_csv.webp" style="max-width: 100%;width: 50%;">

<h4>Create your CSV using google forms (Alternative method)</h4>

Step 1: Create a google form to get the usernames
Step 2: View the responses from 'Responses' menu
<img src="https://github.com/LEARN-LK/lms/blob/master/img/regform.png" style="max-width: 100%;width: 80%;">

<h4>Enrol the Students</h4>

In the Settings block on your course, under Course administration, click Users > Bulk enrolments.

Select Choose a file and upload your CSV file. Make sure Role to assign is left as student. 
Set First column contains to reflect they type of data you have used in your spreadsheet, either the students' email address, userid or ID number. If you need to create groups, ensure Create group(s) if needed is set to Yes. If you would like to create groupings in your course, based on the groups that the students will been placed into, ensure Create grouping(s) if needed is kept to yes. If you do not want to create groupings, set this to No. To receive an email report confirming which students have been enrolled and which groups they have been placed into, keep Send me a mail report set to Yes. Click Enrol them to my course. Check the students have been enrolled in their groups by going to the Settings menu and under Course Administration click on Users then Groups. You should see the groups listed, followed by the number of students in each group in brackets. You can also bulk unenrol students from your course by clicking on Bulk unenrolments in the block, and following the instructions above.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/p-2-Completion Progress-01.png" style="max-width: 100%;width: 80%;">
