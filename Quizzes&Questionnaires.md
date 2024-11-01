<h1>What is the Quiz activity</h1>

The Quiz activity in Moodle 4.0 is a tool that allows teachers to create and deliver assessments to their students. It supports a wide variety of question types, including multiple choice, true/false, fill-in-the-blank, and essay questions. Teachers can also add images, videos, and audio clips to their questions.

Quizzes can be graded automatically or manually. For automatically graded quizzes, the system will automatically assign students a score based on their answers. For manually graded quizzes, teachers will need to review student responses and assign scores manually.Students can take quizzes multiple times, and teachers can control how many attempts students are allowed and whether students can see their scores after each attempt.

<h3>Here are some of the new features in the Quiz activity in Moodle :</h3>

* New question types: Moodle 4.0 includes several new question types, such as drag-and-drop questions, matching questions, and hotspot questions.
* Improved grading: Moodle 4.0 includes a number of improvements to the grading process, such as the ability to give partial credit for answers and the ability to provide feedback to students on their answers.
*  Such as the ability to generate more detailed reports on student performance and the ability to export reports to different formats.

<h2> 01 - How is it set up</h2>

* Open the Moodle course where you want to add the quiz.
* Turn editing on.
* Click the Add an activity or resource button.
* Select Quiz from the list of activities.
* Click the Add button.
* Enter a name and description for the quiz.
* Configure the quiz settings, such as the time limit, number of attempts, and grading method.
* Click Save and Display button.
 <img src="https://github.com/LEARN-LK/lms/blob/master/img/31-%20Quiz.png"  style="max-width: 100%;width: 600px;">
* Click add Quastion button
<img src="https://github.com/LEARN-LK/lms/blob/master/img/32-add%20Quiz.png" style="max-width: 100%;width: 600px;">

* Click Add and then click '+ a new question' (If you already made questions in the question bank, then click '+ from question bank' or if you wish to add a question randomly picked from a category of questions, click '+ a random question'.)"
<img src="https://github.com/LEARN-LK/lms/blob/master/img/33-add%20new%20quastion.png" style="max-width: 100%;width: 600px;">

<h4>To add questions to your quiz:</h4>

* Choose the type of question you want to add.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/34-quastion%20type.png"  style="max-width: 100%;width: 600px;">
  
* Click Add at the bottom.
* Add your question. For help, see the documentation on question types.
* Click Save changes.
* Repeat steps 1-4 for as many questions as you need.
* When you are finished, click Save changes again.

<!-- <h2>02 - Embed answers - Question type(Short answer questions, Numerical questions, Multi-response answers). </h2>

In Moodle, questions can be structured with a passage of text that incorporates embedded answers. These embedded answers may include a variety of response formats, such as multiple-choice, short answers, and numerical answers. This approach allows for a more dynamic and interactive assessment experience, enabling learners to engage with the content in a comprehensive manner.
in this section cover following 
1. :MC: for multiple choice questions
2. :MR: for multi response questions
3. :SA: for short answer questions
4. :NM: for numerical questions

<h3> To add MC: /MR: /SA:/ NM: you should follow below step </h3>

Step: Follow the steps shown in the image.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/34-quastion%20type.png"  style="max-width: 100%;width: 600px;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/135-Embeded.jpg" style="max-width:100%;width: 60%;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/121-emb.png" style="max-width:100%;width: 60%;">

Preview 

<img src="https://github.com/LEARN-LK/lms/blob/master/img/122-em.png?raw=true" style="max-width:100%;width: 60%;">


<h3>Example</h3>
<h4>1 - Adding :MC: for multiple choice questions:</h4>

Match the following cities with the correct state:`
<pre><code>
* `San Francisco: {1:MULTICHOICE:=California#OK~Arizona#Wrong}`
* `Tucson: {1:MULTICHOICE:California#Wrong~%100%Arizona#OK}`
* `Los Angeles: {1:MULTICHOICE:=California#OK~Arizona#Wrong}`
* `Phoenix: {1:MULTICHOICE:%0%California#Wrong~=Arizona#OK}`
</code></pre>

<h4>2 - Adding :MR: for multi response questions</h4>
<p>Which of the following statements about IP addressing are correct? (Select all that apply)</p>

<pre><code> `{1:MR:%34%An IPv4 address is 32 bits long~%-50%In IPv6, addresses are represented as 32 hexadecimal digits~%34%Subnetting is a technique used to divide an IP network into smaller, more manageable sub-networks~%-50%The loopback address in IPv4 is 127.0.0.1~%34%DHCP is used to assign static IP addresses to devices on a network.}` </pre></code>

<h4>3 - SA: for short answer questions</h4>
<pre><code> `Moodle is the {:SA:=best~<span>=</span>leading}` LMS.</pre></code>

<h4>4 - NM: for numerical questions</h4>
<pre><code> `Calculate: 10 x 5 = {1:NM:=50}` </code></pre>

<h2> 03 - Quiz Student View</h2>
Quiz view:

* The quiz will open in a fullscreen popup window.
* At the top of the quiz window, you will see the following information:
     > The quiz name and description
     > The number of questions in the quiz.
     > The time limit for the quiz,
     > if any.The number of attempts you have remaining.Below the quiz information,
* when clicking "attemp quiz" Button [1]. you will see the first question in the quiz .
* To answer a question, select the answer choice that you think is correct.
* To move to the next question, click on the Next button [2].
* To review a previous question, click on the Previous button.
* To flag a question, click on the Flag button. This will mark the question for your review and alert your teacher to a possible query.
To complete the quiz:
* Once you have answered all of the questions in the quiz, click on the Finish attempt button [3].
* You will be asked to review your answers and then click on the Submit all and finish button to submit your quiz.

<h2>04 - Quiz results:</h2>
* After you have submitted your quiz, you will see your quiz results.
* Your results will show you your score for the quiz, as well as the correct answers to each question [4].

<img src="https://github.com/LEARN-LK/lms/blob/master/img/39-all%20-student%20view.png?raw=true" style="max-width:100%;width: 60%;">

<h3>Quiz Teacher View</h3>
To review quiz attempts:

* On the quiz page, click on the Preiews Button.
* This will show you a list of all the quiz reviews that have been created by teachers.
* Grades can be viewed either by clicking the quiz and the link 'Attempts' when students have attempted the quiz, or from the Actions menu top right > Results (as in the above screenshot)

<img src="https://github.com/LEARN-LK/lms/raw/master/img/40-teacher%20preview.png?raw=true" style="max-width: 100%;width: 60%;">   -->



