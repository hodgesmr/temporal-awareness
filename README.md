# Claude Temporal Awareness

An [Agent Skill](https://agentskills.io) instructing Claude to use the Unix `date` command when working with dates, days of week, deadlines, and temporal calculations.

Claude's system prompt date can be stale or unavailable, leading to incorrect temporal reasoning. This skill ensures accuracy by running actual `date` commands before responding to date-sensitive queries. It handles both GNU date (Linux) and BSD date (macOS/FreeBSD), which have different syntax for date parsing and arithmetic.

## Installation (Global)

Clone the repository to a permanent location and symlink the skill into your Claude's skills directory.

```bash
git clone --branch latest git@github.com:hodgesmr/temporal-awareness.git ~/temporal-awareness
```

**Symlink to Claude's skills directory:**
```bash
ln -sfn ~/temporal-awareness/skills/temporal-awareness ~/.claude/skills/temporal-awareness

```

## Updating

```bash
cd ~/temporal-awareness && git fetch --tags --force && git checkout latest
```

Or pin a specific version:
```bash
cd ~/temporal-awareness && git fetch && git checkout 0.0.1
```

## Usage

Once installed, Claude will automatically invoke the skill when it detects date-related queries. Here's an example interaction:

```bash
❯ Here is a section of a contract proposal: "The engagement will begin Monday, March 23 and
  conclude Friday, April 3."

⏺ I notice this proposal specifies day-of-week for those dates. Let me verify if those dates align
  correctly with the days mentioned.

⏺ Skill(temporal-awareness)
  ⎿  Successfully loaded skill · 1 tool allowed

⏺ Bash(date -j -f "%Y-%m-%d" "2026-03-23" +%A && date -j -f "%Y-%m-%d" "2026-04-03" +%A)
  ⎿  Monday
     Friday

⏺ The dates in the proposal are correct for 2026:
  - March 23, 2026 is indeed a Monday
  - April 3, 2026 is indeed a Friday

  This is a 2-week engagement (10 business days).

❯ How would you update that section of the contract proposal to push the start and end dates
  back one week?

⏺ Bash(date -j -f "%Y-%m-%d" "2026-03-30" "+%A, %B %d" && date -j -f "%Y-%m-%d" "2026-04-10" "+%A,
      %B %d")
  ⎿  Monday, March 30
     Friday, April 10

⏺ Updated language:

  "The engagement will begin Monday, March 30 and conclude Friday, April 10."
```

## License

[MIT License](./LICENSE)