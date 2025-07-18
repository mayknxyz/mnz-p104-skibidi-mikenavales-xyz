# Gen Alpha Slang Dictionary

A modern, educational, and fun web dictionary for Gen Alpha slang terms. This project aims to help parents, educators, and anyone curious about the latest internet and youth slang understand the language of the next generation.

---

## 🚀 Why This Project?

The **Gen Alpha Slang Dictionary** is more than just a list of words; it's a bridge between generations. As language evolves rapidly, especially with the influence of the internet, new terms can quickly become commonplace among younger demographics. This dictionary provides clear, concise explanations to demystify Gen Alpha lingo, fostering better understanding and communication.

### 💡 Project Goals (Beyond the Dictionary)

This project is intentionally built using a serverless tech stack, primarily for the purpose of learning and demonstrating proficiency with:

- **SvelteKit**: A powerful and efficient framework for building modern web interfaces.
- **Cloudflare Workers**: Edge computing for highly scalable and performant backend logic.
- **Cloudflare R2**: Cost-effective and globally distributed object storage for assets.
- **Cloudflare D1**: A serverless SQLite database for structured data management.

While some of these technologies might be considered "overkill" for a simple dictionary (e.g., Markdown files could suffice for data), the explicit goal here is to gain hands-on experience and explore the capabilities of this modern serverless ecosystem. This project also serves as a public repository for **open-source collaboration** and an **addition to a development portfolio**.

---

## ✨ Features

- **Comprehensive Slang Database**: Each term includes a definition, pronunciation, example usage, notes, and origin. All definitions are concise (200–300 characters) and written for clarity.
- **Blazing Fast Search**: Instantly search for terms, definitions, or aliases from the homepage, powered by Cloudflare D1.
- **Responsive UI**: Built with **SvelteKit** and **Tailwind CSS** for a clean, modern, and mobile-friendly experience.
- **Accessible and Educational**: Designed for parents, teachers, and curious minds to keep up with Gen Alpha lingo.
- **Open Source**: Easily contribute new terms or improvements. (Contribution guidelines coming soon!)
- **Scroll-to-top button**: A fun `💩` emoji button at the lower right that scrolls to the top of the page and auto-searches the term "skibidi".
- **Home Icon**: A `🏠` emoji icon at the upper right (hidden on the homepage) links to the homepage and matches the scroll-to-top icon in size and style.

---

## 🛠️ Tech Stack

- **Framework**: [SvelteKit](https://kit.svelte.dev/)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/), custom styles
- **Icons**: [Font Awesome](https://fontawesome.com/)
- **Fonts**: [Nunito (Google Fonts)](https://fonts.google.com/specimen/Nunito)
- **Database**: [Cloudflare D1](https://developers.cloudflare.com/d1/) (Serverless SQLite)
- **Object Storage**: [Cloudflare R2](https://developers.cloudflare.com/r2/)
- **Deployment & Backend**: [Cloudflare Workers](https://developers.cloudflare.com/workers/)

---

## 📂 Project Structure

```
.
├── src/
│   ├── lib/                  # Svelte components, utilities
│   ├── routes/               # SvelteKit pages and API endpoints
│   │   ├── +layout.svelte    # Global layout (header, footer)
│   │   ├── +page.svelte      # Homepage, search, and term display
│   │   └── api/              # Serverless API endpoints (e.g., for D1/R2 interaction)
│   ├── db/                   # Database schema and migration scripts for D1
│   ├── app.d.ts              # TypeScript type definitions for platform bindings
│   ├── app.html              # Main HTML template
│   └── app.css               # Global Tailwind CSS directives and custom styles
├── public/                   # Static assets (favicons, etc.)
├── svelte.config.js          # SvelteKit configuration
├── tailwind.config.js        # Tailwind CSS configuration (for JIT/build)
├── wrangler.jsonc            # Cloudflare Workers/Pages configuration (for D1/R2 bindings)
└── package.json              # Project dependencies and scripts
```

---

## 🚀 Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

- Node.js (LTS recommended)
- [Cloudflare `wrangler` CLI](<https://www.google.com/search?q=%5Bhttps://developers.cloudflare.com/workers/wrangler/install-update/%5D(https://developers.cloudflare.com/workers/wrangler/install-update/)>) installed and authenticated.

### Installation

1. **Clone the repo:**

   Bash

   ```
   git clone https://github.com/your-username/mnz-p104-skibidi-mikenavales-xyz.git
   cd mnz-p104-skibidi-mikenavales-xyz
   ```

2. **Install NPM packages:**

   Bash

   ```
   npm install
   ```

3. **Set up Cloudflare D1:**
   - Create your D1 database:
     Bash

     ```
     npx wrangler d1 create gen-alpha-slang-db
     ```

     - **Important**: Note down the `database_id` provided in the output.

   - Apply the database schema:
     Bash
     ```
     npx wrangler d1 execute gen-alpha-slang-db --remote --file=./src/db/schema.sql
     ```
     (The `schema.sql` file will be created in a later step.)
   - You might want to populate some initial data into your D1 database. (Instructions for this will be provided soon.)

4. **Set up Cloudflare R2 (if storing media):**
   - Create your R2 bucket:
     Bash
     ```
     npx wrangler r2 bucket create gen-alpha-slang-assets
     ```

5. **Configure `wrangler.jsonc`:**
   - Open `wrangler.jsonc` at the root of your project.
   - Update the `database_id` for the `DB` binding with the ID you got from step 3.1.
   - Ensure the `r2_buckets` section correctly points to `gen-alpha-slang-assets`. _(Example `wrangler.jsonc` structure will be shown in next steps when we create the file.)_

### Running Locally

You can develop locally using Cloudflare's Miniflare, which emulates the Cloudflare Workers environment, including D1 and R2 bindings.

Bash

```
npx wrangler pages dev .svelte-kit/cloudflare --d1 DB=gen-alpha-slang-db --r2 R2_BUCKET=gen-alpha-slang-assets --compatibility-date=2025-07-18 --binding ENV=development
```

This will start your SvelteKit app, connected to local D1 and R2 instances, usually at `http://localhost:8788`.

### Building for Production

Bash

```
npm run build
```

This command compiles your SvelteKit application into a Cloudflare Pages-compatible output in the `.svelte-kit/cloudflare` directory.

---

## 🤝 Contributing

We welcome contributions from everyone! Whether it's adding new slang terms, improving existing definitions, enhancing the UI, or optimizing the serverless functions, your help is appreciated.

To contribute:

1. **Fork** the repository.
2. **Create a new branch** for your feature or bug fix.
3. **Make your changes**.
4. **Commit your changes** with a clear and descriptive message.
5. **Push** your branch to your fork.
6. **Open a Pull Request** to the `main` branch of this repository.

Please ensure your code adheres to the existing style and that any new features are well-documented. More detailed contribution guidelines will be added soon!

---

## Roadmap

- Implement D1 for all slang term data storage and retrieval.
- Integrate R2 for pronunciation audio files.
- Refine search functionality and performance.
- Add a simple administrative interface for term management (optional, for trusted contributors).
- Improve accessibility features.
- Expand testing.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

## 📞 Contact

[@mayknxyz](https://github.com/mayknxyz)

Project Link: [https://github.com/mayknxyz/mayknxyz-mnz-p104-skibidi-mikenavales-xyz](https://github.com/mayknxyz/mayknxyz-mnz-p104-skibidi-mikenavales-xyz)
