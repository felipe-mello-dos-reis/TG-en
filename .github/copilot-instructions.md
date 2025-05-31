# COPILOT EDITS OPERATIONAL GUIDELINES

**Audience:** All Technology Teams

---

## 1. Prime Directive

1. **Single‑File Focus**: Always work on **one file** at a time to avoid merge conflicts or corruption.
2. **Transparent Communication**: Narrate your approach in real time—explain your rationale, steps, and any trade‑offs as you code.

---

## 2. Large File & Complex Change Protocol

### 2.1 Planning Phase (Mandatory)

For any file exceeding **300 lines** or requiring **multi‑step changes**:

1. **Draft a Detailed Plan** *before* starting edits.
2. **Plan Contents**:

   * **Scope**: List functions, classes, or sections to change.
   * **Sequence & Dependencies**: Define the order and dependencies among edits.
   * **Effort Estimate**: Count discrete edits expected.
3. **Plan Template**:

   ```markdown
   ## PROPOSED EDIT PLAN
   **File:** `<filename>`  
   **Total Edits:** `<n>`  
   1. `<Change 1>` — _Purpose:_ `<why>`  
   2. `<Change 2>` — _Purpose:_ `<why>`  
   …
   ```

### 2.2 Execution Phase

* **One Edit at a Time**: Implement each change sequentially.
* **Before & After**: Present concise diff snippets with brief explanations.
* **Style & Standards**: Verify each change adheres to the project's style guide and lint rules.
* **Progress Logging**: After every edit, log:

  > ✅ Completed edit `[i]` of `[total]`. Ready for the next?
* **Plan Revisions**: If new requirements emerge, pause, update the plan, and obtain approval.

### 2.3 Refactoring Best Practices

* Break refactoring into **self‑contained** steps that maintain build/pass tests at each stage.
* Use **intermediate duplication** to minimize risk and simplify rollback.
* Document the **refactoring pattern** applied (e.g., Extract Method, Rename Class).

### 2.4 Session Management

* For very large changes, propose splitting work into **multiple sessions**.
* Define clear **stopping points** aligned with functional deliverables.

---

## 3. General Code Quality

* Emphasize **readability**, **maintainability**, and **scalability**.
* Write **self‑documenting code**; use meaningful names and concise comments only where necessary.

---

## 4. Accessibility & Inclusivity

* Comply with **WCAG 2.1 AA** (aim for AAA when feasible).
* Always include:

  * Proper `<label>`s for form fields
  * Accurate **ARIA** roles and attributes
  * High contrast and **dark‑mode** support via `prefers-color-scheme`
  * `alt` text / `aria-label` for non‑text content
  * Semantic HTML hierarchy
* Recommend periodic **Lighthouse** or equivalent accessibility audits.

---

## 5. Browser Compatibility & Progressive Enhancement

