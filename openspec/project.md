# Project Context

## Purpose
The purpose of this project is to build a modern, fast, and accessible website for "fast-web-help".

**Key Goals:**
- **Goal 1:** Create a website to help me find freelance web dev and programming work
- **Goal 2:** migrate existing content from openspec/migrated-content.md to the correct pages and components in this new Astro site
- **Goal 3:** generate leads through a contact form

**Target Audience:** potential clients

## Tech Stack
This project is built with the Astro framework.

- **Framework:** Astro
- **Language:** TypeScript
- **UI Components:** Astro components (Svelte in Astro if useful)
- **Styling:** Pure CSS	- Astro's Scoped Styles & Open Props(https://github.com/argyleink/open-props)
- **Deployment:** Netlify
- **Package Manager:**  pnpm

## Project Conventions

### Code Style
**Primary Toolchain:**
- **Tool:** Biome
- This single, high-performance tool replaces the previous stack (Prettier + ESLint) for all code quality checks.
- All configuration is centralized in the root `biome.json` file.

**Linting & Formatting:**
- **Tool:** Biome (handles both formatting and linting).
- **Triggers:** Run on save (via the Biome IDE extension) and as a pre-commit hook.
- **Scope:** Enforces rules for code correctness, style, import sorting, and formatting across the entire codebase. This includes:
  - **Stable:** JavaScript, TypeScript, JSX, JSON, CSS, HTML
  - **Experimental:** Astro, Svelte, Vue, and MDX files.

**Naming Conventions (Enforced by Biome Linter):**
- **Components:** `PascalCase.astro` (e.g., `Header.astro`)
- **Variables/Functions:** `camelCase`
- **Types/Interfaces:** `PascalCase`

### Architecture Patterns
This project follows the standard Astro project structure.

- **Directory Structure:**
  - `src/pages/`: Contains all pages and routes.
  - `src/layouts/`: Contains layout components for pages.
  - `src/components/`: Contains reusable UI components.
  - `src/content/`: for storing content collections (like Markdown, MDX, or JSON).
      - create a `src/content/config.ts` file to define a "schema" for your content (e.g., title: z.string(), pubDate: z.date() )
  - `src/styles/`: Contains global styles.

- **Data Fetching:**
  - **Server-Side (Build-Time):** Data needed to render a page will be fetched using `top-level await` in the frontmatter of `.astro` components. This is the default method for fetching content (e.g., from `src/content/` or a headless CMS).
  - **Client-Side (Runtime):** Data needed *after* the page loads (e.g., for interactive form states, or live-updating data) will be fetched in a client-side script or a UI framework component (like Svelte) hydrated with a `client:` directive.

### Testing Strategy
We follow a "Testing Pyramid" approach, prioritizing E2E tests for critical user flows and component tests for interactive islands.

**End-to-End (E2E) Testing:** Playwright
  - **Requirement:** New or modified **critical user flows** must have a corresponding E2E test. (e.g., contact form submission, main navigation).

- **Component/Unit Testing:** Vitest + Testing Library
  - **Requirement:** Any **interactive component** (e.g., Svelte, React, or Vue components hydrated with `client:`) must have component tests to verify its behavior in isolation.
  - **Scope:** Purely static `.astro` components (components without logic) do not require unit tests.

### Git Workflow
This project follows a disciplined, PR-based workflow.

**The full specification for branching, commits, and merging is defined in: `openspec/specs/git-workflow.md`**

## Domain Context
<!--
This section is for any special terms or business logic. For example, if you were building an e-commerce site, you might add: 
- **SKU (Stock Keeping Unit):** A unique identifier for each product.
- **"Above the fold":** Content visible on the screen without scrolling.
-->

## Important Constraints
- Performance: Lighthouse scores must be above 90 for Performance, Accessibility, Best Practices, and SEO.
- Browser Support: The site must work correctly on the latest versions of Chrome, Firefox, and Safari.
  - Accessibility (A11y): The site must be fully navigable and readable via keyboard-only and screen reader (e.g., VoiceOver, NVDA).
  - Rule: All interactive elements (links, buttons, forms) must have clear and visible focus states.
  - Rule: All content images must have descriptive alt text.
  - JavaScript Footprint: The site must adhere to the "zero-JS by default" Astro philosophy.
  - Rule: JavaScript must only be shipped to the client for interactive components (e.g., the contact form, mobile nav) using Astro's client: directives.
  - Data Privacy & Security: The site must protect user data and prevent spam.
  - Rule: A clear, easy-to-find Privacy Policy must be present, stating what data is collected and how it will be used.
  - Rule: The contact form must be protected from spam using a non-intrusive method (e.g., a honeypot field or Cloudflare Turnstile).
  - Budget: The project prioritizes free-tier services. Paid solutions may be proposed if they offer a compelling return on investment, but the proposal must include a cost-benefit analysis to justify the expense.

## External Dependencies
*[List any third-party systems your project interacts with.]*

-   **Analytics:** None.
    -   **Reason:** To maximize performance (Lighthouse > 90) and ensure user privacy, this site will not use any client-side analytics scripts (like Google Analytics). Basic, non-invasive traffic data (e.g., bandwidth, page views) will be monitored via the Netlify dashboard.

-   **CMS:** Astro Content Collections.
    -   **Reason:** All content (including migrated blog posts and page content) will be stored as local Markdown/MDX files in the `src/content/` directory. This is the most performant, "Astro-native" method. It requires no external API calls, is version-controlled with Git, and provides full type-safety.

-   **Form Handling:** Netlify Forms.
    -   **Reason:** Since the site is deployed on Netlify, we will use Netlify's built-in form handling for the contact form. This requires zero serverless functions, no API keys, and is free. It also includes spam protection (honeypot field) out of the box.
