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

**CHAPTER 0** --- GENERAL CONCEPTS

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



**CHAPTER 1** -- ANGULAR PROJECT COMPONENTS

**Root level**
1. File *angular.json* — the main configuration file for the Angular project; it defines how the project is built, served, and which files or styles are used.

2. File *package.json* — a file with project information, dependencies, and commands in the "scripts" section, such as start, build, and test. npm start / npm test in scripts are wrappers around ng serve / ng test.

3. File *tsconfig.json* — the main TypeScript configuration file for the whole project. Defines compiler options like strict mode and ES target for the whole workspace; the others extend it.

4. File *tsconfig.app.json* — TypeScript settings specifically for compiling the application code.

5. File File *tsconfig.spec.json* — TypeScript settings used when running tests, especially files with the .spec.ts extension.

6. *.editorconfig* — a file with formatting rules for editors, such as indentation, encoding, and line endings.

7. File *.prettierrc* — settings for Prettier, a tool that automatically formats code.

8. File *README.md* — a text file with a project description and basic instructions, usually created automatically by Angular CLI.


**Folders**
⸻
1. Folder *public/* — this folder contains static assets, such as images, icons, or other files that are copied directly and can be used by the app. Served as-is at the app's root URL.

⸻
2. Folder *.vscode/* — this folder contains Visual Studio Code settings for this project, for example recommended extensions in extensions.json or editor settings in settings.json.

⸻
3. Folder *src/* — this folder contains the actual source code of the Angular application.

file *src/index.html* — this is the main HTML page, but it has almost no markup because Angular inserts the app content into it dynamically. there's specifically a <app-root></app-root> tag — the selector from app.ts — that's the anchor point where Angular mounts the app. 

file *src/main.ts* — this is the bootstrap file and the main entry point that starts the Angular application.
file *src/styles.css* — this file contains global CSS styles that apply to the whole application.

⸻
4. Folder **src/app/** — this folder contains the root Angular component and the main files for the app’s structure and logic.

a) File *src/app/app.ts* — this is the root component file, where the main Angular component class is defined.

Questions to file *src/app/app.ts*:

- What is inside the @Component({...}) decorator in app.ts?
It contains metadata for the component, such as selector, imports, templateUrl, and styleUrl.

- What is selector?
selector is the HTML tag name used to place this component on the page, for example <app-root>.

- What is imports?
imports lists other components, directives, or modules that this standalone component needs.

- What is templateUrl?
templateUrl points to the HTML template file for the component, usually ./app.html.

- What is styleUrl?
styleUrl points to the CSS file for the component, usually ./app.css.

b) File *src/app/app.html* - this is the template file for the root component, where the component’s HTML layout is written.

c) File *src/app/app.css* — this file contains styles that apply only to the root component.

d) File *src/app/app.spec.ts* — this file contains tests for the root component.

e) File *src/app/app.routes.ts* — this file contains route definitions that tell Angular which component to show for different URLs.

f) File *src/app/app.config.ts* — this file contains app-level configuration and is used together with main.ts when the application starts.

Question to file *src/app/app.config.ts*:

Why are app.config.ts and main.ts important together?
main.ts starts the Angular app, and app.config.ts provides the app-level settings used during startup.