# Orbital Field Notes

A standalone, accessible space-exploration quiz. Answer 10 questions, learn a short fact after each answer, track your score, and see your personal best.

## Run locally

Open `index.html` directly in a browser. The app has no server, build step, package manager, or external dependencies. Your personal best is saved in the browser when local storage is available.

## Accessibility

The quiz supports keyboard navigation, announces answer feedback to assistive technology, respects the system color scheme, and reduces motion when requested.

## Deployment

GitHub Actions publishes the static site to GitHub Pages when changes are pushed to `main`. The workflow copies `index.html` to a deployment artifact; no site build tools are needed.
