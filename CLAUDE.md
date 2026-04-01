# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is Fred Carbonare's personal open notebook — a collection of reusable code snippets, workflow templates, setup guides, and utility functions organized by technology. There is no build system, package manager, or test suite. The primary content format is Markdown with embedded code blocks.

## Repository Structure

| Directory | Contents |
|-----------|----------|
| `n8n/` | N8N automation workflow templates, deployment guides (AWS Lightsail), and JavaScript utility functions for use inside N8N's Code node |
| `n8n/samples/` | Complete workflow examples as `.json` + companion `.md` docs |
| `n8n/templates/` | Reusable workflow templates (same `.json` + `.md` pattern) |
| `n8n/utils/` | JavaScript snippets for common N8N tasks (dates, names, charts, JSON, files) |
| `pipedrive/` | Standalone HTML tools that call the Pipedrive API in-browser to extract field definitions and config |
| `athena/` | AWS Athena SQL queries and SendGrid/S3/Glue setup guides |
| `stack/` | Notes on infrastructure choices: AWS SES email stack, Novu notifications, Android-as-server, tools under evaluation |
| `ga4-gtm/` | Google Analytics 4 and Tag Manager reference links |
| `rdstation/` | HTML snippets for RD Station landing pages |
| `regex/` | Regex patterns for URL/domain extraction and input validation |
| `sql/` | General SQL and date-handling snippets |

## Content Conventions

- **Markdown files** describe what the snippet does and show usage; embedded code blocks contain the actual snippet.
- **N8N workflows**: JSON files are the importable workflow; the companion `.md` explains setup and any required credentials/environment variables.
- **N8N utils**: JavaScript written for N8N's Code node — uses `$input`, `$json`, `$node` N8N built-ins rather than standard Node.js APIs.
- **HTML tools** in `pipedrive/` are self-contained single-file apps (no dependencies, inline JS).

## Adding New Content

- Follow the existing pattern for the relevant directory: a `.md` doc paired with the raw file (`.json`, `.html`, `.sql`) when applicable.
- N8N workflow JSONs should be exported directly from the N8N editor.
- Utility snippets for N8N go in `n8n/utils/` with a short `.md` describing inputs, outputs, and example usage.
