<!-- yamm-intro:start -->
# YAMM

[YAMM](https://yamm.com/) (Yet Another Mail Merge) is a mail merge for Gmail and Google Sheets. It sends a personalized email to each person on a list in a Google Sheet, from your own Gmail account. Give your AI assistant a Gmail draft and a sheet, and it can send you a test email first, then start the mail merge and report opens, clicks, replies, bounces and unsubscribes.

This repository holds the YAMM plugin for Claude, Claude Code, ChatGPT, and Codex, which connects to YAMM MCP, the hosted remote MCP server. Any compatible MCP client can also connect to the server directly.
<!-- yamm-intro:end -->

> **TIP**
>
> YAMM MCP doesn't need other connectors, but it works best alongside the official Gmail and Google Drive or Google Sheets connectors in your client. They can search for and create Gmail drafts, and find and work on your spreadsheets when needed.

The server is hosted at:

```text
https://mcp.yamm.com/mcp
```

You connect to YAMM MCP by adding this server URL to your client, which gives you [all the YAMM MCP tools](#mcp-tools). For detailed instructions, see:

- [ChatGPT](#chatgpt)

- [Claude](#claude)

- [Other MCP clients](#other-compatible-mcp-clients) that support remote servers over Streamable HTTP with OAuth

<!-- yamm-package:start -->

## Plugin package

**Version:** `1.0.0` · **License:** [Talarian Work License](LICENSE)

Mail merge for Gmail and Google Sheets with YAMM (Yet Another Mail Merge): send a personalized email to each person on a list in a Google Sheet, from your own Gmail account, merged from a Gmail draft. Send yourself a test email first, then follow the sending and track opens, clicks, replies, bounces and unsubscribes.

The repository contains the [YAMM plugin package](docs/plugin.md) for the hosted MCP server.

<!-- yamm-package:end -->

## MCP tools

| Tool | What it does | Inputs |
| --- | --- | --- |
| `yamm_send_test_email` | Sends one test email to your own address, merged from the Gmail draft and the first row below the sheet's header row. | Required: `spreadsheet_url_or_id`, `draft_id`. Optional: `email_column`, `sender_name`, `reply_to` |
| `yamm_send_gmail_mail_merge` | Starts a mail merge: one email per visible row of the sheet, merged from the Gmail draft. The sending goes on in the background after the call answers. | To start: `spreadsheet_url_or_id`, `draft_id`. To send the rest of a mail merge: `campaign_id`. Optional: `email_column`, `sender_name`, `reply_to`, `enable_tracking`, `partial_send_confirmed` |
| `yamm_get_mail_merge` | Reports a mail merge's progress and result, and its campaign's opens, clicks, replies, bounces, unsubscribes and poll answers. | `campaign_id` and `step_id`, or `spreadsheet_url_or_id` for the latest mail merge sent from that sheet |
| `yamm_get_account` | Reports your YAMM account, plan, and how many recipients you can email now. | None |
| `yamm_get_help_links` | Returns YAMM help topics, each with a short answer and a link to the help article. | None |

Notes on the inputs:

- `spreadsheet_url_or_id` accepts either a full Google Sheets URL or a bare spreadsheet ID. A sheet ID (`#gid=`) in the URL selects the sheet.

- `draft_id` identifies a Gmail draft. YAMM MCP does not search Gmail: your client gets the draft from a Gmail connector.

- `email_column` names the column that holds the recipients' addresses, when the sheet has more than one email column.

- `sender_name` sets the name shown in the From field, and `reply_to` the address replies go to.

- Tracking of opens and clicks is on by default. `enable_tracking` turns it off for one mail merge.

- `campaign_id` and `step_id` identify a mail merge. Your client takes them from the previous result, so you do not need to handle them yourself.

## Get started

### Before you start

To use YAMM MCP you need:

- **A Google account with Gmail.** YAMM sends from your own Gmail address. The first time you sign in, YAMM creates a YAMM account for you if you do not have one.

- **A YAMM plan, free or paid.** Your plan sets how many recipients you can email in 24 hours. For current plans, see [YAMM pricing](https://yamm.com/pricing/).

- **A Google Sheet and a Gmail draft.** The sheet holds one row per recipient, with a header row and a column of email addresses. The draft is the email to merge, with markers such as `{{First name}}` that refer to the sheet's column headers. For setup help, see the [YAMM help center](https://yamm.com/help/).

**Signing in.** Your client authenticates to YAMM MCP with OAuth. YAMM opens a browser window for Google sign-in when authentication is required. Accept every permission Google asks for: YAMM sends through Google's Apps Script and Gmail, which refuse a sign-in with fewer permissions. Your client stores the authentication credentials and reuses them for subsequent tool calls.

### ChatGPT

ChatGPT connects to YAMM MCP as a custom MCP server, in ChatGPT on the web. ChatGPT lets a custom MCP server take write actions, such as sending email, only on Business, Enterprise, and Edu workspaces. On other ChatGPT plans, ChatGPT can't send email with YAMM.

On a Business workspace, an admin or owner adds the server. On an Enterprise or Edu workspace, an admin, an owner, or a member with the **Create plugins with MCPs** permission can add it.

To connect ChatGPT to YAMM MCP:

1. Open ChatGPT in your browser.

1. In the sidebar, select **Plugins**.

1. Click **Add**, then select **Add custom MCP server**.

1. Define the server settings:

   - **Name**: Enter `YAMM`.

   - **Connection**: Select **Server URL** and enter `https://mcp.yamm.com/mcp`.

   - **Authentication**: Keep **OAuth**.

   - Check **I understand and want to continue**.

1. Click **Create as a plugin**.

1. Install the YAMM plugin, and follow the on-screen instructions to authenticate to YAMM MCP with your Google account.

Each workspace member authenticates with their own Google account. For who can add, share, and publish custom MCP servers in a workspace, see [Connecting custom MCP servers in ChatGPT](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt).

You can now [use YAMM](#using-yamm) in ChatGPT.

### Claude

Follow the instructions for your Claude account type:

- [Personal account](#claude-personal-account) — Free, Pro, Max, or Ultra plan

- [Organization account](#claude-organization-account) — Team or Enterprise plan

#### Claude personal account

1. Open Claude in your browser or in the Claude desktop app.

1. In the main sidebar, select **Customize**, then select **Connectors**.

1. Click **Add**, then select **Add custom connector**.

1. Enter `YAMM` as the name and `https://mcp.yamm.com/mcp` as the remote MCP server URL, then click **Continue**.

1. Keep the authentication settings marked **Detected**, and click **Add**.

1. Click **Connect**, and follow the on-screen instructions to authenticate to YAMM MCP with your Google account.

On the Free plan, you can add one custom connector.

You can now [use YAMM](#using-yamm) in Claude.

#### Claude organization account

An organization owner must first add YAMM as a custom connector for the organization. Once the connector is added, members can individually authenticate to YAMM MCP.

##### Add the YAMM connector to your Claude organization

If you're an organization owner:

1. Open Claude in your browser or in the Claude desktop app.

1. In the main sidebar, click your user name and select **Organization settings**.

1. In the settings sidebar, select **Plugins > Connectors**.

1. Click **Add**, then select **Custom**. If Claude asks for the connector type, choose **Web**.

1. Enter `YAMM` as the name and `https://mcp.yamm.com/mcp` as the remote MCP server URL. If the dialog shows **Continue**, click it.

1. Keep the authentication settings marked **Detected**, and click **Add**.

The YAMM connector is now available to your organization members.

##### Connect Claude to YAMM MCP

1. Open Claude in your browser or in the Claude desktop app.

1. In the main sidebar, select **Customize**, then select **Connectors**.

1. Find **YAMM**, labeled as custom, and click **Connect**.

1. Follow the on-screen instructions to authenticate to YAMM MCP with your Google account.

1. (Optional) To modify the tool permissions:

   1. In the connectors list, select **YAMM**.

   1. In the **Tool permissions** section, check the permissions and adjust them as needed.

You can now [use YAMM](#using-yamm) in Claude.

### Other compatible MCP clients

Any MCP client that supports remote servers over Streamable HTTP with OAuth can connect to YAMM MCP. Point it at `https://mcp.yamm.com/mcp` and complete the browser sign-in when the client prompts you.

Clients other than the ones above have not been tested with YAMM MCP. Configuration keys, transport names, sign-in commands, and tool permission settings differ between clients, so follow your client's own documentation for the setup steps.

## Using YAMM

To send a mail merge in Claude, ChatGPT, or another MCP client, start with a prompt where you:

- **Identify the Google Sheet with your recipients.** Provide the full Google Sheets URL, copied while the sheet you want is open, or name the spreadsheet so your client can find it.

- **Identify the Gmail draft.** Name it by its subject so your client can find it with its Gmail connector.

- **Say what you want done.** For example, send yourself a test email first, then send to everyone in the sheet.

Example prompt:

```text
Send my "Spring offer" Gmail draft to the contacts in this sheet:
https://docs.google.com/spreadsheets/d/<spreadsheet-id>/edit?gid=<sheet-id>#gid=<sheet-id>
Send me a test email first, and wait for my go-ahead before sending to everyone.
```

### How YAMM MCP works

**Testing.** Your client can send you a test email first, merged from the draft and the first row of the sheet, so you can check it before any recipient gets an email. Tracking, unsubscribe links and polls do not work in test emails.

**Sending.** When you confirm, your client starts the mail merge. YAMM sends from your Gmail account, one email per visible row, at a median rate of 30 emails per minute. The sending goes on in the background after the call answers.

**Following the sending.** YAMM adds a `Merge status` column to your sheet and writes each row's status as it goes, for example `EMAIL_SENT`, then `EMAIL_OPENED` or `RESPONDED` when tracking is on. Your client checks progress with `yamm_get_mail_merge` and reports opens, clicks, replies, bounces and unsubscribes for the campaign.

**Sending the rest.** If a mail merge stops before every row is sent, for example when your quota runs out, your client can send the rest later. Rows already sent are skipped.

Clients display all of this differently. Tool names, approval prompts, and progress reporting vary, so what you see depends on the client you use.

### What you can do

YAMM tests, sends, and follows mail merges from a Gmail draft and a Google Sheet. It sends from your Gmail account, writes each recipient's status in the sheet, and reports how recipients reacted. For work YAMM cannot do, see [YAMM limitations](#yamm-limitations).

#### Testing a mail merge

Send yourself one email, merged from the draft and the first row of the sheet, before any recipient gets one. Each test email counts as one recipient in your quota.

```text
Send me a test email of my "Spring offer" Gmail draft with the contacts in <spreadsheet-url>.
```

```text
Send me a test email of my "Webinar invite" draft with <spreadsheet-url>, from "Anna at Acme", with replies going to events@acme.com.
```

#### Sending a mail merge

Send one personalized email to each visible row of the sheet. YAMM skips rows it has already sent, filtered or hidden rows, and addresses that bounced or unsubscribed during an earlier mail merge.

```text
Send my "Spring offer" Gmail draft to everyone in the Leads sheet of <spreadsheet-url>.
```

```text
Send my "Renewal reminder" draft to the rows I left visible in <spreadsheet-url>, without tracking.
```

```text
The sheet in <spreadsheet-url> has a Work email and a Personal email column. Send my "Newsletter" draft to the Work email column.
```

#### Sending the rest of a mail merge

When a mail merge stops with emails left to send, for example because your quota ran out, send the rest later. Emails already sent do not go out again.

```text
My mail merge from <spreadsheet-url> stopped when I ran out of quota. Send the rest now.
```

#### Following the results

Follow the sending while it goes on, then see how recipients reacted. With tracking on, YAMM reports opens, clicks, replies, bounces, and unsubscribes for every mail merge sent from the same sheet, and poll answers when the email includes a poll.

```text
How is my mail merge from <spreadsheet-url> going?
```

```text
How many people opened, clicked, and replied to my last mail merge from <spreadsheet-url>?
```

```text
What did people answer to the poll in my last mail merge from <spreadsheet-url>?
```

#### Account and help

Check your plan and how many recipients you can email now, and get answers from YAMM's help articles, for example about setting up the sheet or the draft.

```text
How many recipients can I still email with YAMM today?
```

```text
How do I add a personalized link to my YAMM draft?
```

## Important behavior and safe use

**Approving tool calls.** MCP clients ask you to approve tool calls before they run. Where that prompt appears, how it is worded, and whether you can pre-approve a tool all vary by client. The two tools that send email declare themselves as making changes, so clients that act on those declarations will prompt you before running them.

**Emails go out from your Gmail account.** Recipients see them as sent by you. Check the test email before sending, and check that the sheet holds the recipients you mean to email.

**A mail merge cannot be stopped once started.** Every visible row that YAMM has not sent before gets an email. To send to only part of your list, filter or hide the other rows before you start.

**YAMM writes to your sheet.** It adds the `Merge status` column and notes. Do not edit or delete the tracking notes on the email address cells, or tracking stops working for those rows.

**Bounces put your account at risk.** If many emails bounce, YAMM stops the mail merge. Check the addresses in your sheet before sending again.

## YAMM limitations

YAMM MCP works with Google Sheets and Gmail drafts only.

It cannot currently:

- Send from a Gmail alias
- Send personalized attachments
- Send to filtered or hidden rows
- Send to addresses that bounced or unsubscribed during an earlier mail merge
- Stop a mail merge once it has started
- Run more than one mail merge or test email at a time on the same sheet

Your plan sets how many recipients you can email in 24 hours, counting CC and BCC. While Google limits a new Google Workspace account's sending, YAMM caps it at 400 recipients.

## Troubleshooting

**Sign-in fails, or the client says YAMM needs authentication.** Run your client's sign-in step rather than retrying the mail merge request. In ChatGPT and Claude, sign in again from the plugin's or connector's settings. If sign-in succeeds but the client still reports a problem, start a new session or chat and try again.

**Sign-in fails after you unchecked a permission.** YAMM needs every permission Google asks for. Sign in again and accept them all.

**Claude cannot reach the server, but your network can.** Remote connectors are brokered from Anthropic's servers, not from your machine. This is true in Claude Desktop and in Cowork as well. A firewall rule or VPN on your own machine is therefore not the cause, and allowing the address locally will not change the result.

**YAMM cannot open the spreadsheet.** Check that the Google account you signed in with has edit access to that spreadsheet, and that the spreadsheet has not been moved or deleted. YAMM writes each row's status in the sheet, so it needs edit access.

**The spreadsheet URL or ID is rejected.** Supply either the full Google Sheets URL or the bare ID. In a URL such as `https://docs.google.com/spreadsheets/d/1etZyGGQPami0R9D2W6WlJMWbrd_JvStLDdsteFegnko/edit`, the ID is the part between `/d/` and `/edit`. Links from other Google products, and shortened links, may not contain the ID.

**YAMM asks which sheet to use, or used the wrong sheet.** Copy the URL while the sheet you want is open, so its `#gid=` selects the sheet.

**YAMM cannot find the email column.** The sheet needs a header row and a column whose header YAMM recognizes as email addresses. If the sheet has several email columns, say which one to use.

**There is nothing to send.** Every row is already sent, filtered, or hidden, has no email address, or holds an address that bounced or unsubscribed during an earlier mail merge.

**YAMM refuses tracking for the draft.** Tracking needs a draft with formatting, not one written in Gmail's plain text mode. Turn off plain text mode in the draft, or send the mail merge without tracking.

**The test email has not arrived.** YAMM takes about 30 seconds to send it. Check your Gmail inbox before asking for another one: each test email counts as one recipient in your quota.

**Links in the test email are Google redirect links.** They work. In the mail merge with tracking on, YAMM replaces them with direct tracked links.

**The client reported the mail merge as failed, or started over.** The sending goes on in the background after the call answers. Ask your client for the mail merge's status before sending again. Emails already sent do not go out again.

**The sheet is already in use.** A mail merge or a test email is already sending from that sheet. Wait a minute and try again.

**The mail merge stopped with emails left to send.** Your quota may have run out. Your client can send the rest later. Emails already sent do not go out again.

**The status of some emails is unclear.** Emails may have been sent without a status in the `Merge status` column. Check your Gmail Sent folder before sending again.

**Opens and clicks do not show yet.** Tracking can take up to 2 minutes to appear in the `Merge status` column.

**YAMM stopped because of a high bounce rate.** Check the email addresses in your sheet before you start the mail merge again.

**Problems with your client itself.** If your client will not add the connector or plugin, does not pick up its configuration file, does not recognize a command, or does not show the setup screens described here, that is a client-side problem rather than a YAMM problem. Client interfaces change, so yours may differ from what is described here. Check your client's own documentation.

## Support and policies

- [Contact support](https://support.yamm.com/hc/en-us/requests/new)

- [Trust center](https://security.talarian.io)

- [Security and privacy FAQ](https://yamm.com/help/resources/data-security-and-policy/)

- [Privacy policy](https://yamm.com/privacy-policy/)

- [Terms of service](https://yamm.com/terms-of-service/)

- [Data processing agreement](https://talarian.io/data-processing-agreement)

- [Pricing](https://yamm.com/pricing/)

- [Release notes](https://yamm.com/help/resources/release-notes/)

To report a security vulnerability, follow the responsible disclosure process on the [Talarian trust center](https://security.talarian.io).

## About this repository

This repository is the canonical documentation for YAMM MCP.

You do not need anything from this repository to use YAMM MCP. There is no server for you to install or run.

The MCP server source is not in this public repository and is not open source.

The repository root is also the `yamm` plugin package that this repository's Claude Code and Codex marketplaces install, in the portable Agent Plugins 1.0 format. See [docs/plugin.md](docs/plugin.md).

## License

[Talarian Work License](LICENSE)
