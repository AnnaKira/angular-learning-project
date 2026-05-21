# Angular Learning Course — Personal Finance Tracker

## Context

**Why this course exists.** The learner wants to (1) build solid Angular fundamentals while doing parallel HTML/CSS and JS/TS courses, (2) reach a level where they can take on junior frontend tasks using Angular, and (3) practice working with an AI agent that alternates between trainer, examiner, and code reviewer.

The chosen project is a **Personal Finance Tracker** — a single app that grows chapter-by-chapter from a static page into a deployed, tested, real-API-backed application. Each chapter introduces new Angular concepts driven by a real feature the app needs.

**What "done" looks like:** a deployed live app, a polished README in the repo, the ability to confidently answer 20+ junior-level Angular interview questions in writing, and an end-to-end workflow of using an AI mentor for both learning and code review.

---

## Course Profile

| | |
|---|---|
| **Pace** | ~20+ hrs/week (intensive). 16 chapters, ~6–8 weeks total. |
| **Starting baseline** | HTML/CSS course complete. JS/TS in progress. No npm/terminal experience yet. |
| **Project structure** | Single Angular app, grows chapter-by-chapter. |
| **Styling** | Plain CSS (with CSS custom properties for design tokens); UI library introduced in chapter 13. |
| **Data layer** | Mock data → JSON Server (chapter 9) → real public API (chapter 14). |
| **State management** | Signals only (`signal`, `computed`, `effect`) + service pattern. |
| **Testing** | Dedicated chapter mid-course (chapter 10). |
| **AI mentor role** | Adaptive: explain new concepts → review your code → quiz with written exam questions per chapter. |

---

## How to Use This Course (AI Mentor Workflow)

Every chapter follows the same rhythm:

1. **Start of chapter** — Read the *Concepts* list. Ask the AI mentor to explain anything unfamiliar with examples relevant to the finance tracker.
2. **Do the tasks** — Work through *Hands-on Tasks* by yourself. Tick `[ ]` → `[x]` as you finish.
3. **Self-review** — Run through the *Code Review Checklist* before asking for review.
4. **Code review** — Ask the AI mentor: "Review chapter N." It will critique like a code reviewer, list issues, suggest improvements.
5. **Exam** — Answer the *Exam Questions* **in writing, in your own words, without looking at the code**. Then ask the AI mentor to grade.
6. **Only then** move to the next chapter.

**Important:** Don't let the AI write your code for you in this course. Ask it to *explain*, *review*, and *quiz* — not generate. The goal is your fluency, not finished code.

---

## Tech Stack Decisions (locked)

