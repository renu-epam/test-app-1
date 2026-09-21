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

## Question Data Format

Questions are stored in `test-app/data/questions.json`. The data contains three categories:

- `javascript`
- `nodejs`
- `general`

Each category includes a display name and five questions. A question uses the following structure:

```json
{
  "question": "What does a JavaScript function return when it has no return statement?",
  "options": [
    "null",
    "undefined",
    "false",
    "0"
  ],
  "correct": 1,
  "explanation": "A function without a return statement implicitly returns undefined."
}
```

### Question Fields

| Field | Description |
|---|---|
| `question` | The question text shown to the player. |
| `options` | An array of answer choices displayed as numbered options. |
| `correct` | Zero-based index of the correct option in the `options` array. |
| `explanation` | Explanation shown after the player answers. |

For example, `"correct": 1` identifies the second option because array indexes start at zero.

## Extending the Question Bank

To add or update questions:

1. Open `test-app/data/questions.json`.
2. Add a question to an existing category or add a new category using the existing data shape.
3. Ensure every question includes:
   - A non-empty `question` string
   - An `options` array
   - A valid zero-based `correct` index
   - An `explanation` string
4. Confirm that the `correct` index points to an item in the `options` array.
5. Run the application from `test-app/` and verify the new question manually.

Example:

```json
{
  "question": "Which built-in Node.js module provides file system promises?",
  "options": [
    "fs/promises",
    "http/promises",
    "path/promises",
    "readline/promises"
  ],
  "correct": 0,
  "explanation": "The fs/promises module provides promise-based file system APIs."
}
```

The current selection behavior takes the first requested number of entries from a category and then shuffles those selected entries. It does not randomly sample from the entire category before selecting the requested number.

## Architecture

The application uses a small modular architecture built on Node.js built-in APIs.

```text
index.js
  ├── Loads questions.json
  ├── Creates the readline interface
  ├── Displays menus
  ├── Coordinates Quiz
  └── Handles replay and top-level errors

src/input.js
  └── Prompt and validation helpers

src/quiz.js
  └── Quiz state, shuffling, scoring, feedback, and review

src/colors.js
  └── Terminal styling and semantic color helpers

data/questions.json
  └── Quiz content
```

### Runtime Modules

The application uses built-in Node.js modules, including:

- `fs/promises` for asynchronous file loading
- `path` for file path handling
- `url` for module-relative path resolution
- `readline` for interactive terminal input

There are no external runtime or development dependencies.

## Testing Status

The repository includes an npm test script:

```bash
npm test
```

This runs:

```bash
node --test
```

No test files are currently present, so the project does not currently have meaningful automated test coverage. Validation is primarily manual by running the interactive application:

```bash
npm start
```

Potential future tests could cover:

- Question loading and validation
- Fisher-Yates question shuffling
- Correct-answer evaluation
- Score calculation
- Input validation
- Handling of empty or malformed categories

## Configuration

The application does not currently use environment variables, command-line arguments, or separate configuration files.

Current configuration locations include:

- Node.js engine requirement: `test-app/package.json`
- Menu labels and question-count choices: `test-app/index.js`
- Terminal styles: `test-app/src/colors.js`
- Quiz questions and categories: `test-app/data/questions.json`

## Troubleshooting and Caveats

### Run commands from the correct directory

The application is located in `test-app/`. If commands are run from the repository root, npm may not find the application’s `package.json`.

```bash
cd test-app
npm start
```

### Terminal compatibility

The application uses ANSI color codes and Unicode characters. If colors or symbols display incorrectly, use a modern terminal or a terminal configuration with ANSI and Unicode support.

### Interactive terminal requirement

The quiz expects interactive input through `readline`. Running it in a non-interactive environment may prevent prompts from working correctly.

### Question data validity

The application assumes that `questions.json` is correctly structured. Invalid JSON, missing fields, or an out-of-range `correct` index may cause incorrect behavior or runtime errors.

### Empty categories

Empty categories can result in invalid question counts or percentage calculations. Ensure that each selectable category contains valid questions.

### Question selection behavior

When a player selects fewer questions than are available, the application takes the first requested entries and then shuffles them. It does not select a random subset from the complete category.

### Repository metadata

The repository currently includes macOS metadata artifacts such as `.DS_Store` and `__MACOSX/` files. These files are not required by the application and should generally be removed and ignored in future development.

### Error handling

Top-level error handling is present, but malformed question data and some invalid runtime states may still require additional validation.

## Development Recommendations

- Add automated tests for quiz logic and input validation.
- Add validation for the question JSON before starting a game.
- Improve random question selection so a subset is sampled from the full category.
- Handle empty categories and insufficient question counts explicitly.
- Consider separating menu configuration from `index.js`.
- Add a `.gitignore` file for macOS metadata and generated files.
- Add formatting and linting configuration if the project grows.
- Keep question indexes synchronized with their option arrays.
- Test the application in terminals with and without ANSI color support.
- Consider adding a non-interactive mode only if future automation or CI usage requires it.

## Contributing

Contributions are welcome. Before making changes:

1. Fork or clone the repository.
2. Create a focused branch for your change.
3. Make changes inside `test-app/`.
4. Preserve the existing native ES Module style.
5. Update `data/questions.json` carefully when adding quiz content.
6. Run the application manually:

   ```bash
   cd test-app
   npm start
   ```

7. Run the available test command:

   ```bash
   npm test
   ```

8. Review the diff and remove unrelated files or metadata artifacts.
9. Submit a pull request describing the change and how it was verified.

When adding questions, verify that the answer index is zero-based and that the explanation matches the intended answer.

## License

No license file was found in the repository. The project should not be assumed to have an open-source license. Licensing terms should be clarified before redistributing, modifying, or incorporating the project into another product.