* Use **feature detection** (e.g., `if ('fetch' in window)`).
* Support the **latest two** stable releases of **Chrome, Firefox, Edge, Safari**.
* Apply **polyfills** or **transpilation** via **Babel**/**Vite** as needed.

---

## 6. PHP Guidelines (v8.1+)

* **Language Features**: Named arguments, constructor promotion, union types, `match`, nullsafe (`?->`), attributes, `enum`, readonly props, strict typing.
* **Standards**: PSR‑12, `declare(strict_types=1);`, dependency injection, favor composition.
* **Documentation & Analysis**: PHPDoc blocks for PHPStan/Psalm.
* **Error Handling**: Throw curated exceptions; avoid suppressing errors; use clear messaging.

---

## 7. HTML & CSS Standards

### 7.1 HTML5 Best Practices

* Use semantic elements: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`.
* Ensure valid markup (W3C), SEO meta tags (`<title>`, `<meta description>`, Open Graph).
* Responsive images: `srcset`, `sizes`, `loading="lazy"`, modern formats (WebP/AVIF).

### 7.2 Modern CSS

* Layout: CSS Grid & Flexbox.
* Adopt CSS Custom Properties, logical properties (`margin-inline`).
* Use modern selectors (`:is()`, `:where()`, `:has()`) and **BEM** naming.
* Include **dark mode** and responsive media queries.

---

## 8. JavaScript (ES2020+)

* **Syntax**: Arrow funcs, template literals, destructuring, spread/rest, classes, modules (ESM).
* **Async**: `async/await`, `Promise.allSettled()`, avoid callback hell.
* **Features**: Optional chaining (`?.`), nullish coalescing (`??`), dynamic imports, BigInt, `globalThis`, `matchAll`, private fields.
* **Error Handling**:

  * Distinguish network vs business vs runtime errors.
  * Provide user‑friendly messages; log technical details separately.
  * Implement a global handler for unhandled rejections.
* **Optimization**: Code‑split and lazy‑load modules when appropriate.

---

## 9. Python Guidelines (3.10+)

* **Compatibility**: Python 3.10+; leverage `match-case` for pattern matching.
* **Type System**: Enforce type hints (`Optional`, `Union`, `Literal`, `TypedDict`); adopt PEP 695 in 3.12+.
* **Data Modeling**: Use `@dataclass(frozen=True)` and `Enum`/`IntEnum` for clear, immutable models.
* **Clean Syntax**: f‑strings, comprehensions, `with` context managers, `contextlib.contextmanager`.
* **Error Strategy**:

  * Structured `try-except-else-finally`; catch specific exceptions.
  * Raise descriptive exceptions; document with `:raises:`.
  * Use `logging` (no `print()` in production).
* **Quality Tools**: PEP 8 + `black`, `isort`, `flake8`/`ruff`; docstrings per PEP 257.
* **Testing**: **pytest** + fixtures + `unittest.mock`; target ≥90% coverage; include test plans.
* **Dependency Management**: **Poetry** and **UV** for virtual environments and package management; maintain `pyproject.toml` with pinned versions.
* **Concurrency**: `asyncio` for I/O; `concurrent.futures`/`multiprocessing` for CPU; document async APIs; use locks/semaphores.
* **Performance**: Profile (cProfile/line\_profiler) before optimizing; favor readability; use generators/lazy evaluation.
* **Packaging**: Standard layout (`src/`, `tests/`, `pyproject.toml`); automation via Makefile/Invoke.
* **Security**: No hardcoded secrets; use `.env` or secret managers; sanitize inputs; validate with `pydantic`; run **bandit** in CI.
* **Documentation**: Sphinx + autodoc; usage examples in README; maintain CHANGELOG.
* **Pre-commit**: `black`, `flake8`, `isort`, `mypy`.

---

## 10. Repository Structure

```plaintext
project-root/
├── api/         # Handlers & routes
├── config/      # Env vars & configs
├── data/        # DBs & fixtures
├── public/      # Static assets
│   ├── assets/
│   │   ├── css/
│   │   ├── js/
│   │   ├── images/
│   │   └── fonts/
│   └── index.html
├── src/         # Core application code
│   ├── controllers/
│   ├── models/
│   ├── views/
│   └── utils/
├── tests/       # Unit & integration tests
├── docs/        # Documentation
├── logs/        # Log outputs
├── scripts/     # Deployment & maintenance
└── temp/        # Cache & temp files
```

---

## 11. API & DB Documentation

* **JavaScript/TypeScript**: JSDoc (`@param`, `@returns`, `@throws`, `@author`).
* **Databases (SQLite 3.46+)**: Use JSON columns, generated columns, strict mode, foreign keys, check constraints, and transactions.

---

## 12. Security & Compliance

* Sanitize all inputs; parameterize queries.
* Enforce CSP & CSRF protection.
* Secure cookies (`HttpOnly`, `Secure`, `SameSite=Strict`).
* Role‑based access control.
* Centralized logging & real‑time monitoring.

---
