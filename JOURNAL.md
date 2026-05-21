# Course Journal

Session-by-session log of progress, questions, blockers, and exam answers. Read at the start of every session to restore context. Updated by Claude at the end of each session; the user adds their own "lessons learned" bullets per chapter.

Most recent entry is at the **top**.

---

## 2026-05-21 — Chapter 0 complete

**Covered**
- Verified the toolchain: Node v24.14.1, npm 11.11.0, Angular CLI 21.2.11 — all comfortably above the chapter's `≥20` / `≥18` thresholds.
- Wired SSH to GitHub: existing `~/.ssh/id_rsa.pub` (RSA, from 2022) added to GitHub account `AnnaKira`; verified with `ssh -T git@github.com` (got the "Hi AnnaKira! ... does not provide shell access" success line).
- Pushed the local repo to GitHub: `git remote add origin git@github.com:AnnaKira/angular-learning-project.git` + `git push -u origin main`. Repo now lives on GitHub with the four `.md` files.
- Took the Chapter 0 exam:
  - First attempt: **10/50 (20%)** — concepts present in vibe but not substance.
  - After re-reading explanations, second attempt: **44/50 (88%)** — pass.
- Built a Chapter 0 cheat sheet (5 Q&A merged with corrections) for `NOTES.md`.
- Fixed a stale path reference in `CLAUDE.md` and `ROADMAP.md` (was `/Users/igorokhov/repos/iorgvi/...`, now `/Users/annagorohova/repos/...`).

**Questions asked / decisions made**
- Existing RSA key from 2022 was kept (instead of generating a new ed25519). Fine for now; can upgrade later with `ssh-keygen -t ed25519`.
- Empty GitHub repo was created **without** README/.gitignore/license so the first push wouldn't conflict with local files.

**Blockers**
- None.

**Exam — questions and answers (for the audit trail)**
1. *Node vs browser JS engine* — Both run JS. Node uses V8 only; browsers vary (V8 in Chrome/Edge, SpiderMonkey in Firefox, JavaScriptCore in Safari). Node exposes OS-level APIs (`fs`, network, process); browsers expose page-level APIs (DOM, events). In Angular: Node builds and runs the dev tooling; the browser executes the app for the user.
2. *What `npm install` does* — Reads `package.json` for dependency list → downloads packages (and recursive deps) from `registry.npmjs.org` → creates `node_modules/` (the installed folder) and `package-lock.json` (lockfile pinning exact versions for reproducible installs).
3. *`dependencies` vs `devDependencies`* — `dependencies` are needed at runtime and ship with the app; `devDependencies` are dev-only (test runners, linters, build tools) and skipped in production via `npm install --production` / `npm ci --omit=dev`. Keeps prod installs smaller and faster.
4. *`.gitignore` + why `node_modules/`* — `.gitignore` is a list of paths git won't track. `node_modules/` is ignored because it's (a) reproducible from `package.json` + `package-lock.json`, (b) huge, (c) potentially OS-specific (native binaries), (d) third-party code with no review value.
5. *CLI + Angular CLI* — CLI = Command Line Interface; a program controlled by typed commands instead of a GUI. Angular CLI provides `ng new` / `ng generate` / `ng serve` / `ng build` / `ng test` / `ng update`, and wires up TypeScript, the bundler, dev server, test runner, and file conventions so you don't configure them by hand.

**Next session — Chapter 1: Hello Angular**
- Goal: scaffold the `finance-tracker/` app and render the first custom component.
- First tasks: `ng new finance-tracker --standalone --style=css --routing`, run `ng serve`, read the generated files and describe each in `NOTES.md`, then build a child `DashboardComponent` and bind a class property via interpolation. ESLint + Prettier setup at the end.
- Kickoff prompt: *"Read CLAUDE.md, ROADMAP.md, and JOURNAL.md. Tell me where I am, what I just finished, and what's next. Then let's start chapter 1."*

**Lessons learned (your own words — fill in 3 bullets before committing)**
- too many terms and concepts, much to cram. 
- working in terminal and Angular CLI is tricky
- happy to get the infrastructure installed

---

## 2026-05-13 — Course kickoff

**Covered**
- Defined goals: solid Angular fundamentals, junior-ready frontend skills, practice with an AI mentor.
- Picked the project: Personal Finance Tracker, single app growing chapter-by-chapter.
- Locked the tech stack: modern Angular (standalone + signals), plain CSS with CSS custom properties, signals-only state, Vitest browser mode + Playwright, Angular Material at chapter 13, Cloudflare Pages deploy.
- Wrote the 16-chapter roadmap in `ROADMAP.md`.
- Set up the workflow files: `CLAUDE.md`, `ROADMAP.md`, `JOURNAL.md`, `NOTES.md`.

**Questions asked / decisions made**
- Styling: locked to **plain CSS** (not SCSS) — keeps you practicing real CSS alongside the parallel CSS course.
- Testing: locked to **Vitest with browser mode** (Angular's new default) + **Playwright** for e2e. Jest mentioned only for ecosystem awareness.

**Blockers**
- None. You haven't started Chapter 0 yet.

**Next session**
- **Chapter 0 — Dev Environment & Tooling.** Concepts: Node, npm, terminal, git, VS Code, CLI. Tasks: install Node + Angular CLI, learn ~10 terminal commands, init git, push to GitHub, copy ROADMAP into the repo (already done).
- Kickoff prompt to use: *"Read CLAUDE.md, ROADMAP.md, and JOURNAL.md. Tell me where I am, what I just finished, and what's next. Then let's start chapter 0."*

**Lessons learned (your own words — fill in after each chapter)**
- _(Chapter 0 not started yet)_

---
