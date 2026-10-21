# Google Cloud BigQuery

Cursor plugin that connects agents to [Google Cloud BigQuery](https://docs.cloud.google.com/bigquery/docs/use-bigquery-mcp) through Google Cloud BigQuery's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Explore datasets and tables and run SQL queries.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Google Cloud BigQuery**.
3. Click **Install**, then set the OAuth Client ID and Client Secret (below) and complete the Google sign-in prompt.

Or run `/add-plugin google-cloud-bigquery` in chat.

## MCP

```json
{
  "mcpServers": {
    "google-cloud-bigquery": {
      "type": "http",
      "url": "https://bigquery.googleapis.com/mcp",
      "auth": {
        "CLIENT_ID": "${CLIENT_ID}",
        "CLIENT_SECRET": "${CLIENT_SECRET}",
        "scopes": ["https://www.googleapis.com/auth/bigquery"]
      }
    }
  }
}
```

## Before you connect

You need a Google Cloud project with the BigQuery API enabled, and your Google account needs the MCP Tool User role (`roles/mcp.toolUser`) plus BigQuery Job User and Data Viewer on that project.

## Setup

Google's OAuth server does not support Dynamic Client Registration, so you have to bring your own OAuth client.

1. In the Google Cloud console, open **APIs & Services → OAuth consent screen** and configure it if the project doesn't have one yet. Add the `https://www.googleapis.com/auth/bigquery` scope.
2. Open [**APIs & Services → Credentials**](https://console.cloud.google.com/apis/credentials), click **Create credentials → OAuth client ID**, and choose **Web application**.
3. Add both authorized redirect URIs:
   - Desktop: `http://localhost:8787/callback`
   - Web and Cloud Agents: `https://www.cursor.com/agents/mcp/oauth/callback`
4. Copy the **Client ID** and **Client secret**.
5. In **Dashboard → Plugins → Configure**, set **OAuth Client ID** and **OAuth Client Secret** from that client.
6. Complete the Google OAuth login when Cursor prompts.

On a team marketplace an admin can set the credentials once for everyone; each member still completes their own Google login, so queries run with that member's IAM permissions. If the consent screen is in **Testing**, only listed test users can sign in.

## What agents can do

| Category | Capabilities |
| --- | --- |
| Explore | List datasets and tables and read their metadata and schemas |
| Query | Run read-only SQL, including BigQuery ML functions |
| Write | Run DML and DDL when the account allows it |
| Jobs | Poll results and cancel running query jobs |

The hosted runtime is the source of truth for tool names and schemas.

## Notes

- Queries are billed to the project id passed to the tool.
- Admins can block the write-capable `execute_sql` tool with an IAM deny policy while leaving read-only queries available.
- Grok also offers this connector with service-identity auth; this plugin configures only the user OAuth flow.

## Docs

- Use the BigQuery MCP server: https://docs.cloud.google.com/bigquery/docs/use-bigquery-mcp
- Tools reference: https://docs.cloud.google.com/bigquery/docs/reference/mcp
- Server URL: https://bigquery.googleapis.com/mcp

Logo is the official BigQuery product icon from Google Cloud's architecture icon set, on a padded white tile.

## License

MIT
