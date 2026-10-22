# LeadShark Apex: LinkedIn MCP Server

LeadShark Apex is a hosted, remote MCP server for LinkedIn automation. Connect it to Claude, Cursor, ChatGPT or any MCP client and let your agent run comment-to-DM automations, publish lead magnets, work your Leadbox inbox, schedule posts and read your analytics, all inside your own LinkedIn activity limits.

- **Endpoint:** `https://apex.leadshark.io/mcp`
- **Transport:** Streamable HTTP
- **Auth:** OAuth 2.1 with dynamic client registration (PKCE S256)
- **Scopes:** `mcp:read`, `mcp:write`
- **MCP Registry name:** `io.leadshark/apex`
- **Website:** https://www.leadshark.io
- **Docs:** https://www.leadshark.io/linkedin-mcp-server

There is nothing to install or self-host. This repository holds the public listing metadata (`server.json`, `mcp.json`) and docs for the hosted server.

## What you can do

- **Comment-to-DM automations:** create, edit, pause and inspect automations that reply to comments with a keyword and send the DM.
- **Lead magnets:** publish lead-magnet links and LeadShark Pages, and pull the leads they capture.
- **Leadbox inbox:** read your DM threads, get the full context with one person, and reply.
- **Posts:** schedule posts with an automation attached, edit or move them, and comment or react as yourself or as a Company Page.
- **Prospecting and analytics:** search people and posts, enrich profiles and companies, see who engaged with a post, and track engagement on your recent posts.
- **Safety:** check and set your activity limits before acting. Every write action is logged so your agent can audit what it did.

## Connect

When you add the server, your client opens a LeadShark sign-in page. Approve access and you are connected. No API key to copy.

### Claude (claude.ai and Claude Desktop)

1. Open **Settings**, then **Connectors**.
2. Click **Add custom connector**.
3. Name it `LeadShark Apex` and paste `https://apex.leadshark.io/mcp` as the URL.
4. Click **Connect** and sign in to LeadShark.

### Claude Code

```bash
claude mcp add --transport http leadshark-apex https://apex.leadshark.io/mcp
```

Then run `/mcp` inside Claude Code and choose **Authenticate**.

### Cursor

Add this to `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (project):

```json
{
  "mcpServers": {
    "leadshark-apex": {
      "url": "https://apex.leadshark.io/mcp"
    }
  }
}
```

Open **Cursor Settings**, then **MCP**, and click **Login** next to `leadshark-apex`.

### ChatGPT

1. Open **Settings**, then **Apps & Connectors**, then **Advanced settings**, and turn on **Developer mode**.
2. Back in **Apps & Connectors**, click **Create**.
3. Name it `LeadShark Apex`, paste `https://apex.leadshark.io/mcp` as the MCP server URL, and choose **OAuth** for authentication.
4. Click **Create** and sign in to LeadShark.

### Any other MCP client

Most clients that support remote servers accept the same `mcp.json` shape:

```json
{
  "mcpServers": {
    "leadshark-apex": {
      "url": "https://apex.leadshark.io/mcp"
    }
  }
}
```

Clients that only speak stdio can bridge with [`mcp-remote`](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "leadshark-apex": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://apex.leadshark.io/mcp"]
    }
  }
}
```

## Tools

Some tools depend on your LeadShark plan. Your client lists exactly what your account can use.

### Automations

| Tool | What it does |
| --- | --- |
| `list_automations` | List your automations with status, settings, stats and templates. |
| `get_automation` | Read the full current spec of one automation. |
| `create_automation` | Create a comment-to-DM automation for a post (starts as a draft). |
| `edit_automation` | Change an automation's name, status, keywords, templates or settings. |
| `suggest_automation_settings` | Suggest a name, keyword, DM template and replies for a post. |
| `manage_company_reply_automations` | Reply-only automations for Company Page posts. |

### Posts and scheduling

| Tool | What it does |
| --- | --- |
| `schedule_post_with_automation` | Schedule a post with optional automation, mentions and media. |
| `list_scheduled_posts` | List scheduled posts with content, timing and attached automation. |
| `get_scheduled_post` | Read one scheduled post and its pre-automation. |
| `edit_scheduled_post` | Edit a scheduled post's copy, time, mentions or automation. |
| `shift_scheduled_posts` | Move many scheduled posts at once. |
| `cancel_scheduled_post` | Cancel a pending scheduled post (requires confirmation). |
| `list_recent_posts` | Your latest posts with impressions, comments, reactions and reposts. |

### Lead magnets and pages

| Tool | What it does |
| --- | --- |
| `discover_lead_magnets` | Fresh lead-magnet posts from the LeadShark Lead Magnet Radar. |
| `manage_lead_magnet_links` | List, create and edit your lead-magnet links. |
| `list_lead_pages` | List your LeadShark Pages with capture stats. |
| `manage_lead_pages` | Create, edit and publish LeadShark Pages. |
| `get_page_leads` | Pull the email leads captured by one page. |

### Leadbox inbox and outreach

| Tool | What it does |
| --- | --- |
| `list_recent_messages` | Your DM threads, newest first. |
| `get_messages_with_person` | The full conversation with one person. |
| `get_lead_activity` | A briefing on a person before you message or connect. |
| `send_message` | Send a LinkedIn DM as yourself. |
| `send_email` | Send an email through your own connected email account. |
| `send_connection_request` | Send a connection request. |
| `manage_connections` | Connect with or remove connections. |
| `manage_invitations` | List, accept or ignore incoming connection requests. |
| `list_recent_connections` | Your most recent connections. |

### Prospecting and signals

| Tool | What it does |
| --- | --- |
| `search` | Find LinkedIn people or companies. |
| `search_posts` | Find LinkedIn posts by keyword. |
| `enrich` | Turn a LinkedIn person into a structured profile. |
| `enrich_company` | Turn a Company Page into a structured company profile. |
| `icp_fit` | Label people as fit, adjacent or not a fit for your ideal customer. |
| `list_person_posts` | Recent posts from one person. |
| `get_person_activity` | A person's recent comments and reactions. |
| `list_post_engagers` | Everyone who engaged with a post, ranked warmest first. |
| `list_signals` | Your heat-scored intent signals. |
| `feed` | Read your own LinkedIn home feed. |

### Engagement

| Tool | What it does |
| --- | --- |
| `comment_on_post` | Comment on a post as yourself. |
| `react_to_post` | React to a post as yourself. |
| `engage_with_comment` | Reply to or like a comment. |
| `list_companies` | The Company Pages you administer. |
| `comment_as_company` | Comment on a post as one of your Company Pages. |
| `react_as_company` | React to a post as one of your Company Pages. |

### Limits, profiles and audit

| Tool | What it does |
| --- | --- |
| `manage_activity_limits` | Read or change your activity limits before acting. |
| `set_daily_dm_limit` | Set your daily DM limit. Setting it to 0 pauses all DMs. |
| `list_actions` | The audit trail of write actions taken by your account. |
| `list_profiles` | The LinkedIn profiles your account can operate. |

## Files

- `server.json`: the MCP Registry entry for `io.leadshark/apex`.
- `mcp.json`: a ready-to-use client config.

## Support

Questions or issues: open an issue here or visit https://www.leadshark.io.

## License

MIT
