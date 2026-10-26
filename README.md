# Ahmad Raza — Cloud Portfolio

My personal space for web projects, Linux notes and the things I’m learning on the way to cloud engineering.

The portfolio has a light theme, an animated cloud-and-laptop hero, a project reel and a private creator studio. This repo is a reusable version of the design, with the frontend and admin code in one place.

[View my portfolio](https://ahmad-raza-cloud-portfolio.glassybuddy32.chatgpt.site/)

## What’s included

- Responsive portfolio with about, projects, skills and contact sections.
- Reel and grid views, image/video uploads, and a pause-animation option.
- Owner-only project creation, editing, publishing and deletion.
- Drafts with protected media access.
- Optional likes and comments for accounts provisioned by the owner.
- TypeScript checks, security regression tests and GitHub Actions.

**Stack:** Next.js App Router, React, TypeScript, CSS, Supabase Auth, PostgreSQL and Storage.

The live site was built for the Sites runtime. This export keeps its interface and project workflow, while using standard Next.js and independent Supabase authentication so someone else can run their own copy. It contains no connection to my production database, accounts or uploads.

## Run it locally

Install Node.js 22.13 or newer, then run these commands inside the project folder:

```sh
npm ci
npm run dev
```

Open **http://localhost:3000**. The design runs without credentials and shows labelled sample projects. Sign-in and writes stay disabled until you set up your own backend.

For the admin panel, follow [the setup guide](docs/SETUP.md). A GitHub repository stores the source; the full app needs a Node.js host and a database. GitHub Pages alone cannot run this backend.

## Make it yours

Edit [`config/portfolio.ts`](config/portfolio.ts) for your name, introduction, education, links, skills and contact settings. Change `public/favicon.svg` if you want different initials in the browser tab.

Contact details are placeholders. Add your own public email and Formspree endpoint; message delivery is disabled by default. Add your real projects through `/admin` after backend setup.

## Project map

| Path | Purpose |
| --- | --- |
| `app/components/` | Portfolio sections, project cards and animation |
| `app/admin/` | Creator studio and its protected entry page |
| `app/sign-in/`, `app/sign-out/` | Account screens |
| `app/api/[...path]/route.ts` | Project, media, session and community API |
| `config/portfolio.ts` | Public profile and learning-stack settings |
| `lib/auth.ts` | Verified sessions and owner authorization |
| `lib/store.ts` | Server-side database and private media adapter |
| `supabase/schema.sql` | Empty database schema and private bucket |
| `.env.example` | Configuration names, without credentials |
| `tests/` | Access-control and request-validation checks |
| `.github/` | Automated checks and dependency update settings |

## Check your changes

```sh
npm run check
npm run build
```

Read [SECURITY.md](SECURITY.md) before deploying, and [the verification notes](docs/VERIFICATION.md) for what has and has not been tested. [FIRST-REPO.md](docs/FIRST-REPO.md) has a short Roman Urdu guide for uploading your first repository.

## License

The project code is available under the [MIT License](LICENSE). You can adapt it for your own portfolio; keep the license notice. Use your own name, links, accounts and project content. Third-party packages and brand marks retain their respective licenses and rights.
