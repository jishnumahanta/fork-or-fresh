# Fork or fresh?

An [Agent Skill](https://agentskills.io) that stops your coding agent from rebuilding things that already exist.

<p align="center">
  <a href="https://github.com/jishnumahanta/fork-or-fresh/raw/main/assets/fork-or-fresh.mp4">
    <img src="assets/demo.gif" alt="Search GitHub, compare the top three by license, last commit and stars, then fork or build fresh" width="480">
  </a>
  <br>
  <sub>▶ <a href="https://github.com/jishnumahanta/fork-or-fresh/raw/main/assets/fork-or-fresh.mp4">Watch the full 33-second video (with sound)</a></sub>
</p>

Before it builds something new, the agent searches GitHub for open-source projects that already do the job,
compares the top 3 by **license**, **last commit** and **stars**, and asks you one question:

> **Fork one, or build fresh?**

Often the thing already exists, it's maintained, and the license lets you use it. You start from code other people
have already debugged, and you build from scratch only the part that's actually new.

## Install

### Claude Code (plugin)

```
/plugin marketplace add jishnumahanta/fork-or-fresh
/plugin install fork-or-fresh@fork-or-fresh
```

### Codex, Cursor, OpenCode and other agents that support Agent Skills

With the [Skills CLI](https://github.com/vercel-labs/skills):

```
npx skills add jishnumahanta/fork-or-fresh
```

It installs into the current project; add `-g` to make it available in all your projects. Add `-a <agent>` (for example `-a codex`) to pick one agent.

### Manual

Copy `skills/fork-or-fresh/` into your agent's skills folder, for example `~/.claude/skills/fork-or-fresh/` for
Claude Code.

## Use it

Just ask for something new:

```
build me a clipboard manager for macOS
```

The agent searches first and replies with something like:

| Repo | License | Last commit | Stars | Fits? |
|---|---|---|---|---|
| p0deje/Maccy | MIT | 3 days ago | 22.1k | Yes: native, fast, maintained |
| Slackadays/Clipboard | GPL-3.0 | May 2026 | 5.9k | Terminal tool, not a menu-bar app |
| yuzeguitarist/Deck | Other | 5 days ago | 1.5k | Check the license first |

**Recommendation:** fork Maccy (MIT, active) and add only the feature you need. Fork one, or build fresh?

It skips the search for small changes inside your own codebase, learning exercises, or when you say
"build it from scratch".

It works best with the [GitHub CLI](https://cli.github.com) (`gh`) logged in. Without it, the agent falls back to
GitHub's public search API.

## Licenses, in one line each

- **MIT / Apache-2.0 / BSD / ISC:** reuse freely, keep the license and copyright notice.
- **GPL / AGPL:** fine for open source; your changes must be shared under the same license.
- **No license:** you can't legally reuse it.

This is not legal advice; read the project's LICENSE.

## Made by

**Jishnu Mahanta**, full-stack, IoT and AI engineer from Assam, India.

[Website](https://www.jishnumahanta.in) ·
[GitHub](https://github.com/jishnumahanta) ·
[X](https://x.com/jishnumahanta17) ·
[LinkedIn](https://www.linkedin.com/in/jishnumahanta) ·
[Threads](https://www.threads.com/@mahantajishnu) ·
[Instagram](https://www.instagram.com/jishnubuilds/)

If this saves you a weekend, a ⭐ helps other people find it.

## License

MIT © [Jishnu Mahanta](https://www.jishnumahanta.in)