- **Angular** — latest stable (modern Angular: standalone components, signals, new control flow `@if`/`@for`/`@switch`, `inject()` function).
- **Language** — TypeScript with strict mode on.
- **Styling** — Plain CSS until chapter 13. Use **CSS custom properties** (`--color-primary`, etc.) for the design system. No SCSS, no utility-first frameworks early on — you mentioned a CSS course in parallel, so this keeps you practicing real CSS.
- **State** — Signals + service-owns-state pattern. No NgRx.
- **Forms** — Both template-driven (intro) and reactive (production use).
- **HTTP mock** — `json-server` package from chapter 9.
- **Charts** — `ng2-charts` (Chart.js wrapper) — chosen for popularity and good docs. Reconsider in chapter 11 if it feels wrong.
- **Testing** — **Vitest with browser mode** (Angular's new default test runner, replacing Karma). Jest is the well-known alternative and worth knowing about but we will use Vitest. **Playwright** for end-to-end tests.
- **UI library (chapter 13)** — Angular Material (most aligned with junior job postings).
- **Real API (chapter 14)** — TBD; likely exchangerate-api.com for currency conversion since the app already handles money.
- **Deployment** — Cloudflare Pages or Netlify (free, fast, no card).
- **Code quality** — ESLint + Prettier from chapter 1.

---

## Critical Files (created during the course)

| Path | Purpose | Introduced in |
|---|---|---|
| `/Users/annagorohova/repos/angular-learning-project/` | Project root (currently empty) | Chapter 1 |
| `package.json`, `angular.json`, `tsconfig.json` | Project config | Chapter 1 |
| `src/main.ts`, `src/app/app.config.ts` | Bootstrap | Chapter 1 |
| `src/app/app.component.{ts,html,css}` | Root component | Chapter 1 |
| `src/app/features/transactions/` | Transactions feature module | Chapter 2 |
| `src/app/features/categories/` | Categories feature module | Chapter 8 |
| `src/app/features/stats/` | Charts/statistics feature | Chapter 11 |
| `src/app/core/services/` | Singleton services (TransactionsService, etc.) | Chapter 7 |
| `db.json` | JSON Server mock data | Chapter 9 |
| `README.md` | Final portfolio README | Chapter 15 |
| `ROADMAP.md` (copy of this plan) | In-repo learning checklist | Chapter 0 |

---

## Chapters

---

### Chapter 0 — Dev Environment & Tooling

> Goal: have a working development environment and understand what each tool does.

**Concepts to learn**
[x]- What Node.js is (and isn't) — a JS runtime outside the browser.
[x]- npm: package manager, `package.json`, dependencies vs devDependencies, lockfile.
[x]- Terminal basics: `cd`, `ls`, `mkdir`, `rm`, `pwd`, path conventions, environment variables (intro).
[x]- Git basics: `init`, `add`, `commit`, `status`, `log`, `diff`, `.gitignore`.
[x]- What an IDE does. VS Code essentials and useful Angular extensions.
[x]- What a CLI is and why frameworks ship one (`ng`, `npm`, `git`).

**Hands-on Tasks**
[x]- [ ] Install Node.js LTS (via `nvm` recommended) and verify with `node --version` and `npm --version`.
[x]- [ ] Install Angular CLI globally: `npm install -g @angular/cli` and verify `ng version`.
[x]- [ ] Install VS Code + extensions: Angular Language Service, ESLint, Prettier, EditorConfig.
[x]- [ ] Practice 10 terminal commands until they feel natural: `cd`, `ls -la`, `pwd`, `mkdir`, `touch`, `rm`, `cp`, `mv`, `cat`, `grep`.
[x]- [ ] `git init` in the project folder, configure name/email, make a dummy initial commit, learn `git status`/`git log`/`git diff`.
[x]- [ ] Create a GitHub account (if needed), set up SSH key, push the empty repo.
[x]- [ ] Copy this plan file to the project as `ROADMAP.md` so it lives in the repo.

**Exam Questions (answer in writing)**
1. What's the difference between Node.js and a browser's JS engine?
2. What does `npm install` actually do? What gets created on disk?
3. What's the difference between `dependencies` and `devDependencies`?
4. What does `.gitignore` do, and why is `node_modules/` in it?
5. What is a CLI, and what does the Angular CLI specifically provide?

**Code Review Checklist**
[x]- [ ] `node --version` returns 20+ or 22+.
[x]- [ ] `ng version` shows Angular 18+ (or whatever is current LTS).
[x][x]- [ ] `git log` shows an initial commit.
- [ ] `.gitignore` excludes `node_modules` and `.DS_Store`.

---

### Chapter 1 — Hello Angular

> Goal: scaffold the project, understand the file structure, render your first custom component.

**Concepts**
- What Angular is (framework vs library), what makes it opinionated.
- Anatomy of an Angular project: `src/`, `main.ts`, `app.config.ts`, `app.component.*`.
- The **standalone components** model (no NgModules).
- Component = class + template + styles. Decorators.
- `ng serve`, `ng build`, `ng generate` — what they do under the hood.
- Interpolation `{{ }}` and the basics of templates.
- Change detection at a 1000-ft level (just enough to not be confused).

**Hands-on Tasks**
- [ ] `ng new finance-tracker --standalone --style=css --routing` inside the working directory.
- [ ] Run `ng serve` and open the app in the browser.
- [ ] Read every file the CLI generated; write a 1-sentence description of each in a `NOTES.md` (for yourself).
- [ ] Replace the default `app.component.html` with a custom welcome screen for the finance tracker.
- [ ] Add a class property `appTitle = 'Finance Tracker'` and bind it via interpolation.
- [ ] Generate a child component: `ng g c features/dashboard/dashboard`. Render it inside `app.component.html`.
- [ ] Set up ESLint + Prettier (`ng add @angular-eslint/schematics`, then install Prettier).
- [ ] Commit: "chapter 1: scaffold app and first component".

**Exam Questions**
1. What is a standalone component? How does it differ from the old NgModule approach?
2. What is the role of `main.ts`?
3. What is `app.config.ts` for? What does `providers` mean inside it?
4. What does the Angular CLI do when you run `ng generate component`?
5. What is interpolation, and what kinds of expressions are allowed in `{{ }}`?

**Code Review Checklist**
- [ ] `ng serve` runs without errors.
- [ ] At least one custom child component renders inside `AppComponent`.
- [ ] `.editorconfig`, ESLint, Prettier configs present and consistent.
- [ ] No leftover Angular default placeholder content.
- [ ] Commit history shows incremental, meaningful commits.

---

### Chapter 2 — Components, Bindings & Control Flow

> Goal: build a real transaction list UI with parent/child components and the new template syntax.

**Concepts**
- Property binding `[prop]`, event binding `(event)`, two-way binding `[(ngModel)]` (preview).
- Input/output via `input()` and `output()` signal-based APIs.
- New control flow: `@if`, `@else`, `@for` (with `track`), `@switch`.
- Template reference variables `#myInput`.
- Why `track` matters in `@for`.

**Hands-on Tasks**
- [ ] Define a `Transaction` TypeScript interface: `{ id, type: 'income'|'expense', amount, description, date }`.
- [ ] Create a hardcoded array of 5 sample transactions in `DashboardComponent`.
- [ ] Build `TransactionListComponent` that takes transactions via `input()` and renders them with `@for`.
- [ ] Build `TransactionItemComponent` that takes one transaction via `input()` and emits `delete` via `output()`.
- [ ] Wire delete: clicking the trash button removes the item (in parent state).
- [ ] Show an empty state with `@if` when there are no transactions.
- [ ] Use `@switch` to render different icons for income vs expense.
- [ ] Style the list and items with plain CSS — flexbox, hover states.

**Exam Questions**
1. Difference between `[value]="x"` and `value="{{x}}"` — when does each apply?
2. Why does `@for` require a `track` expression? What happens without it?
3. When would you use `output()` vs calling a service directly from the child?
4. What's a template reference variable and where is it useful?
5. New control flow vs the old `*ngFor`/`*ngIf` — what improved?

**Code Review Checklist**
- [ ] No `any` types in interfaces or component classes.
- [ ] Parent passes data down, child emits events up — no other coupling.
- [ ] `@for` has a stable `track` (e.g., `track t.id`).
- [ ] Empty state handled.
- [ ] CSS is component-scoped (no global leaks — Angular's view encapsulation does this by default).

---

### Chapter 3 — Signals & Reactive State

> Goal: make all state reactive using signals, derived state via `computed`.

**Concepts**
- `signal()`, `.set()`, `.update()`, reading via `()`.
- `computed()` — derived state.
- `effect()` — side effects in response to signal changes (use sparingly).
- Why signals replace a lot of Subject/BehaviorSubject usage.
- Signals + change detection — why this is faster.

**Hands-on Tasks**
- [ ] Convert the transactions array into a `signal<Transaction[]>([])`.
- [ ] Implement `addTransaction()` and `deleteTransaction(id)` using `.update()`.
- [ ] Derive `balance`, `totalIncome`, `totalExpense` with `computed()`.
- [ ] Display all three derived values in the dashboard, formatted manually for now.
- [ ] Add an `effect()` that `console.log`s whenever the balance crosses zero.
- [ ] Refactor `TransactionItemComponent` so the delete logic flows back via the signal-owning component.

**Exam Questions**
1. What's the difference between `computed()` and `effect()`? When is each appropriate?
2. Why do you call a signal with `()` to read it? What would happen if you tried `mySignal` directly in a template?
3. What does signal-based change detection avoid that Zone.js-based detection didn't?
4. Why is over-using `effect()` considered an anti-pattern?
5. Why is `update()` safer than `set(currentValue + 1)` in concurrent scenarios?

**Code Review Checklist**
- [ ] No plain class fields holding reactive state.
- [ ] All derived values use `computed()`, not method calls in template.
- [ ] At most one `effect()`, and it's clearly justified.
- [ ] Templates read signals via `()`.

---

### Chapter 4 — Template-Driven Forms

> Goal: introduce form basics with the simplest API.

**Concepts**
- `FormsModule`, `ngModel`, `ngForm`.
- Form state: `dirty`, `touched`, `valid`, `invalid`.
- Built-in validators: `required`, `min`, `max`, `pattern`.
- When template-driven is fine (small forms) vs when to graduate to reactive.

**Hands-on Tasks**
- [ ] Build an "Add Transaction" form with template-driven approach.
- [ ] Fields: type (radio), amount (number), description (text), date (date input), category (select — hardcoded for now).
- [ ] Validate: all required, amount > 0.
- [ ] Show inline validation errors only after the user touches a field.
- [ ] Disable the submit button when invalid.
- [ ] On submit, call `addTransaction()` and reset the form.

**Exam Questions**
1. When does Angular consider a control "touched" vs "dirty"?
2. Why are inline errors usually shown after `touched`, not immediately?
3. What's the difference between `ngModel` with a name attribute inside a form vs standalone?
4. Why is template-driven forms a poor fit for dynamic forms (e.g., add/remove fields)?
5. What does the form's `valid` flag aggregate from?

**Code Review Checklist**
- [ ] Form resets cleanly after submit.
- [ ] Errors only appear after interaction.
- [ ] Submit button disabled when invalid.
- [ ] No business logic in the template — handler delegates to a method.

---

### Chapter 5 — Reactive Forms

> Goal: rebuild the form using reactive forms, the production approach.

**Concepts**
- `ReactiveFormsModule`, `FormBuilder`, `FormGroup`, `FormControl`, `FormArray`.
- Validators (built-in + custom).
- `valueChanges` and `statusChanges` observables.
- Cross-field validation.
- Reusing one form for add and edit modes.

**Hands-on Tasks**
- [ ] Convert the Add Transaction form to reactive forms.
- [ ] Write a custom validator: `amountMustBePositive`.
- [ ] Add cross-field validation: if type is `expense`, amount must not exceed current balance (optional warning, not blocker).
- [ ] Add an Edit Transaction flow that reuses the same form component (route param drives mode).
- [ ] Listen to `valueChanges` and log them.

**Exam Questions**
1. Template-driven vs reactive forms — give two reasons to choose each.
2. How do you write a custom synchronous validator? What's its return shape?
3. What does `FormBuilder` give you over `new FormGroup(...)`?
4. What's the difference between `valueChanges` and `statusChanges`?
5. How would you implement an async validator (e.g., "is this category name unique")?

**Code Review Checklist**
- [ ] One form component handles both add and edit cleanly.
- [ ] Custom validator is in its own file and unit-testable.
- [ ] No memory leaks — subscriptions are managed (or `takeUntilDestroyed` used).
- [ ] Template is thin; logic in the component class.

---

### Chapter 6 — Routing & Navigation

> Goal: turn the single-page UI into a navigable multi-route app.

**Concepts**
- Routes config, `provideRouter`, `RouterOutlet`, `RouterLink`, `RouterLinkActive`.
- Route parameters and query parameters.
- Lazy loading via `loadComponent` / `loadChildren`.
- Route guards (`canActivate` — preview).
- 404 / wildcard routes.

**Hands-on Tasks**
- [ ] Define routes: `/`, `/transactions`, `/transactions/new`, `/transactions/:id/edit`, `/categories`, `/stats`, `/**` (404).
- [ ] Build a top nav with `routerLink` + `routerLinkActive` styling.
- [ ] Read the `:id` param in the edit route and load the transaction.
- [ ] Lazy-load `/stats` with `loadComponent`.
- [ ] Add a guard that blocks `/transactions/:id/edit` if the id doesn't exist.

**Exam Questions**
1. What is lazy loading and what problem does it solve?
2. Difference between route params and query params — when use which?
3. What's the difference between `canActivate` and `canMatch`?
4. How does `RouterLinkActive` decide what counts as active?
5. Why is the wildcard route always last?

**Code Review Checklist**
- [ ] Deep links work (refreshing on a sub-route doesn't 404).
- [ ] Stats route is lazy-loaded (verify in Network tab).
- [ ] Nav active state visually correct.
- [ ] No hardcoded URLs scattered around — use route consts or a routing config.

---

### Chapter 7 — Services & Dependency Injection

> Goal: move all state out of components into singleton services owned by signals.

**Concepts**
- `@Injectable({ providedIn: 'root' })`.
- The injector hierarchy (root, component, route).
- The `inject()` function vs constructor injection.
- Service-owned state pattern: service exposes signals + methods, components are dumb.
- Why testability improves.

**Hands-on Tasks**
- [ ] Create `TransactionsService` that owns the transactions signal and all CRUD methods.
- [ ] Create `CategoriesService` (placeholder for now).
- [ ] Refactor all components to `inject()` services instead of holding state.
- [ ] Move derived computeds (balance, totals) into the service.
- [ ] Confirm no component has business logic — only `inject` and render.

**Exam Questions**
1. What does `providedIn: 'root'` mean? What's an alternative?
2. What does Angular's injector actually do at runtime?
3. When would you provide a service at the component level instead of root?
4. Why is `inject()` preferred in modern Angular? Where can/can't you call it?
5. Why is service-owned state easier to test than component-owned state?

**Code Review Checklist**
- [ ] Components contain zero business logic.
- [ ] Services expose readonly signals (`asReadonly()`) where appropriate.
- [ ] No circular dependencies between services.
- [ ] Inject is used consistently (not mixed with constructor injection).

---

### Chapter 8 — Categories Feature, Pipes & UI Polish

> Goal: round out the second domain entity, master pipes, and polish the look.

**Concepts**
- Pipes: built-in (`currency`, `date`, `decimal`, `percent`, `keyvalue`, `json`).
- Pure vs impure pipes.
- Custom pipes — when warranted, when overkill.
- View encapsulation modes (Emulated, None, ShadowDom).
- Host bindings and `:host` selector in component CSS.

**Hands-on Tasks**
- [ ] Build full CRUD for categories: name, color, icon (emoji), monthly budget (optional, used later).
- [ ] Display transactions with `currency` and `date` pipes.
- [ ] Write one custom pipe: `RelativeDatePipe` (`Today`, `Yesterday`, `3 days ago`).
- [ ] Add category color/icon to each transaction line.
- [ ] Build a coherent design system in plain CSS using **CSS custom properties** (`--color-primary`, `--space-md`, `--font-size-base`, etc.) defined on `:root` in a global stylesheet.
- [ ] Improve accessibility: semantic HTML, alt text, ARIA labels where needed.

**Exam Questions**
1. What's a pure pipe and why is it the default?
2. What problem does view encapsulation solve?
3. When is a custom pipe better than a `computed()` or a method?
4. What's the difference between `transform(value)` and a getter on the component class?
5. Why are semantic HTML and ARIA important — what does a screen reader actually do?

**Code Review Checklist**
- [ ] No hardcoded colors/spacings in components — use CSS custom properties.
- [ ] Custom pipe is pure (no hidden state).
- [ ] All interactive elements are keyboard-accessible.
- [ ] Layout works at mobile and desktop widths.

---

### Chapter 9 — HTTP & JSON Server

> Goal: replace in-memory state with HTTP calls against a local mock REST API.

**Concepts**
- `HttpClient`, `provideHttpClient` in `app.config.ts`.
- Observables (intro): `subscribe`, `pipe`, `map`, `tap`, `catchError`.
- The `async` pipe vs manual subscribe.
- `takeUntilDestroyed()` for cleanup.
- HTTP interceptors (intro — actual use in chapter 14).
- Loading and error UI states.

**Hands-on Tasks**
- [ ] Install `json-server`, create `db.json` with seed data.
- [ ] Add an npm script: `"db": "json-server --watch db.json --port 3001"`.
- [ ] Replace `TransactionsService` methods with `HttpClient` calls returning Observables.
- [ ] Decide: keep a signal "cache" inside the service that's updated after HTTP responses (common real-world pattern).
- [ ] Add loading and error state signals; show spinners / error banners.
- [ ] Convert one consumer to use the `async` pipe directly; keep another using the signal cache, and articulate the tradeoff.

**Exam Questions**
1. What does an Observable give you that a Promise doesn't?
2. Why does `HttpClient` return an Observable that completes after one emission?
3. What does `async` pipe do for you (subscription, unsubscription, change detection)?
4. When is a signal cache inside a service better than re-fetching on every render?
5. What's an HTTP interceptor and what's a good use case?

**Code Review Checklist**
- [ ] No subscription leaks (`takeUntilDestroyed` or `async` pipe).
- [ ] Loading and error UI is consistent across the app.
- [ ] Optimistic updates not used yet (covered later) — but state stays consistent after every request.
- [ ] `db.json` is committed and seeded with realistic-looking data.

---

### Chapter 10 — Testing (mid-course checkpoint)

> Goal: retrofit tests across what we've already built, understand the testing pyramid.

**Concepts**
- **Vitest with browser mode** — Angular's new default test runner (replaces Karma). Real browser environment, fast, modern. Jest is the well-known alternative and you should know it exists, but we use Vitest.
- `TestBed`, `ComponentFixture`, `DebugElement` — these are Angular concepts, runner-agnostic.
- Mocking `HttpClient` with `provideHttpClientTesting` and `HttpTestingController`.
- Marble testing (intro only).
- **Playwright** for end-to-end tests — modern, multi-browser, great DX.
- The testing pyramid — why most tests should be unit tests.

**Hands-on Tasks**
- [ ] Configure the Angular project to use **Vitest browser mode** as the test runner (`ng test` should run Vitest, not Karma).
- [ ] Write unit tests for `TransactionsService` (CRUD + computeds + HTTP mocked via `provideHttpClientTesting`).
- [ ] Write unit tests for `RelativeDatePipe`.
- [ ] Write a component test for `TransactionItemComponent` (render + click delete emits).
- [ ] Install and configure **Playwright**.
- [ ] Write one Playwright e2e test for the "add transaction" happy path.
- [ ] All tests run locally with `ng test` (Vitest) and `npx playwright test` (e2e). CI is optional follow-up.

**Exam Questions**
1. What's the testing pyramid? Why more unit tests than e2e?
2. What does `TestBed.configureTestingModule` actually do?
3. Why mock `HttpClient` in service tests? What would happen without mocking?
4. What does a `DebugElement` give you that querying the DOM directly doesn't?
5. What's a "test smell"? Give two examples.

**Code Review Checklist**
- [ ] Tests are independent — order doesn't matter.
- [ ] No tests that just assert what the framework does.
- [ ] Each test has a clear arrange / act / assert structure.
- [ ] Playwright e2e test runs against a known data state (seeded `db.json` or Playwright fixtures).

---

### Chapter 11 — Charts & Statistics

> Goal: build a visual stats dashboard reacting to live data.

**Concepts**
- Integrating a third-party library: types, providers, SSR caveats.
- `ng2-charts` (Chart.js wrapper) — installation, basic config.
- Driving chart data with `computed()` from service signals.
- Performance: avoiding unnecessary re-renders.
- Accessibility for charts (data tables as a fallback).

**Hands-on Tasks**
- [ ] Install and configure the chart library.
- [ ] Pie chart: expenses by category (current month).
- [ ] Bar chart: income vs expense over last 6 months.
- [ ] Line chart: balance over time.
- [ ] All charts react reactively when transactions change.
- [ ] Add a textual summary alongside each chart (a11y).

**Exam Questions**
1. Why drive chart data via `computed()` instead of a manual recompute method?
2. What's an example where a re-render of a chart would be visually janky and how would you mitigate?
3. Why is providing a data table alongside a chart important for accessibility?
4. What's the risk of installing a heavy 3rd-party library — list two costs.
5. How would you swap the chart library later with minimal damage?

**Code Review Checklist**
- [ ] No `any` types creeping in from the chart lib.
- [ ] Charts update without manual triggers when underlying data changes.
- [ ] Reasonable default colors that work with the app's design system.
- [ ] Accessible alternatives exist for every chart.

---

### Chapter 12 — Budgets, Recurring Transactions & Power Features

> Goal: build the "advanced" feature set — complex derived state and scheduled logic.

**Concepts**
- Multi-level `computed()` chains.
- Modeling recurring data (cron-ish: weekly, monthly).
- When `effect()` is genuinely the right tool (e.g., persistence triggers).
- File handling: CSV parse/generate.
- Defensive copies and immutability.

**Hands-on Tasks**
- [ ] Add monthly budget per category (uses the field added in chapter 8).
- [ ] Show progress bars per category with over/under indicators.
- [ ] Implement recurring transactions: a `RecurringTransaction` entity that materializes into real transactions when due.
- [ ] Add CSV export of transactions (download a `.csv` file).
- [ ] Add CSV import (paste/upload, validate, dedupe).
- [ ] Show alerts in the UI when a category is over budget for the current month.

**Exam Questions**
1. Why is a chain of `computed()` better than recomputing the same intermediate value in three places?
2. How would you decide between modeling recurring transactions as a separate entity vs. flags on a transaction?
3. What's the risk of mutating an object held inside a signal?
4. Why is CSV import a "trust nothing" boundary even for personal data?
5. When is `effect()` the right tool vs. when is it a hack?

**Code Review Checklist**
- [ ] No mutation of signal-held data; everything is replace.
- [ ] CSV import validates and gives clear errors.
- [ ] Recurring logic has no off-by-one errors at month boundaries.
- [ ] Performance acceptable with 1000+ transactions (try it).

---

### Chapter 13 — UI Library Integration (Angular Material)

> Goal: replace some custom UI with library components without losing the design.

**Concepts**
- Why use a component library at all (a11y, consistency, speed).
- Angular Material setup, theming.
- Standalone Material components.
- When to use library components vs. roll your own.
- CDK (Component Dev Kit) — overlays, a11y, drag/drop (preview).

**Hands-on Tasks**
- [ ] `ng add @angular/material`, pick a theme.
- [ ] Replace the date picker with `mat-datepicker`.
- [ ] Replace the category select with `mat-select`.
- [ ] Replace the snackbar/alert with `MatSnackBar`.
- [ ] Replace the delete confirmation with `MatDialog`.
- [ ] Ensure your custom design language still feels coherent (override theme variables if needed).

**Exam Questions**
1. What does Angular Material give you for free that handwritten components don't?
2. What's the difference between Material and the Angular CDK?
3. Why don't you just use Material for everything from day one?
4. How does Material theming work under the hood (very high level)?
5. What's a tradeoff of relying on a UI library — name a real cost.

**Code Review Checklist**
- [ ] No visual regressions vs. previous chapter.
- [ ] Material components blend with the rest of the design.
- [ ] No unused Material modules imported.
- [ ] All interactive elements remain keyboard-accessible after the switch.

---

### Chapter 14 — Real Public API & Production Concerns

> Goal: hit a real internet API, deal with real-world quirks.

**Concepts**
- CORS — what it is, why it bites.
- Environment files in Angular (`environment.ts`, `environment.prod.ts`).
- Secrets and why they never go in frontend code (and what to do instead).
- API keys, rate limits, exponential backoff.
- HTTP interceptors for auth/logging.
- Real-world error categories (network down, 4xx, 5xx, timeouts).

**Hands-on Tasks**
- [ ] Pick a real API (suggested: exchangerate-api.com to add multi-currency conversion).
- [ ] Add the API key to `environment.ts` (and `.gitignore` if it's a real key).
- [ ] Build an HTTP interceptor that attaches the key.
- [ ] Build a retry interceptor with exponential backoff.
- [ ] Handle network errors gracefully (offline detection, friendly messages).
- [ ] Add a currency converter widget that uses live rates.

**Exam Questions**
1. What is CORS in one sentence, and why is it the server's choice, not the client's?
2. Why is committing API keys to a public repo a bug, not a security feature?
3. When would you use an interceptor instead of doing the same in a service?
4. What's exponential backoff, and what bug does it prevent?
5. Name two ways a real network call can fail that a local mock will never simulate.

**Code Review Checklist**
- [ ] No real API keys in git history.
- [ ] All network calls have an error path that doesn't crash the UI.
- [ ] Interceptors are tested with mocked HTTP.
- [ ] App still works offline (graceful degradation), not silently broken.

---

### Chapter 15 — Portfolio Polish: Deploy, README, Interview Prep

> Goal: ship the app to a real URL, present it well, and prep for junior interviews.

**Concepts**
- SPA deployment basics, why client-side routing needs server config.
- Cloudflare Pages / Netlify / Vercel — what's free, what's not.
- Writing a portfolio-quality README.
- Junior Angular interview question patterns.

**Hands-on Tasks**
- [ ] Decide on a host (Cloudflare Pages recommended).
- [ ] Configure `_redirects` or `netlify.toml` so SPA routing works on refresh.
- [ ] Build for production: `ng build --configuration production`. Inspect bundle size.
- [ ] Deploy. Verify deep links work in production.
- [ ] Write a README that includes: 1-paragraph pitch, screenshots, live link, tech stack, "how to run locally", "what I learned", honest limitations.
- [ ] Record a 60–90 second screen recording demo and link it from the README.
- [ ] Write answers to 20 junior Angular interview questions in `INTERVIEW.md` (mentor will provide the question set or generate one with you).
- [ ] Do a mock interview: mentor asks 10 questions, you answer in writing, mentor grades.

**Exam Questions (final exam)**
The mentor selects 10 random questions from across **all previous chapters'** exam lists. You answer them in writing in one sitting, no peeking at the code or notes. Mentor grades and gives a final assessment.

**Code Review Checklist**
- [ ] Live URL works on mobile and desktop.
- [ ] Refreshing on any sub-route does not 404.
- [ ] README is professional — could be linked from a CV without embarrassment.
- [ ] Demo recording exists and is linked.
- [ ] All 20 interview answers are written in your own words.

---

## Verification (end-to-end)

A successful course completion means **all of the following are true**:

1. **It runs locally.** `git clone` → `npm install` → `npm run db` (in one terminal) → `ng serve` (in another) starts a working app reachable at `http://localhost:4200`.
2. **It runs on the internet.** A public URL works for the entire app on a fresh browser session.
3. **It's tested.** `ng test` (Vitest) passes. `npx playwright test` passes the happy-path test.
4. **It's documented.** README is portfolio-grade. ROADMAP.md in the repo shows every chapter's checkboxes ticked.
5. **You can talk about it.** You can answer any of the 20 interview questions in writing, and explain the architectural choices verbally to a friend.
6. **It's deployed via CI (stretch).** Optional GitHub Actions workflow that builds and deploys on push to main.

---

## Suggested daily rhythm (intensive, 20+ hrs/week)

- **Morning (2-3 hrs):** Read chapter concepts, ask mentor to explain unclear parts with examples.
- **Midday (3-4 hrs):** Implement hands-on tasks. Tick off as you go.
- **Afternoon (1-2 hrs):** Self-review using checklist; commit; push.
- **End of day (30 min):** Answer 1-2 exam questions in writing.
- **End of chapter:** Full code review + full exam grading session with mentor.

---

## Open items to revisit before chapter 1

These are intentionally deferred until you're closer to using them — don't pre-decide:

- Exact charting library (revisit at chapter 11).
- Exact UI library (revisit at chapter 13 — Material is the default).
- Real API choice (revisit at chapter 14).
- Test runner is locked: Vitest browser mode + Playwright. Jest is mentioned only for awareness of the ecosystem.
