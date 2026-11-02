<p align="center">
  <img src="assets/logo.png" alt="BiglySales" width="96" height="96">
</p>

# BiglySales MCP Server

Connect Claude, ChatGPT or any MCP client to your [BiglySales](https://biglysales.com) workspace and configure the AI sales assistant that calls and texts your leads, by chatting instead of clicking through settings.

This is a hosted (remote) MCP server. There is nothing to install or run. This repository holds the public listing, connection details and registry metadata; the server itself runs at BiglySales.

| | |
|---|---|
| **Server URL** | `https://app.biglysales.com/mcp` |
| **Transport** | Streamable HTTP |
| **Authentication** | OAuth 2.1 (sign in with your BiglySales account), or a workspace access token |
| **Documentation** | [docs.biglysales.com/mcp](https://docs.biglysales.com/mcp) |

## What you can do

- Review and change AI settings such as timezone, guard rails and whether AI is enabled.
- Edit the company variables, intros, opening messages and qualifying questions your assistant uses.
- Switch the voice assistant's LLM, voice or speech-to-text model and tune its prompt.
- Manage the SMS agents that answer inbound texts.
- Set up follow-up sequences, first-day follow-ups and working hours.
- Manage outbound webhooks, AI tool settings and Web Calling (embed snippet and allowed domains).
- Preview the exact context your assistant will use on a call, without placing one.

It does **not** read or edit contacts, lists, calls, messages, billing or phone numbers, and it never places calls or sends messages.

### Safe by design

- Every change is shown to you as a preview first and is only applied after you confirm it.
- Credentials and API keys are entered in the BiglySales app, never in chat. Stored ones always come back masked.
- Credit data is never shown.
- Each connection is tied to you and to one workspace, and every change is audited.

## Requirements

- A BiglySales workspace with MCP access enabled. If it isn't enabled for your account, contact [support](https://biglysales.com/contact/).
- A role that includes MCP access. Owners and admins have it by default.

## Connect

Full step-by-step instructions are at [docs.biglysales.com/mcp/connect](https://docs.biglysales.com/mcp/connect).

### Claude (web, desktop and mobile)

1. In Claude, open **Customize › Connectors › Add custom connector**.
2. Name: `BiglySales`, Remote MCP server URL: `https://app.biglysales.com/mcp`.
3. Click **Connect**, sign in to BiglySales, pick a workspace and click **Allow**.

Claude Team and Enterprise Owners can add the connector for the whole organization.

### ChatGPT

Add a custom MCP server with the URL `https://app.biglysales.com/mcp` and Authentication set to **OAuth** (leave client ID and secret empty), then sign in and allow access.

### Claude Code, Codex, Cursor, VS Code, Windsurf, Gemini CLI and other clients

These clients connect with a workspace access token:

1. In BiglySales, open the MCP setup screen and generate an access token. It is shown only once; treat it like a password.
2. Copy your workspace's MCP URL from the same screen. It ends in `/api/v2/mcp`.
3. Add the server to your client with the header `Authorization: Bearer <token>`.

The setup screen generates the exact snippet for each client. For example, Claude Code:

```bash
claude mcp add biglysales --transport http <your-workspace-mcp-url> --header "Authorization: Bearer <token>"
```

Cursor (`~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "biglysales": {
      "url": "<your-workspace-mcp-url>",
      "headers": { "Authorization": "Bearer <token>" }
    }
  }
}
```

You can revoke a token, or disconnect an OAuth app, at any time from the BiglySales app.

## Tools

Each area has a read tool and an update tool. Update tools work in two steps: `preview_update` shows the change, and `apply_update` saves it only after you confirm.

| Tool | Title | Type |
|---|---|---|
| `tenant_ai_onboarding_guide` | Get onboarding guide | Read-only |
| `tenant_ai_settings` | Read AI settings | Read-only |
| `tenant_ai_settings_update` | Update AI settings | Write |
| `tenant_ai_company_variables` | Read company variables | Read-only |
| `tenant_ai_company_variables_update` | Update company variables | Write |
| `tenant_ai_intros` | Read AI intros | Read-only |
| `tenant_ai_intros_update` | Update AI intros | Write |
| `tenant_ai_voice_prompt` | Read voice assistant | Read-only |
| `tenant_ai_voice_prompt_update` | Update voice assistant | Write |
| `tenant_ai_sms_agents` | Read SMS agents | Read-only |
| `tenant_ai_sms_agents_update` | Update SMS agents | Write |
| `tenant_ai_followup` | Read followup sequence | Read-only |
| `tenant_ai_followup_update` | Update followup sequence | Write |
| `tenant_ai_first_day_followup` | Read first-day followup | Read-only |
| `tenant_ai_first_day_followup_update` | Update first-day followup | Write |
| `tenant_ai_webhooks` | Read webhooks | Read-only |
| `tenant_ai_webhooks_update` | Update webhooks | Write |
| `tenant_ai_tools_configuration` | Read AI tool settings | Read-only |
| `tenant_ai_tools_configuration_update` | Update AI tool settings | Write |
| `tenant_ai_web_call` | Read web calling settings | Read-only |
| `tenant_ai_web_call_update` | Update web calling settings | Write |
| `tenant_ai_call_context_preview` | Preview AI call context | Read-only |

The server also provides guided prompts (onboarding, working hours, follow-up sequences, voice and model changes, SMS agents, diagnosing blocked calls) and reference resources (settings, placeholders, models, prompt-writing guide).

## Example prompts

- "Show me my AI assistant's current settings."
- "Change my follow-up working hours to 9am–5pm Eastern, Monday to Friday."
- "Preview what my AI will say on a web call."

## Support, privacy and terms

- Support: [biglysales.com/contact](https://biglysales.com/contact/) or support@biglysales.com
- Privacy policy: [biglysales.com/privacy-policy](https://biglysales.com/privacy-policy/)
- Terms of use: [biglysales.com/terms-of-use](https://biglysales.com/terms-of-use/)
