# Personal Notes

This file is yours. Claude reads it for context but **does not edit it**.

Use it for whatever helps you: analogies that clicked, mistakes you want to remember, confusing topics to revisit, links to good articles, questions to ask later, anything.

Suggested structure (feel free to ignore):

- **Concepts I want to revisit:** ...
- **Mistakes I made and what I learned:** ...
- **Analogies that worked for me:** ...
- **Links / resources:** ...
- **Open questions for next session:** ...

---

_(start writing here)_


Q1. **Node.js vs browser JS engine.**
  Both Node and browsers run JavaScript, but the runtime environment around the engine differs.
  - Engines: Node always uses V8. Browsers vary — Chrome/Edge use V8, Firefox uses SpiderMonkey, Safari uses JavaScriptCore.
  - Node runs on a PC or server and gives you OS-level APIs: files (fs), network, process.
  - Browser JS engine runs inside a browser and gives you page-level APIs: DOM, events.
  - In an Angular project: Node builds the project and runs the dev tooling; the browser JS engine executes the Angular app for the user.
  - Code written for one usually won't run in the other.

  ---
  Q2. **What npm install does.**
  Installs project dependencies in three steps:
  1. Reads package.json for the list of dependencies.
  2. Downloads the packages and their recursive dependencies from the npm registry (registry.npmjs.org).
  3. Creates on disk:
    - node_modules/ — folder containing all installed packages.
    - package-lock.json — a lockfile recording the exact version of every package, making installs reproducible across machines.

  ---
  Q3. **dependencies vs devDependencies.**
  - dependencies — packages the app needs at runtime to actually work (e.g., @angular/core, rxjs). Shipped with the app.
  - devDependencies — packages only needed during development: test runners, linters, build tools (e.g., vitest, eslint, prettier). Not shipped to
  production.
  - Why the split: smaller production install, faster CI, no dev tooling on the server.
  - Mechanism: in production deploys, npm install --production (or npm ci --omit=dev) skips devDependencies.

  ---
  Q4. **.gitignore + why node_modules/ is in it.**
  .gitignore is a file that tells git which files and folders must not be added to the repository.
  node_modules/ is ignored because:
  1. Reproducible — anyone can run npm install to recreate it from package.json + package-lock.json. No need to store it.
  2. Huge — often tens of thousands of packages and their dependencies; would flood the repo.
  3. OS-specific — can contain binaries built for the installing machine; each PC should install its own.
  4. No code review value — it's third-party library code, not yours.

  ---
  Q5. **CLI + Angular CLI.**
  - CLI = Command Line Interface — a program you interact with by typing commands in a terminal (vs clicking buttons in a GUI). Examples: git, npm, ng.
  - Angular CLI is the official set of ng commands to create, run, build, test, and update Angular projects:
    - ng new — scaffold a project
    - ng generate — create components/services/pipes
    - ng serve — dev server with live reload
    - ng build — production build
    - ng test — run tests
    - ng update — upgrade Angular versions
  - What it wires up for you: TypeScript, the bundler (Webpack/esbuild), dev server, test runner, file conventions. Instead of configuring all that by
  hand, the CLI does it.