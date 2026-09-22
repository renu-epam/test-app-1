# Quiz CLI

An interactive programming quiz command-line application built with Node.js and ES Modules. The application allows users to select a quiz category, choose the number of questions, answer questions interactively, and review their final score with explanations for incorrect answers.

## Key Features

- Interactive terminal-based quiz experience
- Three quiz categories:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Select between all available questions, three questions, or five questions when applicable
- Randomized question order using the Fisher–Yates shuffle algorithm
- Progress bar displayed during the quiz
- Immediate correct or incorrect answer feedback
- Optional explanations for answers
- Final score, percentage, and performance message
- Review of incorrect answers
- Replay option after completing a quiz
- ANSI terminal colors implemented without external dependencies
- Promise-based input handling with Node.js `readline`
- Uses Node.js built-in modules only
