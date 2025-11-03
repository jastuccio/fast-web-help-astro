#  Git Workflow

This project follows a disciplined, PR-based workflow that prioritizes a clean, linear, and well-documented `main` branch.

---

## 📂 Branching Strategy
-   **`main`** → 🟢 Always stable, deployable, production-ready.
-   **`feature/`** → ✨ For new features (e.g., `feature/contact-form`).
-   **`fix/`** → 🐞 For bug fixes (e.g., `fix/header-layout`).
-   **`chore/`** → ⚙️ For tooling, config, or build changes (e.g., `chore/update-biome`).
-   **`docs/`** → 📖 For documentation-only changes (e.g., `docs/readme-setup`).

**Rule:** Branches should be small, focused, and short-lived.

---

## 📝 Commit Standards

All commits on feature branches must follow the **Conventional Commits** standard.

**Format:**
`<type>(<scope>): <summary>`

**Allowed Types:**
-   ✨ `feat` → A new feature for the user.
-   🐞 `fix` → A bug fix for the user.
-   ⚙️ `chore` → Build system, tooling, configs, or other non-user-facing changes.
-   📖 `docs` → Documentation-only changes.
-   🔄 `refactor` → Code changes that neither add a feature nor fix a bug.
-   🧪 `test` → Adding or updating tests.

**Examples:**
-   `feat(contact): build basic contact form component`
-   `fix(nav): correct z-index on mobile menu`
-   `chore(biome): enable Astro experimental linting`
-   `docs(readme): add git workflow section`

---

## 🔀 Merging (Pull Requests)

All code must enter the `main` branch through a Pull Request (PR). This is true even for solo development, as it provides a crucial documentation trail and a consistent merge process.

1.  **Push Your Branch:**
    ```fish
    # From your feature branch
    git push -u origin <branch-name>
    ```

2.  **Open a Pull Request:**
    -   In GitHub, open a PR from your branch to `main`.
    -   The PR title should be the final, clean commit message (e.g., `feat(contact): add contact form and lead capture`).
    -   The PR description should summarize *why* the change was made and any other relevant context.

3.  **Merge the PR:**
    -   Once all checks (CI, Netlify deploy preview) have passed, merge the PR using the **"Squash and Merge"** button.
    -   **This is mandatory.** It condenses all "WIP" and "fixup" commits from your branch into the single, well-written commit message from your PR title. This keeps the `main` branch history pristine.

4.  **Clean Up:**
    -   Allow GitHub to automatically delete the branch after merging.

---

## 🏷️ Release & Tagging

Releases are managed using the "Releases" feature in the GitHub UI, which creates the official Git tag for you.

1.  **Navigate to "Releases":** In your GitHub repo, go to the "Releases" tab (on the right-hand sidebar).
2.  **Draft a New Release:** Click "Draft a new release."
3.  **Create a New Tag:** In the "Choose a tag" dropdown, type your new version number (e.g., `v1.0.0`) and click "Create new tag: ... on publish."
4.  **Set the Title:** Make the release title the same as the tag (e.g., `v1.0.0`).
5.  **Write Release Notes:** Write your changelog here. You can summarize the major features and fixes that this version includes.
6.  **Publish:** Click "Publish release." This will create the release and the `v1.0.0` Git tag automatically.

---

## 📦 Versioning

-   **Semantic Versioning:** We follow `MAJOR.MINOR.PATCH` (e.g., `v1.2.1`).
-   **`v1.0.0`** → Stable, public release.