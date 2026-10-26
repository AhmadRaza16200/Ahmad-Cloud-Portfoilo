# Security

This public repository contains application code and an empty database schema. It does not contain the original site's credentials, account IDs, database records, messages, uploaded media, deployment configuration or Git history.

## Access model

The portfolio is public. A visitor can see the login screen, but project writes and uploads require a server-verified session whose user UUID exactly matches `ADMIN_USER_ID`. Authentication alone is not admin authorization. Caller-supplied identity headers and profile metadata never grant ownership.

Supabase verifies access tokens through `auth.getUser`. Owner checks are applied to API mutations and the admin page. Secrets are in server-only modules; no `NEXT_PUBLIC_*` secret is required. Unsafe/missing origins are rejected for writes, input is validated, request bodies are bounded, and user text is rendered through React.

Tables have RLS enabled and grants revoked from `anon` and `authenticated`. The service-role key bypasses RLS and is therefore confined to the server. Use a dedicated Supabase project. Do not add broad RLS policies or make the media bucket public.

Anonymous media requests need a matching published project. Draft and detached uploads require owner access, including when a filename is known. Media responses are not shared-cacheable. Content that was already publicly downloaded cannot be recalled by unpublishing it.

## Before making a repository public

- Keep `.env.local`, credentials, logs, uploads, database dumps and hosting state out of Git.
- Run `npm run check:public` and inspect `git diff --cached` before committing.
- Enable GitHub secret scanning/push protection where available. The included scanner is only a supplementary pattern check.
- Use a new repository history for this export. `.gitignore` does not remove secrets from old commits.
- If a real secret is ever committed, revoke/rotate it first, then remove it from history. Deleting its current file is insufficient.
- Keep framework/dependency updates current and review Dependabot pull requests.

## Operational limits

The tests use fake authentication responses and isolated in-memory records. They check application authorization behavior; they do not certify a hosting provider, a live Supabase configuration, all dependencies, or the original live website. No software is guaranteed invulnerable.

There is no automatic session refresh, public signup, password-recovery UI, MFA setup, distributed rate limiter, database backup job or orphan-media cleanup job. Account recovery can be managed through your Supabase admin account. Protect that account and your hosting/GitHub accounts with their available account security controls.

The public feed returns at most 100 projects and each discussion at most 100 comments. Views are browser-cookie counts, not verified visitor analytics. Comments have a basic cooldown; it is not a transactional anti-spam guarantee.

## Reporting a problem

Use GitHub's private vulnerability reporting if the repository owner has enabled it. Otherwise contact the owner through the public portfolio. Do not post credentials or exploit details in a public issue.
