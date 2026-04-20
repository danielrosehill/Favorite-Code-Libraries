---
description: Add one or more libraries (URLs, package names, or repo slugs) to README.md — classify into the right section, fetch a one-line description, and insert alphabetically.
argument-hint: <url | pkg-name | owner/repo> [more...]
---

# Add Library to Index

You are adding **$ARGUMENTS** to the Favorite Code Libraries index (`README.md` in the current repo).

## Procedure

For each input (URL, package name, or `owner/repo` slug):

1. **Resolve to a canonical GitHub repo URL.**
   - If a URL is given, use it directly.
   - If a package name is given (e.g. `edge-tts`, `jiwer`, `pdfplumber`), search to find the canonical GitHub repo. Prefer `gh search repos <name>` or a quick web fetch of the npm/PyPI page. Never guess the URL.
   - If it's a Python package, the PyPI page usually has the repo link; same for npm.

2. **Fetch the repo's one-line description.**
   - Use `gh repo view <owner>/<repo> --json description,primaryLanguage,topics` when possible.
   - If the description is vague, terse, or duplicates another entry, read the README (via `gh repo view <owner>/<repo>`) and write a one-liner that disambiguates: what it's for, what makes it good. Do not blindly paste the upstream description.

3. **Pick the right section.** Read the current `## Table of Contents` and existing sections to see what's available. Typical sections (alphabetical):
   - AI / LLM
   - Audio / Media
   - CLI & Tooling
   - JavaScript / TypeScript
   - Python
   - Speech / ASR

   Use the repo's `primaryLanguage`, topics, and purpose to decide. If none fit cleanly, **propose a new section** to Daniel before adding (don't create one silently). If two sections fit, pick the more specific one (e.g. `Speech / ASR` over `Python`).

4. **Pick the display name.** Use the human-readable project name (Title Case, spaces), not the hyphenated repo slug. E.g. `### Readability`, not `### readability`. The slug only appears in the badge URL.

5. **Insert alphabetically** within the chosen section, using this exact entry format:

   ```markdown
   ### {Display Name}

   {One-line description}

   [![View Repo](https://img.shields.io/badge/View-Repo-blue?style=flat&logo=github)](https://github.com/{owner}/{repo})
   ```

   If the section currently has the placeholder `<!-- Empty — ... -->` comment, replace the comment with the first entry.

6. **Check for duplicates** before inserting — if the repo URL already exists in the README, skip it and tell the user.

7. **Update `**Last Updated:**`** to the current month/year if it's stale.

8. **Commit and push** using the `commit-and-push` skill convention:
   ```
   git add -A
   git commit -m "Add {name}[, {name}...] to {section}"
   git push
   ```

## Hard rules (from the maintainer spec)

- Heading-based layout — one `###` per entry, one-line description, one View Repo badge. **No tables.**
- Sections alphabetical, entries within sections alphabetical by display name.
- Display name is human-readable with spaces; repo slug only in the badge URL.
- Descriptions should disambiguate, not blindly copy. Fetch the README if needed.
- No star counts or vanity badges.

## Report

After pushing, briefly report: what was added, to which section, and link to the updated README.
