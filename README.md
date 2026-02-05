# ai-agent-standards

This repository contains shared, cross-project instructions for AI
coding agents (Claude, Codex, Cursor, etc.). It is designed to provide a
single, consistent source of truth for how agents should behave when
working in any of your Rails projects.

These standards are meant to be reused across all repositories by adding
this repo as a Git submodule and linking the files into each project.

------------------------------------------------------------------------

## Overview

This repo typically contains:

-   `AGENTS.md` --- canonical, cross-agent instructions
-   `CLAUDE.md` --- Claude compatibility shim
-   `.cursor/rules/*.mdc` --- Cursor-specific scoped rules

The recommended setup uses a Git submodule so you can maintain one
central standards repo and share it across all projects without copying
files.

------------------------------------------------------------------------

## Initial Setup (One-Time)

Create this repository on GitHub:

    github.com/moottoast/ai-agent-standards

Then clone it locally and add your files:

    mkdir ai-agent-standards
    cd ai-agent-standards
    git init

    # Add:
    # - AGENTS.md
    # - CLAUDE.md
    # - .cursor/rules/*.mdc

    git add -A
    git commit -m "Initial agent standards"
    git branch -M main
    git remote add origin git@github.com:moottoast/ai-agent-standards.git
    git push -u origin main

This becomes your single source of truth for all agent behavior.

------------------------------------------------------------------------

## Using in a NEW Project

From the root of a new project repository:

### 1) Add as a submodule

    git submodule add git@github.com:moottoast/ai-agent-standards.git .ai-agent-standards

### 2) Create symlinks so agents find the files

    ln -sf .ai-agent-standards/AGENTS.md AGENTS.md
    ln -sf .ai-agent-standards/CLAUDE.md CLAUDE.md

    mkdir -p .cursor
    ln -sfn ../.ai-agent-standards/.cursor/rules .cursor/rules

### 3) Commit the wiring

    git add -A
    git commit -m "Add AI agent standards (submodule + links)"

Agents will now automatically see:

-   `AGENTS.md`
-   `CLAUDE.md`
-   `.cursor/rules/`

------------------------------------------------------------------------

## Adding to an EXISTING Project

From the root of the existing repository:

    git submodule add git@github.com:moottoast/ai-agent-standards.git .ai-agent-standards

    ln -sf .ai-agent-standards/AGENTS.md AGENTS.md
    ln -sf .ai-agent-standards/CLAUDE.md CLAUDE.md

    mkdir -p .cursor
    ln -sfn ../.ai-agent-standards/.cursor/rules .cursor/rules

    git add -A
    git commit -m "Add AI agent standards (submodule + links)"

------------------------------------------------------------------------

## Updating Standards Across Projects

When you improve the standards:

### 1) Update this repo

    git add -A
    git commit -m "Refine standards"
    git push

### 2) Pull updates into a project

Inside a project that uses the submodule:

    git submodule update --remote --merge
    git add .ai-agent-standards
    git commit -m "Update AI agent standards"

That project now uses the latest version.

------------------------------------------------------------------------

## Cloning Projects That Use This Submodule

When cloning:

    git clone --recurse-submodules <repo-url>

If already cloned:

    git submodule update --init --recursive

------------------------------------------------------------------------

## Optional Helper Script

You can create a script to automate adding standards to any repo:

``` bash
#!/usr/bin/env bash
set -euo pipefail

git submodule add git@github.com:moottoast/ai-agent-standards.git .ai-agent-standards || true

ln -sf .ai-agent-standards/AGENTS.md AGENTS.md
ln -sf .ai-agent-standards/CLAUDE.md CLAUDE.md

mkdir -p .cursor
ln -sfn ../.ai-agent-standards/.cursor/rules .cursor/rules

git add -A
git status
echo "Next: git commit -m \"Add AI agent standards\""
```
