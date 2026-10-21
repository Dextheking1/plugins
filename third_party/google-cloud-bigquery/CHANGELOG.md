# Changelog

All notable changes to this plugin will be documented here.

## 1.1.0 — bring your own OAuth client

- Added required `CLIENT_ID` and `CLIENT_SECRET` plugin variables, because Google's OAuth server has no dynamic client registration. Users create a Web application OAuth client in their Google Cloud project and enter its credentials.
- Requests the `https://www.googleapis.com/auth/bigquery` scope, which the server advertises in its protected resource metadata.

## 1.0.0 — initial release

- Added the `google-cloud-bigquery` MCP server pointing at Google Cloud BigQuery's hosted Streamable HTTP endpoint (`https://bigquery.googleapis.com/mcp`).
- Auth uses OAuth with Google Cloud BigQuery user login — no API key or client ID to configure.
- Logo: Official BigQuery product icon from Google Cloud's architecture icon set, on a padded white tile.
