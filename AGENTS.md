# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository contains a Claude Code skill called "temporal-awareness" that ensures temporal accuracy by using Unix date commands. The skill should be invoked whenever Claude needs date/time information: current date, day of week calculations, date arithmetic, or deadline computations.

## Structure

```
skills/temporal-awareness/SKILL.md  # Skill definition and documentation
```

## Key Concepts

- **GNU vs BSD date**: The skill handles both GNU date (Linux) and BSD date (macOS/FreeBSD), which have different syntax for date parsing and arithmetic
- **Trigger conditions**: Use this skill when users ask about dates, days of week, deadlines, durations, or any temporal context
- **Verification first**: Always run `date` commands before responding to date-sensitive queries, as Claude's system prompt date may be stale
