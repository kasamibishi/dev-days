# Project Guidelines

## Architecture

- This is a dependency-free, single-page static quiz. The entire application lives in [`index.html`](../index.html): semantic markup, inline CSS, and inline JavaScript are intentionally kept together so the page can be opened directly with a `file:` URL.
- The quiz state is held in the script-level `current`, `score`, and `answered` variables. The `questions` array is the single source of truth for question text, answer choices, and zero-based correct-answer indexes.
- `renderQuestion()` rebuilds the answer buttons and updates the counter, score, progress bar, and feedback region. `chooseAnswer()` locks the current question, applies the correct/incorrect visual state, and reveals the next control. `showResults()` swaps the quiz view for the results view; the restart handler resets state and renders the first question.
- Preserve the existing DOM IDs and class names when changing behavior because the script and CSS use them as the component boundary. Keep new UI state synchronized with the accessible text and ARIA attributes, not only with visual styles.

## Build, Test, and Lint

- There is no package manager, build step, test suite, or lint configuration. Do not add dependencies for routine changes.
- Validate changes by opening [`index.html`](../index.html) directly in a browser (the VS Code integrated browser is the preferred workflow) and exercising the quiz from answer selection through results and restart.
- For focused manual checks, verify both correct and incorrect answers, score/progress updates, keyboard focus behavior, the final results screen, and the responsive single-column answer layout at narrow widths.

## Conventions

- Keep the app self-contained: use inline CSS and JavaScript, avoid external assets and network requests, and do not introduce a server requirement.
- Follow the existing visual language: CSS custom properties are defined in `:root`; colors, spacing, rounded cards, and animations should reuse those tokens and patterns rather than introducing unrelated styling systems.
- Use semantic HTML and native controls. Answer choices and actions are `<button>` elements; status text belongs in the existing live feedback region; progress changes belong on the existing `role="progressbar"` element.
- Preserve accessibility behavior when editing interactions: keep visible `:focus-visible` styles, button disabled states after an answer, `aria-live` feedback, reduced-motion handling, and the heading focus transfer when advancing questions.
- Keep the question data declarative in the `questions` array and use zero-based indexes for `correct`, matching the current rendering logic.
