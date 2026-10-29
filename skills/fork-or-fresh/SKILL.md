---
name: fork-or-fresh
description: Before building a new app, tool, library, CLI, plugin or feature from scratch, search GitHub for existing open-source projects that already do the job, compare the top 3 by license, last commit and stars, and recommend whether to fork/reuse one or build fresh. Use when the user asks to build, create, make or write something new ("build me a…", "create a…", "I want a tool that…"), or asks whether something already exists.
license: MIT
metadata:
  author: Jishnu Mahanta (github.com/jishnumahanta)
  version: "1.0.0"
---

# Fork or fresh?

Most things people ask an agent to build already exist, are maintained, and have a license that allows reuse.
Check first. Starting from code other people have already debugged saves days.

## When to run this

Run it **before writing any code** when the user asks for something new and self-contained: an app, CLI, library,
service, plugin, bot, script with a clear purpose, or a big feature that could be its own package.

Skip it (or say in one line why you skipped) when:
- the user says to build it from scratch, or it is a learning exercise;
- the change is inside their existing codebase and is small (a bug fix, a refactor, a single function);
- it is private glue code that only makes sense for their project.

## Steps

1. **Name the job in 2–4 keywords.** e.g. "build me a clipboard manager for macOS" → `clipboard manager macos`.
   Also think of 1–2 synonyms (`pasteboard`, `clipboard history`).

2. **Search GitHub.** Prefer the GitHub CLI if it is installed and logged in:

   ```bash
   gh search repos clipboard manager macos --sort stars --limit 10 \
     --json fullName,description,stargazersCount,pushedAt,license,isArchived,url
   ```

   - Pass keywords as **separate words**. Quoting the whole query makes it an exact-phrase search and hides the best
     projects.
   - No `gh`? Use the public API: `curl -s "https://api.github.com/search/repositories?q=clipboard+manager+macos&sort=stars&per_page=10"`
     (unauthenticated calls are rate-limited, so keep it to one or two queries), or a web search with `site:github.com`.
   - If the top results are off-topic, retry once with the synonyms.

3. **Shortlist the top 3** that really do the job (read the descriptions; skip archived repos, forks and empty ones).

4. **Compare them in a table:**

   | Repo | License | Last commit | Stars | Fits? |
   |---|---|---|---|---|

   - **License:** MIT, Apache-2.0, BSD and ISC allow reuse in closed or commercial work. GPL/AGPL require sharing your
     changes under the same license (fine for open source, a problem for closed products). No license means you
     can't legally reuse it. Say this plainly for each one.
   - **Last commit:** within ~6 months = maintained; older than ~2 years = likely abandoned.
   - **Stars:** a rough signal of use, not quality.
   - **Fits?:** platform, language and the user's must-have features.

5. **Ask the one question, with your recommendation:** *Fork one, use it as a dependency, or build fresh?*
   - **Fork / reuse** when a project is maintained, has a compatible license and covers most of the job.
   - **Build fresh** only when nothing fits (wrong platform, dead project, incompatible license, or the core idea is
     genuinely new). Then build only the part that is actually new and borrow the rest.

6. **Wait for the user's choice** before writing code. If they fork, follow the project's license (keep its LICENSE
   and copyright notices).

## Example output

> Before building, I checked GitHub for existing clipboard managers for macOS:
>
> | Repo | License | Last commit | Stars | Fits? |
> |---|---|---|---|---|
> | p0deje/Maccy | MIT | 3 days ago | 22.1k | Yes: native, fast, maintained |
> | Slackadays/Clipboard | GPL-3.0 | May 2026 | 5.9k | Terminal tool, not a menu-bar app |
> | yuzeguitarist/Deck | Other | 5 days ago | 1.5k | Check the license first |
>
> **Recommendation:** fork Maccy (MIT, active) and add only the feature you need.
> Fork one, or build fresh?

Never claim a number you didn't read from the search results. If the search fails, say so and ask the user how to
proceed instead of guessing.
