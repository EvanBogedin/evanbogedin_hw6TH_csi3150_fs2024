# Table of Content
- [Introduction](#introduction)
- [Features](#features)
- [Structure](#structure)
- [Codebase](#codebase)
  

## Introduction

Demo Quiz App is a tool to help students memorize important information about web development. It was made using JavaScript, HTML, and CSS. Upon starting the quiz, users will be presented with the rules which are as follows.

<div align="center">
  
![{A6750969-4A92-4CF2-AA42-2403AD9F4D79}](https://github.com/user-attachments/assets/8ce425ec-4638-4bbb-bc9e-29a8d0d1d3e1)

</div>

If the user wishes to continue, a multiple-choice question with 4 choices will be presented. After selecting one the correct answer will be highlighted green with a checkmark and if a wrong choice is selected it will be highlighted red with an x. 

<div align="center">
  
![{6107A1CA-0D4B-4CCE-80C3-6DCED6240277}](https://github.com/user-attachments/assets/d3ce4e26-b43e-407a-97fb-7bf9384f907a)

</div>

The quiz consists of a total of five questions. Upon completing the quiz the user will then be presented with a message indicating that the quiz has been completed as well as the number of questions that were answered correctly. The user will also be prompted to choose to either replay the quiz or quit.

<div align="center">
  
![{54A4ABF2-8E4D-4D47-8FC3-959F1EB292FD}](https://github.com/user-attachments/assets/3b47cfb5-0a10-4ea8-b98e-31bcffa586e9)

</div>

## Features

- Runs in browser
- Slick GUI interface
- 5 questions
- The topic is web development
- Score overview
- Replayable

## Structure

QuizApp is organized within a master folder that contains and index.html file as well as 2 subfolders named js and css.
- The css folder contains one style sheet named style.css
- The js folder contains questions.js and quizApp.js

- The index.html serves as the foundation of the app. It has links to the style.css as well as to both the js files. Having both js files linked in the index.html allows for quizApp.js to access variables that are within questions.js
- style.css is used to style every element within the app. even elements that are not yet present but will be added dynamically. Note: style.css imports a font from fontawesome 
- questions.js contains each question in the form of a js object stored in an array labeled questions, which will be accessed by quizApp to dynamically present the user with questions.

The following is an example of one question as a js object.
```js
  {
    numb: 1,
    question: "What does HTML stand for?",
    answer: "Hyper Text Markup Language",
    options: [
      "Hyper Text Preprocessor",
      "Hyper Text Markup Language",
      "Hyper Text Multiple Language",
      "Hyper Tool Multi Language",
  ]
```
- quizApp.js contains all the logic for the app.

quizApp.js contains the following references to the DOM elements from index.html, allowing for dynamic updating of the HTML page. Having a reference to an element allows for the manipulation of the elements' attributes as well as the ability to insert new HTML within the referenced elements' tags.
```js
  const start_btn = document.querySelector(".start_btn button");
  const info_box = document.querySelector(".info_box");
  const exit_btn = info_box.querySelector(".buttons .quit");
  const continue_btn = info_box.querySelector(".buttons .restart");
  const quiz_box = document.querySelector(".quiz_box");
  const result_box = document.querySelector(".result_box");
  const restart_quiz = result_box.querySelector(".buttons .restart");
  const quit_quiz = result_box.querySelector(".buttons .quit");
  const option_list = document.querySelector(".option_list");
  const time_line = document.querySelector("header .time_line");
  const timeText = document.querySelector(".timer .time_left_txt");
  const timeCount = document.querySelector(".timer .timer_sec");
  const next_btn = document.querySelector("footer .next_btn");
  const bottom_ques_counter = document.querySelector("footer .total_que");
```

quizApp.js also initializes listeners for each of the buttons used in the app. An example of one listener being initialized is as follows.

```js
  start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo"); //show info box
});
```

## CodeBase

index.html is used to define the structure of the content used in the app. I would like to note elements that belong to the following classes that are key to the functionality of the app.
- start_btn: Initiates the display of the instructions.
- restart: Initiates the quiz.
- que_text: Here is where the questions will be dynamically inserted.
- option_list: Here is where the options to the questions will be inserted.
- total_que: Here is where the question count will be displayed and updated.
- result_box: This is where the results will be displayed after completion of the quiz.

style.css is used to style the page, the following classes initially have no elements assigned to them. They will have elements assigned to them dynamically by Java script and are used to indicate the correctness of user choices.
- correct: The styling for this class makes everything a shade of green.
- incorrect: The styling for this class makes everything a shade of pink

quizApp.js contains the following variables that control the various quiz operations such as how long the user has to answer a question and the user score as well as que_count to keep track of which question the user is on.

```js
  let timeValue = 15;
  let que_count = 0;
  let que_numb = 1;
  let userScore = 0;
  let counter;
  let counterLine;
  let widthValue = 0;
```
### eventListeners

quizApp.js contains eventlisteners for the following buttons.

start_btn
  - shows info box.

exit_btn:
  - hides info box.

continue_btn
  - Hides info box.
  - Shows quiz box.
  - Calls showQestions function.
  - Calls queCounter function passing a 1 in as a parameter.
  - Calls startTimer function, passing in a 15.
  - Calls startTimerLine function.

restart_quiz
  - Shows quiz box.
  - Hides result box.
  - Resets timeValue, que_count, que_numb, userScore, and widthValue to their initial values.
  - Calls showQuestions function.
  - Calls queCounter function.
  - Calls clearInterval function for both counter and counterLine (stops both timers).
  - Calls starTimer and StartTimerLine functions
  - Changes the text of timeText to "Time Left"
  - Hides the next button

quit_quiz
  - Reloads the current window

next_btn

  If it does not exceed max questions
    
  - Increment the que_count value
  - Increment the que_numb value
  - Calls showQestions function
  - Calls queCounter function
  - Calls clearInterval function for both counter and counterLine (stops both timers).
  - Calls startTimer and startTimerLine functions
  - Changes the timeText to Time Left
  - hide the next button

  Else
  - Calls clearInterval function for both counter and counterLine (stops both timers).
  - Calls showResult function

### Functions

#### quizApp.js contains the following 6 functions; showQuestion(), optionSelected(), showResult(), startTimer(), startTimerLine() and queCounter().

showQuestions(): gets the questions and options from questions.js and creates the necessary HTML code and appends it to the DOM. 
  - Specifically, it stores the HTML required to display the question in a variable called que_tag. note it gets the current question from the questions array using the passed-in index
  - Similarly, it stores the HTML required to display the answer options in a variable called option_list.
  - It then uses the following code to insert the newly created HTML code into the DOM.

```js
  que_text.innerHTML = que_tag; //adding new (child) span tag inside que_tag
  option_list.innerHTML = option_tag; //adding new (child) div tag inside option_tag

```

- Finally, it uses the following code to set onclick attribute to all newly created html elements assigned to the options class. Now when the user clicks on an option it will run optionSelected()

```js
    const option = option_list.querySelectorAll(".option");

  // set onclick attribute to all available options
  for (i = 0; i < option.length; i++) {
    option[i].setAttribute("onclick", "optionSelected(this)");
  }
}
```

optionSelected(): used to handle when the user selects one of the available options.
- It checks if the selected option is the correct answer
- stops the timer.
- If the user choice is correct it increase userScore by 1 and then adds the selected option to the option correct class.
- If the user choice is incorrect it adds the selected option to the incorrect class, it also finds the option with the correct answer and adds it to the option correct class.
- with the options added to the appropriate classes the css specified in style.css will now style the options so they indicate the correctness of the user's choice by highlighting them either green or red.
- Finally, it makes the element of the .next_btn class visible.

showResults() 
- Creates the necessary HTML for the result box.
- hides the info and quiz boxes
- displays the user's score with a corresponding message.
- 3 messages can be displayed, depending on the score of the user.
- The HTML string is stored in a variable named scoreTag
- Finally, the construct HTML string is inserted into a div that is a member of the scoreText class.

- startTimer() 
- Creates a timer
- It inserts the amount of time left into the .timer_sec element.
- It pads the displayed time with a 0 if the time left is less than 9.
- Finally, when the time runs out it prevents the user from selecting an option and turns off the timer.
- Also, when the time runs out it will find the option with the correct answer and add it to the correct option class so that it gets highlighted green and makes the .next_btn element visible.

startTimerLine(): Shows a progress bar to visually indicate how much time has passed. 
- It simply creates a timer
- increments the width of the .time_line element by 1px every second using the following code, which takes the current time and concatenates "px" to the end of it. 
```js
  time_line.style.width = time + "px"; //increasing width of time_line with px by time value
```

- Finally, once the time exceeds 549 it stops the timer.

queCounter(): Constructs the necessary HTML to display the current question number at the bottom left of the quiz box.
- It takes the current question number as an argument
- gets the total number of questions by getting the length of the questions array (which in this case is 5).
- It stores the resulting string of HTML code in a variable named totalQueCountage in the following code.

```js
  let totalQueCounTag =
    "<span><p>" +
    index +
    "</p> of <p>" +
    questions.length +
    "</p> Questions</span>";
```
- Then it inserts the HTML into the .bottom_ques_counter element.























