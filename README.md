# Quiz CLI

A small interactive Node.js command-line quiz application. Users select a quiz category and question count, answer multiple-choice questions in the terminal, and receive immediate feedback, explanations, progress updates, and a final results summary.

The application is located in the [`test-app/`](./test-app/) directory.

## Features

- Interactive terminal-based quiz experience
- Quiz categories:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Multiple-choice questions with:
  - Question text
  - Answer options
  - Zero-based correct-answer index
  - Explanations
- Question-count selection:
  - All questions
  - Three questions
  - Five questions
- Immediate correctness feedback after each answer
- Answer explanations
- Progress and score tracking
- Review of incorrect answers at the end of the quiz
- Option to replay the quiz
- Native Node.js ES modules
- No runtime or development dependencies

## Prerequisites

- [Node.js](https://nodejs.org/) version 18 or later
- An interactive terminal

The required Node.js version is specified in `test-app/package.json`:

```json
{
  "engines": {
    "node": ">=18"
  }
}
```

## Installation

Clone the repository and move into the application directory:

```bash
git clone https://github.com/renu-epam/test-app-1.git
cd test-app-1/test-app
```

The project uses only Node.js built-in modules and does not require external dependencies. Running `npm install` is optional:

```bash
npm install
```

There is currently no lockfile or dependency installation requirement.

## Running the Application

From the `test-app/` directory, start the quiz with:

```bash
npm start
```

Alternatively, run the entry point directly:

```bash
node index.js
```

The application is designed for local terminal use and does not provide a web server, API, or deployment configuration.

## Interactive Flow

When the application starts:

1. Select a quiz category from the displayed menu.
2. Select the number of questions:
   - All available questions
   - Three questions
   - Five questions
3. Answer each question by entering the corresponding numeric option.
4. Press Enter when prompted to continue between questions.
5. Review whether each answer was correct, along with the explanation.
6. View the final score and progress summary.
7. Review incorrect answers, if any.
8. Choose whether to replay the quiz.

The CLI expects numeric menu choices and an interactive terminal session. Output uses ANSI color codes, and `console.clear()` behavior may vary depending on the terminal environment.

## Quiz Data Format

Quiz content is stored in:

```text
test-app/data/questions.json
```

The data contains the available categories. Each category contains five multiple-choice questions. Each question is expected to include:

- `question`: The question text
- `options`: The available answer choices
- `answer`: A zero-based index identifying the correct option
- `explanation`: Text explaining the correct answer

A representative question object has the following shape:

```json
{
  "question": "What is the purpose of ...?",
  "options": [
    "Option A",
    "Option B",
    "Option C",
    "Option D"
  ],
  "answer": 1,
  "explanation": "The correct answer is Option B because ..."
}
```

The application assumes that the JSON data is valid. Malformed or incorrectly structured data can cause the application to fail during startup.

### Question Selection Behavior

When three or five questions are selected, the application takes the first three or five questions from the selected category before shuffling them. It does not select a random subset of questions.

## Project Structure

```text
test-app/
├── data/
│   └── questions.json   # Static quiz categories and questions
├── src/
│   ├── colors.js        # Terminal color and formatting helpers
│   ├── input.js         # Interactive input and readline utilities
│   └── quiz.js          # Quiz flow, scoring, feedback, and results
├── index.js             # Application entry point
└── package.json         # Project metadata and npm scripts
```

The application resolves the quiz data path relative to `index.js` using the ES module location, so it can locate `data/questions.json` independently of the current working directory once started from the project.

## Available Scripts

Run these commands from `test-app/`:

| Command | Description |
| --- | --- |
| `npm start` | Starts the quiz application |
| `npm test` | Runs Node.js's built-in test runner |

`npm start` is equivalent to:

```bash
node index.js
```

`npm test` runs:

```bash
node --test
```

## Testing Status

The project currently does not contain test files. The `npm test` script is configured to invoke Node.js's built-in test runner, but automated application tests have not yet been implemented.

Manual testing can be performed by running:

```bash
npm start
```

and completing each category, question-count option, answer flow, results review, and replay path.

## Caveats

- The application requires an interactive terminal and is not intended for non-interactive environments.
- Menu selections and answers must be entered as numeric choices.
- Users are prompted to press Enter between questions.
- ANSI colors and terminal clearing may not behave consistently in every terminal.
- The quiz data is static and stored locally in JSON.
- The JSON structure is assumed to be valid; malformed data is not handled with a dedicated validation or recovery flow.
- Selecting three or five questions uses the first questions in the selected category before shuffling rather than choosing a random subset.
- The repository currently has no automated tests, CI configuration, Docker configuration, environment configuration, or deployment setup.
- Repository artifacts such as `__MACOSX` and `.DS_Store` are not part of the application.

## Future Improvements

Potential improvements include:

- Add automated unit and integration tests
- Validate quiz data at startup with clearer error messages
- Select a random subset when the user chooses three or five questions
- Improve handling of invalid input and interrupted sessions
- Add configuration for custom quiz data
- Improve terminal compatibility and accessibility
- Add CI checks for linting and tests
- Add a more detailed score history or persistent results
- Provide additional categories and question sets

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT), as specified in `test-app/package.json`.
