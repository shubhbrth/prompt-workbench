# Gemini CLI Adapter

## Install

Copy `GEMINI.md` into the project or user context location Gemini CLI is configured to read. Keep `../../skill/` nearby if the CLI can include additional context files.

## Loading Behavior

Gemini CLI context loading depends on user and project settings. This adapter does not assume native Agent Skill discovery.

## Source Access

Use local bundled references when loaded. Web search and file access depend on Gemini CLI configuration and tool permissions.

## Smoke Test

Ask: `Improve this prompt using Prompt Workbench: "Analyze this data and tell me insights."`

Expected: Gemini asks clarifying questions before rewriting and notes any missing access to bundled references.

## Limitations

This adapter is a minimal phase 1 context file. It does not configure MCP servers, sandboxing, or alternate context filenames.
