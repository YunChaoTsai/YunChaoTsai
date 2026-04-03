# GitHub Profile Redesign — Design Spec

**Date:** 2026-04-04
**Status:** Approved

## Overview

Redesign the GitHub profile README from a near-empty placeholder (only a Daily.dev devcard) into a polished, hybrid-style profile that communicates YunChao's identity as a Full Stack Developer without over-engineering the page.

## Style Direction

**Hybrid** — clean centered header with typing animation, categorized tech stack badges, auto-updating GitHub activity graph, and auto-updating recent activity feed. No featured projects section (most work is in private org repos).

Reference inspirations:
- [UranusLin](https://github.com/UranusLin) — detailed, structured layout
- [VdustR](https://github.com/VdustR) — clean, animated, centered

## Sections

### 1. Header

- Greeting: `Hi, I'm YunChao 👋`
- Typing animation (readme-typing-svg): `Full Stack Developer | TypeScript · Go · Flutter`
- LinkedIn badge: `https://www.linkedin.com/in/yunchaocai/`

### 2. Tech Stack

Displayed as shields.io badges organized in three labeled rows:

| Category | Technologies |
|----------|-------------|
| Frontend | TypeScript, React, Vite |
| Backend  | Python, Django, Go, Gin, Docker |
| Mobile   | Flutter, Dart |

### 3. GitHub Activity Graph

- Service: `github-readme-activity-graph.vercel.app`
- Theme: `gruvbox`
- Auto-updated on every push via the existing daily-devcard workflow (or a new workflow)

### 4. Recent Activity

- Service: `github-readme-activity` GitHub Action (`jamesgeorge007/github-activity-readme`)
- Shows latest 5 GitHub events (PRs merged, pushes, releases, etc.)
- Auto-updated on a daily cron schedule via GitHub Actions
- Wrapped in `<!--START_SECTION:activity-->` / `<!--END_SECTION:activity-->` markers

## GitHub Actions

Two workflows required:

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| `cron_update_daily_dev.yml` | existing | Keeps Daily.dev devcard (already present, keep as-is or remove) |
| `update_activity.yml` | daily cron + push | Updates Recent Activity section |

> The Daily.dev devcard is removed from the profile to keep it clean. The existing workflow can be disabled or deleted.

## Existing Workflow

`cron_update_daily_dev.yml` — currently updates the devcard SVG to the `devcard` branch. Since the devcard is being removed from the profile, this workflow should be disabled.

## Non-Goals

- No featured projects section
- No GitHub streak stats
- No top languages widget
- No Buy Me A Coffee or other monetization links
- No Twitter/X or other social links beyond LinkedIn

## Implementation Notes

- All badges use `shields.io` flat-square style for consistency
- Activity graph uses `hide_border=true` to match minimal aesthetic
- README is center-aligned for the header, left-aligned for body sections
- `.superpowers/` should be added to `.gitignore`
