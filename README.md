# Onboarding Assistant

A general-purpose Claude Code extension that automatically sets up any development environment from documentation — no URLs needed. Works for new employees, experienced engineers hitting setup issues, and anyone onboarding to a new project or technology.

## How it works

1. Tell it what you want to set up — a project name, repo, or technology (e.g. Apache Kafka, AutoBuild, my-org/payments-service)
2. It auto-discovers the docs — searches GitHub, Confluence/Jira, official external docs, and internal wikis
3. It extracts a setup plan — prerequisites, environment variables, ordered steps
4. It walks you through execution — shows each command and waits for your confirmation before running
5. It validates the result — smoke tests containers, endpoints, and DB connections

## Trigger

Type /dev-setup or just say: set up my environment, I am new to this project, help me set up Kafka

## Architecture

The skill orchestrates five agents in sequence:

- doc-discoverer — searches GitHub, Confluence, and external docs for setup documentation
- doc-analyzer — parses the discovered docs into a structured setup plan
- env-checker — checks which tools and environment variables are already present
- executor — runs each setup step after user confirmation
- validator — smoke tests the completed setup

## MCP Integrations

| Integration | How |
|---|---|
| GitHub / GitLab | Custom MCP wrapping gh CLI |
| Docker / Compose | @hypnosis/docker-mcp-server |
| Confluence / Jira | atlassian MCP |
| External docs | WebFetch built-in tool |
| SAP internal wiki | bdi-wiki MCP (auto-detected in SAP environments) |
| Shell / DB checks | Bash built-in tool |

## Supported tech stacks

Works with any stack. Tested with:
- Java / Maven / Spring Boot
- Node.js / npm
- Docker / Docker Compose
- Apache Kafka
- PostgreSQL / MySQL

## Design principles

- No URL required — docs are discovered automatically
- Confirm before every command — nothing runs silently
- General-purpose — not tied to any company or stack
- Extensible — add new doc sources or execution strategies without changing the core skill

## Status

v1.0 — core onboarding flow (discovery → analysis → env check → execution → validation)

Wiki self-update planned for v2.
