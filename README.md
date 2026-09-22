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

## Quiz Data

Quiz content is stored in:

```text
data/questions.json
```

The data is organized by category:

```json
{
  "categories": {
    "javascript": {
      "name": "JavaScript Basics",
      "questions": []
    },
    "nodejs": {
      "name": "Node.js Fundamentals",
      "questions": []
    },
    "general": {
      "name": "General Programming",
      "questions": []
    }
  }
}
```

Each question contains a prompt, answer options, a zero-based correct-answer index, and an optional explanation:

```json
{
  "question": "Example question?",
  "options": ["Option A", "Option B", "Option C"],
  "answer": 0,
  "explanation": "Explanation of the correct answer."
}
```

The current dataset contains 15 questions total, with five questions in each category.

## Project File Structure

```text
test-app/
├── index.js                  # Application entry point and quiz coordinator
├── package.json              # Project metadata, scripts, and Node.js configuration
├── data/
│   └── questions.json        # Categories and quiz questions
└── src/
    ├── colors.js             # ANSI color and terminal-style utilities
    ├── input.js              # Readline-based input and selection helpers
    └── quiz.js               # Quiz state, question handling, scoring, and results
```

Repository-level artifacts:

```text
.DS_Store                     # macOS filesystem metadata; not application logic
__MACOSX/                     # macOS archive metadata; not application logic
```

## Available npm Scripts

| Command | Description |
|---|---|
| `npm start` | Starts the quiz application with `node index.js` |
| `npm test` | Runs Node.js’s built-in test runner |

## Application Flow

```text
Start application
      │
      ▼
Load data/questions.json
      │
      ▼
Display welcome banner
      │
      ▼
Select category
      │
      ▼
Select question count
      │
      ▼
Shuffle selected questions
      │
      ▼
Answer questions interactively
      │
      ▼
Display feedback and explanations
      │
      ▼
Display score and incorrect-answer review
      │
      ▼
Choose whether to play again
```

## License

This project is licensed under the MIT License.
