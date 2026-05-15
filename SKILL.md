---
name: go-live
description: Use when the user is building, editing, or vibe-coding an app, website, prototype, or frontend and wants every change deployed to a public production or preview URL immediately so they can view it from a phone or remote device. Triggers on explicit "Go Live", "go live", "auto deploy", "deploy every change", "send me a deployed link", or similar requests for live public links after app/site changes.
---

# Go Live

## Operating Rule

Treat deployment as part of the implementation, not a separate follow-up. For every app or website change, ship a public URL the user can open immediately.

This skill exists for phone-first vibe coding: the user may not be able to inspect localhost, so a deployed link is the real preview.

## Workflow

1. Identify the app or website being edited and its existing deployment path.
2. Make the requested code/content/design change.
3. Run the fastest meaningful local check available for the stack, such as build, lint, typecheck, unit test, or smoke test.
4. Deploy the changed app to the public target.
5. Verify the deployed URL loads the changed experience.
6. Reply with the public link, what changed, and the verification result.

## Deployment Choice

Prefer the project's existing production or preview pipeline:

- Use existing npm scripts, deployment configs, CI/CD, Vercel, Netlify, Cloudflare, Firebase, GitHub Pages, or other project-specific setup when present.
- If the project is already linked to a provider, deploy through that provider instead of inventing a new path.
- If production deploys require commit/push, make a clean commit only when the user has asked for source control changes or the deployment pipeline requires it.
- If there is no persistent deployment configured, create the quickest public preview available in the environment and clearly label it as a temporary preview.

## Link Standard

The final response must include a public URL unless deployment is genuinely blocked.

When possible, include:

- Public URL
- Deployment provider or command used
- Build/check command result
- Short note confirming the changed screen or route was verified

If deployment fails, do not stop at "failed." Explain the blocker in plain language and give the next concrete recovery step, such as missing auth, missing project link, failed build, or provider outage.

## Cadence

For small requests, deploy once after the change is complete.

For larger requests, deploy after each coherent user-visible increment and at minimum before the final answer. Avoid leaving the user with only a localhost link unless they explicitly ask for local-only work.

## Guardrails

- Do not claim a deployment succeeded until the public URL has been checked.
- Do not expose secrets, API keys, private environment values, or private repo details in the deployed UI or final response.
- Do not overwrite an existing production project with unrelated work. If the repo has no clear deployment target and the deployment choice could affect a real production property, pause and ask which target to use.
- Keep the user moving: if the ideal production path is blocked, provide the fastest safe public preview alternative.
