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

## Prerequisites

- Node.js version `18.0.0` or later
- npm, included with Node.js

Verify your installed Node.js version:

```bash
node --version
```

The project does not require any external runtime dependencies.

## Setup Instructions

Clone the repository and navigate to the application directory:

```bash
git clone https://github.com/renu-epam/test-app-1.git
cd test-app-1/test-app
```

No dependency installation is required because the application uses only Node.js built-in modules. If desired, initialize the local npm environment with:

```bash
npm install
```

## How to Run

Start the interactive quiz:

```bash
npm start
```

Alternatively, run the entry point directly:

```bash
node index.js
```

During the quiz:

1. Select a category by entering its displayed number.
2. Select the number of questions.
3. Answer each question by selecting an option.
4. Review your score and incorrect answers.
5. Choose whether to play again.

To exit, select the option to stop playing or terminate the process with `Ctrl+C`.

## Testing

The project defines a test command using Node.js’s built-in test runner:

```bash
npm test
```

Currently, no test files are included in the repository, so the command does not execute application-specific tests.
