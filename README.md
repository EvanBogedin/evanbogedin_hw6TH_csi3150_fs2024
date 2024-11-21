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

Within the master folder is the index.html with the CSS and JS files separated into their two respective folders named css and js. The css folder contains one style sheet; style.css and the js folder contains 2 js files; questions.js and quizApp.js. index.html serves as the foundation of the app and has the css as well as both questions.js and quizApp linked to it. 

- style.css is used to style every element within the app.
- questions.js contains each question in the form of a js object stored in an array labeled questions.The following is an example of one question as a js object.
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

quizApp.js contains the following references to the DOM elements from index.html.
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

quizApp.js also initializes listeners for each of the buttons used in the app. An example of one listener is as follows.

```js
  start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo"); //show info box
});
```

quizApp.js contains the following variables that control quiz operations such as how long the user has to answer a question and the user score.

```js
  let timeValue = 15;
  let que_count = 0;
  let que_numb = 1;
  let userScore = 0;
  let counter;
  let counterLine;
  let widthValue = 0;
```

quizApp.js contains the following 6 functions; showQuestion(), optionSelected(), showResult(), startTimer(), startTimerLine() and queCounter.
