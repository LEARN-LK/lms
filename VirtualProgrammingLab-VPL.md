## Virtual Programming Lab - VPL

Here are the steps to download, install, and configure Virtual Programming Lab (VPL) for Moodle, and how to set up a simple "Hello World" assignment for students.

### 1. Download and Install VPL Plugin for Moodle

#### Step 1: Download VPL Plugin
1. Go to the [Moodle plugins directory](https://moodle.org/plugins/mod_vpl).
2. Download the latest version of the **Virtual Programming Lab (VPL)** plugin for your Moodle version.

#### Step 2: Install VPL on Moodle
1. Log in to your Moodle site as an administrator.
2. Navigate to `Site administration > Plugins > Install plugins`.
3. Upload the VPL plugin file you downloaded (ZIP file) and click **Install plugin from the ZIP file**.
4. Follow the prompts to complete the installation.

#### Step 3: Configure VPL
1. After installation, navigate to `Site administration > Plugins > Activity modules > VPL`.
2. Configure the VPL execution server (optional, but needed for actual code execution). If you want to run the VPL server:
   - Install the VPL server on a separate machine or the same server. Detailed instructions can be found [here](https://vpl.dis.ulpgc.es).
   - Configure the execution server in Moodle using the server’s IP address and port.

### 2. Create a Simple VPL Assignment (Print "Hello World")

#### Step 1: Create a New VPL Activity
1. Go to your Moodle course and **Turn editing on**.
2. In the section where you want the assignment to appear, click **Add an activity or resource**.
3. Select **Virtual Programming Lab (VPL)** from the activity list.

#### Step 2: Configure the VPL Activity
1. **Name** the activity (e.g., "Hello World Program").
2. In the **Description**, provide instructions like: 
   - "Write a program that prints 'Hello World' on the screen."
3. Under the **Submission restrictions**:
   - Set the programming language (e.g., Python, Java, C++).
4. Under **Grade**:
   - Choose the grading method and maximum grade.

#### Step 3: Configure Execution Settings
1. Go to the **Execution options** tab and configure:
   - Enable **Run** to allow students to run their programs.
   - Enable **Evaluation** if you want automatic grading based on test cases.
   
2. For automatic grading, go to **Execution files** and add a test case:
   - Create a file like `vpl_evaluate.cases` for Python or other languages and input a simple case to check for "Hello World" output.
   - Example for Python:
     ```
     output == "Hello World\n"
     ```

3. Save the activity.

### 3. Adding a VPL Question for Teachers

#### Step 1: Access the VPL Assignment
1. As a teacher, log in and navigate to the course.
2. Select the VPL activity you've created (e.g., "Hello World Program").

#### Step 2: Add VPL Question (Simple Task)
1. Inside the VPL activity, click **Edit**.
2. You can add a test case in the **Execution files** section by selecting **Create a new file**. 
   - Name the file `vpl_evaluate.cases`.
   - Inside the file, write the evaluation criteria. For example:
     ```bash
     output == "Hello World\n"
     ```
3. Click **Save** and return to the assignment.

### Example Student Assignment:
- **Task**: Write a program in Python that outputs the text "Hello World".
- **Submission Instructions**: Students will write and submit the program using the VPL interface.

This setup will allow you to automatically grade the assignment when students submit their programs.

Would you like to test a different type of question, or is this enough for the assignment?
