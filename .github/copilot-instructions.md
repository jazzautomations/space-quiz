# Copilot instructions

## Build, test, and lint

- The app is a standalone `index.html`; open it directly in a browser (`file://`). No server, build step, package manager, or external dependency is needed.
- No test runner, test files, or lint commands are currently configured. There is no single-test command.
- For a quick syntax check of the inline JavaScript, extract the `<script>` contents from `index.html` and pass them to `new Function(...)` in Node.js.

## Architecture

- The entire app lives in `index.html`: semantic markup, embedded CSS, and a vanilla JavaScript quiz controller. Keep it self-contained unless the project requirements explicitly change.
- The `questions` array is the quiz content source. Each item has a prompt, answer strings, and a zero-based `correct` answer index.
- Quiz state (`currentQuestion`, `score`, and `answered`) is managed in the inline script. `renderQuestion()` updates the question UI; `chooseAnswer()` handles one selection, score and progress updates, feedback, and advancing; `showResults()` and the restart handler manage the end and replay flows. The personal best is stored in browser `localStorage` when available, with a session-only fallback.
- CSS custom properties define the light theme and are overridden by `prefers-color-scheme: dark`. Motion is also reduced through `prefers-reduced-motion`, including an immediate final score instead of a count-up.

## Codebase conventions

- Keep markup, styles, and behavior in `index.html`; there is no framework or module system.
- When changing quiz content, preserve the question object shape and zero-based answer indices. Progress maximum and question labels are derived from `questions.length`.
- Keep DOM IDs used by the script aligned with the corresponding elements in the markup. Use the existing question-rendering, answer-selection, results, and restart flow rather than adding parallel state.
- Preserve keyboard support and accessible status updates: answers and actions are native buttons, focus moves to the next question or results heading, answer feedback uses a live region, and progress exposes its value as a progress bar.
- Use the existing CSS variables for theme-sensitive colors and honor both color-scheme and reduced-motion preferences when changing visual behavior.
- If Playwright MCP is available, use browser checks for the full quiz flow: answer all questions, verify score and progress, inspect the results and replay states, and confirm keyboard and reduced-motion behavior.
