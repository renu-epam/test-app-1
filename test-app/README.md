# Quiz CLI

An interactive command-line quiz game for learning JavaScript, Node.js, and general programming concepts.

## Table of contents

- [Overview](#overview)
- [Features](#features)
- [Technology stack](#technology-stack)
- [How it works](#how-it-works)
- [Prerequisites](#prerequisites)
- [Installation and setup](#installation-and-setup)
- [Configuration and question data](#configuration-and-question-data)
- [Running the application](#running-the-application)
- [Usage](#usage)
- [Build and distribution](#build-and-distribution)
- [Testing](#testing)
- [Project structure](#project-structure)
- [Development](#development)
- [Troubleshooting](#troubleshooting)
- [License](#license)

## Overview

Quiz CLI is a dependency-free Node.js terminal application. It loads quiz categories and questions from a local JSON file, lets the player choose a category and question count, presents multiple-choice questions, and displays a score with explanations and a review of incorrect answers.

## Features

- Interactive terminal menus for category and question-count selection.
- Three included categories: JavaScript Basics, Node.js Fundamentals, and General Programming.
- Multiple-choice questions with immediate correctness feedback and explanations.
- Fisher–Yates shuffling of questions for each quiz.
- Progress bar and question counter.
- Score percentage and performance message at the end of a quiz.
- Review of incorrect answers.
- Option to play again.
- ANSI-colored terminal output implemented without external packages.

## Technology stack

- Node.js with ES modules.
- Node.js built-in `readline` module for input.
- Node.js built-in `node:fs/promises`, `node:path`, and `node:url` modules.
- JSON question data.
- npm scripts defined in `test-app/package.json`.

## How it works

1. `index.js` creates a readline interface and loads `data/questions.json`.
2. The player selects a category and an available question count.
3. A `Quiz` instance shuffles the selected questions and tracks progress, answers, and score.
4. Each question is displayed with numbered options; invalid menu input is rejected and retried.
5. The application shows feedback and an optional explanation after every answer.
6. Final results include the category, score, percentage, performance message, and incorrect-answer review.
7. The player can start another quiz or exit.

There is no HTTP server, API, database, external service, or build pipeline in the repository.

## Prerequisites

- Node.js 18 or newer. The package manifest declares the engine requirement as `>=18.0.0`.
- A terminal capable of displaying ANSI escape codes for the colorized output.

## Installation and setup

From the repository root:

```bash
cd test-app
npm install
```

The project currently declares no npm dependencies, so installation does not need to download runtime packages. Running `npm install` is still a standard way to initialize the local npm project.

## Configuration and question data

The application has no environment variables or configuration files beyond `test-app/package.json` and `test-app/data/questions.json`.

Questions are loaded at runtime from `data/questions.json`, relative to `index.js`. The JSON contains a `categories` object. Each category has a display `name` and a `questions` array. Each question contains:

- `question`: prompt text.
- `options`: answer choices in display order.
- `answer`: zero-based index of the correct option.
- `explanation`: optional feedback text.

To add or edit quiz content, preserve this structure and ensure each `answer` value points to an item in its question's `options` array. The application uses the category object keys internally and displays each category's `name`.

## Running the application

From `test-app`:

```bash
npm start
```

Equivalent direct command:

```bash
node index.js
```

The application is interactive and expects input from the terminal. It clears the terminal before displaying the welcome banner, so it should be run in a normal interactive shell rather than a non-interactive pipeline.

## Usage

When prompted:

1. Enter the number for a category.
2. Enter the number for the question count. `All questions` is always offered; `3 questions` and `5 questions` are offered when the category contains enough questions.
3. Press Enter to begin.
4. For each question, enter the number of the selected answer.
5. Press Enter between questions when prompted.
6. Review the results and answer `y` or `n` when asked whether to play again.

The included data currently provides five questions in each category, so all three question-count choices are available for every included category.

## Build and distribution

No build step is defined. The application runs directly from its JavaScript source files using Node.js. There is no transpilation, bundling, Docker configuration, or packaging script in the repository.

## Testing

The package defines the following test command:

```bash
npm test
```

This invokes Node.js's built-in test runner with `node --test`. No test files are currently present in the repository, so the command is the available test entry point but does not run project-specific test cases at this time.

## Project structure

```text
test-app/
├── data/
│   └── questions.json     # Categories and multiple-choice question content
├── src/
│   ├── colors.js          # ANSI color and text-style helpers
│   ├── input.js           # readline interface and interactive prompts
│   └── quiz.js            # Quiz state, scoring, shuffling, and results
├── index.js               # Application entry point and main loop
├── package.json           # npm metadata, scripts, and Node.js requirement
└── README.md              # Project documentation
```

The repository also contains macOS metadata files under `__MACOSX/` and `.DS_Store`; these are not used by the application.

## Development

The project uses native ES module syntax because `package.json` sets `"type": "module"`. Keep imports with their `.js` extensions, as used by the existing source.

Useful development commands from `test-app`:

```bash
npm start       # Run the interactive quiz
npm test        # Run Node's built-in test runner
node index.js   # Run the entry point directly
```

The main extension point for new content is `data/questions.json`. Changes to quiz behavior belong primarily in `src/quiz.js`, while terminal prompts are centralized in `src/input.js` and styling helpers are in `src/colors.js`.

## Troubleshooting

### Node reports an unsupported engine

Install Node.js 18 or newer, then run the application again. The required version is declared in `package.json`.

### Questions fail to load

Run the command from the `test-app` directory or use `npm start` after changing into that directory. Confirm that `data/questions.json` exists and remains valid JSON with the expected `categories` structure.

### A menu keeps rejecting input

Enter a whole number corresponding to one of the displayed options. The input handler trims whitespace and accepts only numeric selections within the displayed range.

### Colors or box-drawing characters do not display correctly

Use a terminal with ANSI color and Unicode support. The application uses ANSI escape codes and box-drawing/block characters directly; no color library is installed.

## License

This project is licensed under the MIT License, as declared in `test-app/package.json`.
