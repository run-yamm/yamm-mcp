# YAMM MCP

Placeholder introduction: the first release replaces this title and paragraph with the intro maintained in the internal repository.

The server is hosted at:

```text
https://mcp.yamm.com/mcp
```

Depending on your client, you either install YAMM from the client's directory or manually add the server URL to your client. Either way, you get [all the YAMM MCP tools](#mcp-tools). For detailed instructions, see:

- [ChatGPT](#chatgpt)

- [Codex CLI](#codex-cli)

- [Claude](#claude)

- [Claude Code CLI](#claude-code-cli)

- [Other MCP clients](#other-compatible-mcp-clients) that support remote servers over Streamable HTTP with OAuth

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

- **Google Drive, Google Sheets, and Gmail connectors in your client.** YAMM MCP does not search, read, or create spreadsheets or drafts. Your client finds them with its own connectors and passes them to YAMM.

**Signing in.** Your client authenticates to YAMM MCP with OAuth. YAMM opens a browser window for Google sign-in when authentication is required. Accept every permission Google asks for: YAMM sends through Google's Apps Script and Gmail, which refuse a sign-in with fewer permissions. Your client stores the authentication credentials and reuses them for subsequent tool calls.

<!-- TODO: replace the placeholder directory links (TODO-yamm) once YAMM is listed, and add the screenshots. -->

### ChatGPT

Install the [YAMM plugin from the ChatGPT plugins directory](https://chatgpt.com/plugins/TODO-yamm-plugin-id). Installing the plugin makes YAMM available in ChatGPT and Codex, including the Codex CLI.

Follow the instructions for your ChatGPT account type:

- [Personal account](#chatgpt-personal-account)

- [Organization account](#chatgpt-organization-account) — Part of a managed workspace

#### ChatGPT personal account

1. Sign in to ChatGPT in your browser or in the ChatGPT desktop app.

   If you're in the browser, you can go directly to the [YAMM plugin's directory listing](https://chatgpt.com/plugins/TODO-yamm-plugin-id), click **Install plugin**, and continue from step 5.

1. In the sidebar, select **Plugins**.

1. Search for `YAMM`.

1. Click the **+** button for **YAMM**. In the ChatGPT desktop app, click **Install** instead.

1. Click **Continue to YAMM**.

1. Follow the on-screen instructions to authenticate to YAMM MCP with your Google account.

You can now [use YAMM](#using-yamm) in ChatGPT as well as in Codex, including the Codex CLI.

#### ChatGPT organization account

A workspace admin or owner must first make the YAMM plugin available to workspace members. Once the plugin is available, members can individually connect to YAMM MCP.

##### Add the YAMM plugin to your ChatGPT workspace

If you're a workspace admin or owner:

1. Sign in to the [OpenAI Admin Console](https://admin.openai.com/).

1. In the sidebar, select **Plugins**.

1. Search for `YAMM`.

1. In the public search results, select **YAMM**.

1. Click **Enable**.

1. In the **Availability** section, select how you want to make the YAMM plugin available to your workspace members:

   - **Available**: Members can search for and install the plugin if they want to use YAMM.

   - **Installed**: Members have the plugin preinstalled, but they still need to authenticate before they can use YAMM.

1. Check and configure the other plugin settings. For more information, see the [OpenAI documentation](https://learn.chatgpt.com/docs/enterprise/apps-and-connectors).

The YAMM plugin is now available to your workspace members. To connect to YAMM MCP, members can follow the instructions in [Connect ChatGPT to YAMM MCP](#connect-chatgpt-to-yamm-mcp).

##### Connect ChatGPT to YAMM MCP

- If the YAMM plugin is not available in your workspace, ask your workspace admin or owner to add it. They can follow the instructions in [Add the YAMM plugin to your ChatGPT workspace](#add-the-yamm-plugin-to-your-chatgpt-workspace).

- If the YAMM plugin is available but not preinstalled in your workspace, follow the instructions in [ChatGPT personal account](#chatgpt-personal-account).

- If the YAMM plugin is preinstalled in your workspace:

  1. Sign in to ChatGPT in your browser or in the ChatGPT desktop app.

     If you're in the browser, you can go directly to the [YAMM plugin's directory listing](https://chatgpt.com/plugins/TODO-yamm-plugin-id), click **Manage**, and continue from step 5.

  1. In the sidebar, select **Plugins**.

  1. Under **Installed**, select **YAMM**.

  1. Click **Manage**.

  1. Click **Connect**.

  1. Click **Continue to YAMM**.

  1. Follow the on-screen instructions to authenticate to YAMM MCP with your Google account.

You can now [use YAMM](#using-yamm) in ChatGPT as well as in Codex, including the Codex CLI.

### Codex CLI

> **NOTE**
>
> If you already have [ChatGPT connected to YAMM MCP](#chatgpt), the Codex CLI is also connected — provided you're signed in to the CLI with the same ChatGPT user account. If not, connecting the CLI also connects ChatGPT and the rest of Codex to YAMM MCP.

1. Open the Codex CLI in your terminal.

1. Enter `/plugins`. Codex lists all available plugins.

1. Enter `YAMM` to filter the list.

1. In the list, select **YAMM**.

1. Select **Install plugin**.

1. Select **Install on ChatGPT**. ChatGPT opens in your browser.

   If you have an organization account and Codex does not show **Install on ChatGPT**, YAMM is not available in your ChatGPT workspace. Select **Uninstall plugin**, and ask your workspace admin or owner to add YAMM. They can follow the instructions in [Add the YAMM plugin to your ChatGPT workspace](#add-the-yamm-plugin-to-your-chatgpt-workspace).

1. Sign in to ChatGPT.

1. Click **Manage**.

1. Click **Connect**.

1. Click **Continue to YAMM**.

1. Follow the on-screen instructions to authenticate to YAMM MCP with your Google account.

1. Back in the Codex CLI, select **I've installed it**.

You can now [use YAMM](#using-yamm) in the Codex CLI as well as in ChatGPT and the rest of Codex.

### Claude

Install the [YAMM connector from the Claude connectors directory](https://claude.ai/directory/connectors/TODO-yamm). Installing the connector makes YAMM available in Claude and Claude Code.

Follow the instructions for your Claude account type:

- [Personal account](#claude-personal-account) — Free, Pro, or Max plan

- [Organization account](#claude-organization-account) — Part of a team

#### Claude personal account

1. Open Claude in your browser or in the Claude desktop app.

   If you're in the browser, you can go directly to the [YAMM connector's directory listing](https://claude.ai/directory/connectors/TODO-yamm) and continue from step 6.

1. In the main sidebar, click your user name and select **Settings**.

1. In the settings sidebar, select **Customize > Connectors**.

1. Search for `YAMM`.

1. Select **YAMM**.

1. Click **Connect to Claude**.

1. Follow the on-screen instructions to authenticate to YAMM MCP.

You can now [use YAMM](#using-yamm) in Claude.

#### Claude organization account

An organization owner must first make the YAMM connector available to organization members. Once the connector is available, members can individually authenticate to YAMM MCP.

##### Add the YAMM connector to your Claude organization

If you're an organization owner:

1. Open Claude in your browser or in the Claude desktop app.

1. In the main sidebar, click your user name and select **Organization settings**.

1. In the settings sidebar, select **Plugins > Connectors**.

1. Click **Add > All available**.

1. Search for `YAMM`.

1. Click the **+** button for **YAMM**.

1. Click **Connect for your team**.

1. (Optional) To modify the tool permission restrictions for your organization:

   1. Select the **Tools** tab.

   1. Check the permission restrictions and adjust them as needed.

The YAMM connector is now available to your organization members.

##### Connect Claude to YAMM MCP

1. Open Claude in your browser or in the Claude desktop app.

   If you're in the browser, you can go directly to the [YAMM connector's directory listing](https://claude.ai/directory/connectors/TODO-yamm), click **Connect**, and continue from step 5.

1. In the main sidebar, click your user name and select **Settings**.

1. In the settings sidebar, select **Customize > Connectors**.

1. Click **Connect** for **YAMM**.

1. Follow the on-screen instructions to authenticate to YAMM MCP.

1. (Optional) To modify the tool permissions:

   1. In the connectors list, select **YAMM**.

   1. In the **Tool permissions** section, check the permissions and adjust them as needed.

You can now [use YAMM](#using-yamm) in Claude.

### Claude Code CLI

> **NOTE**
>
> If you already have [Claude connected to YAMM MCP](#claude), the Claude Code CLI is also connected — provided you're signed in to the CLI with the same Claude user account.

1. Open your terminal and run the following command:

   ```bash
   claude mcp add --transport http yamm https://mcp.yamm.com/mcp
   ```

   This adds the server for the current project only. To make the server available in all your projects, add `--scope user` to the command:

   ```bash
   claude mcp add --transport http yamm https://mcp.yamm.com/mcp --scope user
   ```

1. Start a new Claude Code CLI session.

1. Run `/mcp`, select `yamm`, and select `Authenticate`. Follow the on-screen instructions to authenticate to YAMM MCP.

You can now [use YAMM](#using-yamm) in the Claude Code CLI.

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

## Data and privacy

YAMM MCP works through your Google account, only on the spreadsheet and Gmail draft your client names in a tool call. It reads the sheet and the draft to merge them, sends from your Gmail account, and writes each row's status to the sheet. At sign-in, you grant YAMM access to Gmail and Google Sheets. Your AI assistant gets back counts, statuses and IDs, never a recipient's row or a personalized email. YAMM stores your subject lines, the spreadsheet's ID and title, tracking counts, and the addresses that bounced or unsubscribed, which it checks before each mail merge. It does not store your other recipients' addresses, your drafts or your sheet's contents. For details, see [what data YAMM stores](https://yamm.com/help/resources/data-security-and-policy/data-policy/data-storage-what-data-is-stored-by-yamm-and-how-is-it-used/) and the [YAMM privacy policy](https://yamm.com/privacy-policy/).

## Important behavior and safe use

**Approving tool calls.** MCP clients ask you to approve tool calls before they run. Where that prompt appears, how it is worded, and whether you can pre-approve a tool all vary by client. The two tools that send email declare themselves as making changes, so clients that act on those declarations will prompt you before running them.

**Emails go out from your Gmail account.** Recipients see them as sent by you. Check the test email before sending, and check that the sheet holds the recipients you mean to email.

**A mail merge cannot be stopped once started.** Every visible row that YAMM has not sent before gets an email. To send to only part of your list, filter or hide the other rows before you start.

**YAMM writes to your sheet.** It adds the `Merge status` column and notes. Do not edit or delete the tracking notes on the email address cells, or tracking stops working for those rows.

**Bounces put your account at risk.** If many emails bounce, YAMM stops the mail merge. Check the addresses in your sheet before sending again.

## Platforms and compatibility

<!-- TODO: fill in which clients were tested end to end before release. -->

| Client | Tested | Restrictions to know |
| --- | --- | --- |
| ChatGPT | To confirm | Organization accounts: An admin or owner must first make the YAMM plugin available. |
| Codex CLI | To confirm | Organization accounts: An admin or owner must first make the YAMM plugin available. |
| Claude | To confirm | Organization accounts: An owner must first make the YAMM connector available. |
| Claude Code CLI | To confirm | None |
| Other MCP clients | No | Untested. Follow your client's own documentation. |

Every client needs Streamable HTTP support and OAuth to connect.

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

**Sign-in fails, or the client says YAMM needs authentication.** Run your client's sign-in step rather than retrying the mail merge request. In ChatGPT and Claude, sign in again from the plugin's or connector's settings. This also covers Codex and Claude Code when they're connected through ChatGPT or Claude. If sign-in succeeds but the client still reports a problem, start a new session or chat and try again.

**Sign-in fails after you unchecked a permission.** YAMM needs every permission Google asks for. Sign in again and accept them all.

**Browser sign-in in a terminal, a remote session, or a headless environment.** In the Codex CLI, connect the YAMM plugin in ChatGPT on any device, and then select **I've installed it** in the CLI. In the Claude Code CLI, connect the YAMM connector in Claude on any device, and then start a new CLI session. Signing in from the CLI itself with `/mcp` needs a browser on the machine running the CLI.

**The Codex CLI shows YAMM as installed, but every request fails because YAMM MCP is not connected.** The plugin was installed in the CLI without a ChatGPT connection. This happens when YAMM is not available in your ChatGPT workspace. Uninstall the plugin in `/plugins`, ask your workspace admin or owner to [add YAMM to your workspace](#add-the-yamm-plugin-to-your-chatgpt-workspace), and then [install it again](#codex-cli).

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
