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



### 2. Prepare the Assignment Question
The assignment question will be the same for both Python and C++:

**Assignment**:  
Write a program that calculates the sum of the following numbers: **123 + 234 + 43352** and prints the result.

**Expected Output**:  
43709

### 3. Steps to Add the Question in Moodle VPL for Python and C++

#### Step 1: Create a New VPL Activity
1. **Log in** to your Moodle site as a teacher.
2. Go to the course where you want to add the assignment and **Turn editing on**.
3. In the section where you want to place the assignment, click **Add an activity or resource**.
4. From the list, select **Virtual Programming Lab (VPL)**.

#### Step 2: Configure the Assignment
1. **Name** the activity (e.g., "Sum Calculation in Python and C++").
2. In the **Description** field, provide instructions like:
   - **Description for Python**: "Write a Python program that calculates the sum of 123, 234, and 43352, and prints the result."
   - **Description for C++**: "Write a C++ program that calculates the sum of 123, 234, and 43352, and prints the result."

3. Under the **Submission restrictions** section, select both Python and C++ as allowed programming languages.

4. In the **Grade** section, set up your grading method and assign the maximum grade.

#### Step 3: Configure VPL Execution Files (for Python and C++)
To ensure that students' code is evaluated, you will add an evaluation file.

1. In the **Execution options** tab:
   - Enable **Run** to allow students to run their programs.
   - Enable **Evaluation** if you want the assignment to be automatically graded.

2. In the **Execution files** tab:
   - Click **Create a new file** and name it `vpl_evaluate.cases`.

3. Add the following content to `vpl_evaluate.cases` to check if the output is correct:

   For **Python**:
   ```bash
   output == "43709\n"
   ```

   For **C++**:
   ```bash
   output == "43709\n"
   ```

4. Save the `vpl_evaluate.cases` file and the overall assignment.

#### Step 4: Add Sample Code (Optional)
You can also provide students with a sample template for Python and C++ to help them get started.

- For **Python**:
  ```python
  # Python program to calculate sum of 123 + 234 + 43352
  result = 123 + 234 + 43352
  print(result)
  ```

- For **C++**:
  ```cpp
  // C++ program to calculate sum of 123 + 234 + 43352
  #include <iostream>
  using namespace std;

  int main() {
      int result = 123 + 234 + 43352;
      cout << result << endl;
      return 0;
  }
  ```

You can add these snippets in the **Instructions** or as a **Preloaded code** in the VPL interface if you want to guide students.

#### Step 5: Finalize and Test
1. Save and return to the course.
2. Test the activity by submitting the code as a student to ensure that both the Python and C++ code are evaluated correctly and produce the expected output.

### Summary:
- **Assignment**: Calculate the total of 123 + 234 + 43352.
- **Languages**: Python and C++.
- **Steps**: Add the VPL activity, configure execution options, add evaluation cases, and optionally provide sample code.

Let me know if you need any further customizations or additional test cases!
