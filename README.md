# Test App 1 — Interactive CLI Quiz

A small interactive Node.js command-line quiz game covering JavaScript, Node.js, and general programming concepts. The application presents multiple-choice questions, provides explanations after each answer, tracks the score, and reviews incorrect responses at the end.

> **Important:** The application lives under `test-app/`. Run all setup, test, and execution commands from that directory.

## Features

- Interactive terminal-based gameplay
- Three quiz categories:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Question-count selection:
  - All available questions
  - Three questions
  - Five questions when available
- Numeric answer selection with input validation
- ANSI-colored terminal output
- Immediate correctness feedback
- Explanations for questions
- Progress and score tracking
- Final score summary
- Incorrect-answer review
- Option to replay the quiz
- Native Node.js ES Modules
- No external runtime or development dependencies

## Prerequisites

- Node.js version 18 or later
- npm, included with Node.js
- An interactive terminal capable of displaying ANSI color codes and Unicode characters

Verify the installed versions:

```bash
node --version
npm --version
```

The project declares its Node.js engine requirement in `test-app/package.json`.

## Installation

Clone the repository and move into the application directory:

```bash
git clone https://github.com/renu-epam/test-app-1.git
cd test-app
```

The application uses only Node.js built-in modules and currently has no external dependencies. Running `npm install` is optional but harmless:

```bash
npm install
```

There is currently no lockfile in the repository.

## Running the App

From the `test-app/` directory, start the quiz with:

```bash
npm start
```

Alternatively, run the entry point directly:

```bash
node index.js
```

The application is an interactive TTY program and should be run in a terminal rather than through a non-interactive input environment.

## Gameplay Flow

When the application starts:

1. A colored welcome banner is displayed.
2. Select one of the available quiz categories:
   - JavaScript Basics
   - Node.js Fundamentals
   - General Programming
3. Select the number of questions:
   - All available questions
   - Three questions
   - Five questions, when the category contains enough questions
4. Read each question and select an answer by entering its numeric option.
5. Receive immediate feedback indicating whether the answer was correct.
6. Review the explanation for the question.
7. Continue until all selected questions have been answered.
8. View the final score and progress summary.
9. Review incorrect answers, when applicable.
10. Choose whether to replay or exit the application.

## npm Scripts

Run these commands from `test-app/`.

| Command | Description |
|---|---|
| `npm start` | Starts the application using `node index.js`. |
| `npm test` | Runs Node.js’s built-in test runner with `node --test`. |

There are currently no test files in the repository, so `npm test` does not provide meaningful automated test coverage at this time.

## Project Structure

```text
test-app/
├── package.json
├── index.js
├── data/
│   └── questions.json
└── src/
    ├── colors.js
    ├── input.js
    └── quiz.js
```

### File and Directory Responsibilities

- `package.json`
  - Defines the package metadata and Node.js engine requirement.
  - Declares the npm scripts.
  - Configures the project as a native ES Module application.

- `index.js`
  - Main application entry point.
  - Creates the `readline` interface.
  - Loads the question data from `data/questions.json`.
  - Displays category and question-count menus.
  - Coordinates the quiz lifecycle and replay behavior.
  - Handles top-level errors and input-session cleanup.

- `src/quiz.js`
  - Defines the `Quiz` class.
  - Manages the current quiz state, selected questions, score, and progress.
  - Shuffles questions using the Fisher-Yates algorithm.
  - Evaluates answers.
  - Stores explanations and incorrect-answer information for the final review.

- `src/input.js`
  - Provides promise-based helpers around the Node.js `readline` interface.
  - Handles prompts and numeric input validation.

- `src/colors.js`
  - Defines ANSI terminal escape sequences.
  - Provides semantic styling used for banners, prompts, feedback, and other output.

- `data/questions.json`
  - Contains the quiz categories and question definitions.
