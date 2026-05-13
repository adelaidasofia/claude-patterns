# claude-patterns

A Claude Code plugin that scans recent sessions, journal entries, and decisions for recurring patterns — then turns them into concrete captures: CLAUDE.md rules, concept notes, writing seeds, skill improvements.

The Instinct Engine. It catches what's hardening into real insight before it evaporates.

---

## What it does

You run `/patterns` and Claude:

1. Pulls in your last session, last 10-15 decisions, recent drafts, and last 7 journal entries
2. Scans for recurring themes, repeating decision logic, recurring metaphors, behavioral loops, and vault gaps
3. Surfaces up to 5 specific findings, with the actual quotes and the proposed capture
4. After you confirm, writes the rules, drafts, concept notes, or skill notes in one pass
5. Logs the run

It also runs semi-autonomously: at the end of every session, Claude can silently check four auto-detection triggers (tool-call friction, corrections, dead-end recovery, non-trivial discoveries) and surface a one-line suggestion if any fire.

The point is to make implicit pattern recognition explicit — and to capture the pattern in a place the next session can see, not in your head where the next session can't.

---

## Install

Open Claude Code, paste:

    /plugin marketplace add adelaidasofia/claude-patterns
    /plugin install claude-patterns@claude-patterns

Then in any Claude Code session:

```
/patterns
```

On first use, Claude asks where your sessions, decisions, journals, drafts, and concept notes live. Takes 60 seconds, never asks again.

<details><summary>Legacy install</summary>

```bash
claude plugin add github.com/adelaidasofia/claude-patterns
```

</details>

---

## Requirements

- Claude Code
- A vault or notes folder with at least one of: a last-session file, a decision log, a journal, a drafts folder
- Nothing else

**Optional integrations:**
- The daily-journal plugin — `/patterns` reads the last 7 entries automatically if your journal lives in the path you configured
- The insights plugin — if a weekly review was just run, `/patterns` uses that output instead of re-scanning journals

---

## What gets captured

**Writing seed** → a draft with the exact phrasing + context of where the pattern appeared. The most original material is usually the metaphor that resurfaced three times across two months without you noticing.

**CLAUDE.md rule** → a new rule added to the relevant section. Decision frameworks that repeat ("when X, I always do Y because Z") become rules so the next session doesn't re-derive them.

**Concept note** → for ideas that keep appearing in passing but never got their own page.

**Skill improvement** → flagged for the next skill update. If a workflow keeps requiring manual steps, the workflow itself needs to change.

---

## The four auto-detection triggers

At session end, Claude silently checks for:

1. **High tool-call friction** — 5+ steps for something routine? Missing shortcut or rule.
2. **User correction** — you said "no, not that way"? Worth checking if this echoes prior corrections.
3. **Dead-end recovery** — Claude backtracked before finding the working path? Preserve the working path.
4. **Non-trivial discovery** — found something non-obvious about a tool, API, or workflow? May warrant a rule.

If any fire, Claude offers a one-line prompt — never a wall of text. You can say "yes" (run full /patterns), "just save it" (capture the specific finding), or "no" (skip).

The full scan never auto-runs. Only suggestions.

---

## How this differs from the insights plugin

- **insights** is periodic review (weekly, monthly). It looks at floor trends, behavioral patterns, and panel commentary across a defined time window.
- **patterns** is signal extraction. It looks at what's repeating across the most recent ~2 weeks and proposes concrete captures.

Use insights for "how was this week." Use patterns for "what's hardening into something I should write down."

---

## Submitting to the Cowork marketplace

Once the repo is on GitHub, submit at: **[clau.de/plugin-directory-submission](https://clau.de/plugin-directory-submission)**

For the community marketplace:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
```

---


## Telemetry

This plugin sends a single anonymous install signal to `myceliumai.co` the first time it loads in a Claude Code session on a given machine.

**What is sent:**
- Plugin name (e.g. `slack-mcp`)
- Plugin version (e.g. `0.1.0`)

**What is NOT sent:**
- No user identifiers, names, emails, tokens, or API keys
- No file paths, message content, or anything from your work
- No IP address is stored after dedup processing

**Why:** Helps the maintainer know which plugins people actually install, so attention goes to the ones that get used.

**Opt out:** Set the environment variable `MYCELIUM_NO_PING=1` before launching Claude Code. The hook will skip the network call entirely. Already-pinged installs leave a sentinel at `~/.mycelium/onboarded-<plugin>` — delete it if you want to reset state.

## License

MIT
