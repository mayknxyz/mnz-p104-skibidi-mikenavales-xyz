# 🤝 Contributing to Gen Alpha Slang Dictionary

We're thrilled you're interested in contributing to the Gen Alpha Slang Dictionary! This project thrives on community involvement, and your contributions are highly valued. By contributing, you help us build a more comprehensive, accurate, and fun resource for understanding youth slang.

## 🌟 How Can You Contribute?

There are many ways to contribute to this project:

- **Suggesting New Slang Terms**: Know a term we're missing? Let us know!
- **Improving Existing Definitions**: Is a definition unclear, inaccurate, or could it be better? Help us refine it.
- **Reporting Bugs**: Found a glitch or something not working as expected? Please open an issue.
- **Suggesting Enhancements**: Have an idea for a new feature or an improvement to existing ones? We'd love to hear it.
- **Code Contributions**: Want to dive into the codebase? We welcome pull requests for bug fixes, new features, or performance improvements.

## 📝 Code of Conduct

Please note that this project is released with a [Contributor Code of Conduct](https://github.com/mayknxyz/mayknxyz-mnz-p104-skibidi-mikenavales-xyz/blob/main/CODE_OF_CONDUCT.md). By participating in this project, you agree to abide by its terms. We aim to foster an open and welcoming environment.

## 🚀 Getting Started with Code Contributions

If you're looking to contribute code, here's how to get your development environment set up.

### Prerequisites

- Node.js (LTS recommended)
- npm (as the package manager)
- [Cloudflare Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install-and-update/) installed and authenticated.

### Installation

1. **Clone the repository:**

   ```
   git clone https://github.com/your-username/mnz-p104-skibidi-mikenavales-xyz.git
   cd mnz-p104-skibidi-mikenavales-xyz
   ```

2. **Install NPM packages:**

   ```
   npm install
   ```

3. **Set up Cloudflare D1:**
   - Create your D1 database (if you haven't already):

     ```
     npx wrangler d1 create gen-alpha-slang-db
     ```

     - **Important**: Note down the `database_id` from the output.

   - Apply the database schema:
     ```
     npx wrangler d1 execute gen-alpha-slang-db --remote --file=./src/db/schema.sql
     ```
     (The `schema.sql` file will be part of the project's `src/db` directory.)
   - For local development, you might want to populate some initial data. You can use `npx wrangler d1 execute gen-alpha-slang-db --local --file=./src/db/seed.sql` (assuming you create a `seed.sql` file).

4. **Set up Cloudflare R2 (if working with media assets):**
   - Create your R2 bucket (if you haven't already):
     ```
     npx wrangler r2 bucket create gen-alpha-slang-assets
     ```

5. **Configure `wrangler.jsonc`:**
   - Open `wrangler.jsonc` at the root of your project.
   - Update the `database_id` for the `DB` binding with the ID you got from step 3.1.
   - Ensure the `r2_buckets` section correctly points to `gen-alpha-slang-assets`.

### Running Locally

```
npx wrangler pages dev .svelte-kit/cloudflare --d1 DB=gen-alpha-slang-db --r2 R2_BUCKET=gen-alpha-slang-assets --compatibility-date=2025-07-18 --binding ENV=development
```

This command starts your SvelteKit app, connected to local D1 and R2 instances, usually at `http://localhost:8788`.

## ✍️ Contribution Guidelines

### Branching Strategy

- All contributions should be made via a new branch created from `main`.
- Name your branch clearly, e.g., `feature/add-new-term-rizz` or `fix/search-bug`.

### Commit Messages

- Write clear, concise, and descriptive commit messages.
- Use the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/ 'null') specification (e.g., `feat:` Add `scroll-to-top button`, `fix: Correct definition for 'skibidi'`).

### Pull Request Process

1. Ensure your code builds and runs locally without errors.
2. Push your branch to your forked repository.
3. Open a Pull Request (PR) against the `main` branch of `mnz-p104-skibidi-mikenavales-xyz`.
4. In your PR description, clearly explain:
   - What problem your PR solves.
   - How you solved it.
   - Any relevant screenshots or GIFs for UI changes.
   - Any specific areas you'd like feedback on.

5. Be responsive to feedback and be prepared to iterate on your changes.

### Code Style

- We use Prettier and ESLint to maintain consistent code style. Please ensure your code is formatted correctly before submitting a PR. You can run `npm run format` (if configured) or ensure your editor integrates with Prettier/ESLint.

## 📚 Adding or Editing Slang Terms (Data Contribution)

Since we're using Cloudflare D1 for data storage, direct Markdown file contributions for terms will no longer be the primary method. Instead, you can:

1. **Open an Issue**: The easiest way to contribute new terms or suggest edits is to open a new issue on the GitHub repository. Please use the "New Slang Term Suggestion" or "Definition Improvement" issue templates (if available) and provide all relevant details (term, definition, pronunciation, example usage, notes, origin).
2. **Direct Database Contribution (Advanced)**: For those comfortable with SQL or programmatic data insertion, you could potentially contribute a SQL migration file (`.sql`) to `src/db/migrations/` with `INSERT` or `UPDATE` statements. Please discuss this in an issue first to ensure it aligns with the project's migration strategy.

## ⚖️ License

By contributing to the Gen Alpha Slang Dictionary, you agree that your contributions will be licensed under the MIT License, as per the project's [LICENSE](https://github.com/mayknxyz/mayknxyz-mnz-p104-skibidi-mikenavales-xyz/blob/main/LICENSE) file.

Thank you for helping us build this awesome resource!
