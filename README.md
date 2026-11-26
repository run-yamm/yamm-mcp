<!-- yamm-intro:start -->
# YAMM

[YAMM](https://yamm.com/) (Yet Another Mail Merge) is a mail merge for Gmail and Google Sheets. It sends a personalized email to each person on a list in a Google Sheet, from your own Gmail account. Give your AI assistant a Gmail draft and a sheet, and it sends you a test email, starts the mail merge, and reports opens, clicks, replies, bounces and unsubscribes.

This repository holds the YAMM plugin for Claude, Claude Code, ChatGPT, and Codex, which connects to YAMM MCP, the hosted remote MCP server. Any compatible MCP client can also connect to the server directly.
<!-- yamm-intro:end -->

<!-- yamm-package:start -->

## Plugin package

**Version:** `0.1.0` · **License:** [Talarian Work License](LICENSE)

Mail merge for Gmail and Google Sheets with YAMM (Yet Another Mail Merge): send a personalized email to each person on a list in a Google Sheet, from your own Gmail account, merged from a Gmail draft. Send yourself a test email first, then follow the sending and track opens, clicks, replies, bounces and unsubscribes.

The repository contains the [YAMM plugin package](docs/plugin.md) for the hosted MCP server.

<!-- yamm-package:end -->

## Get started

Setup instructions for each client go here.

## About this repository

You do not need anything from this repository to use YAMM MCP. There is no server for you to install or run.

The MCP server source is not in this public repository and is not open source.

The repository root is also the `yamm` plugin package that this repository's Claude Code and Codex marketplaces install, in the portable Agent Plugins 1.0 format. See [docs/plugin.md](docs/plugin.md).

## License

[Talarian Work License](LICENSE)
