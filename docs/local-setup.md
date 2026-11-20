# Local n8n setup

From the repository root, with Docker Desktop or Docker Engine running:

```sh
docker compose config --quiet
docker compose up -d --wait --wait-timeout 120
docker compose ps
curl --fail --silent --show-error http://127.0.0.1:5678/healthz
curl --fail --silent --show-error http://127.0.0.1:5678/healthz/readiness
```

Both endpoints should return HTTP 200. Readiness also checks whether the
database is ready. Open [the n8n editor](http://localhost:5678/) and create
your local instance owner on first launch. Use the localhost URL for browser
sign-in and OAuth. [n8n health endpoints](https://docs.n8n.io/hosting/logging-monitoring/monitoring/)

Compose publishes n8n only on IPv4 loopback and sets both the container and
n8n workflow timezone to `Africa/Lagos`. The named volume stores the SQLite
database, instance settings and credential encryption key. Use
`docker compose logs --tail=100 n8n` to diagnose startup and
`docker compose down` to stop the stack while keeping its data. Preserve
the volume when recreating the container and back it up before upgrades.
[n8n Docker setup](https://docs.n8n.io/hosting/installation/docker/)

## Fictional Lead Capture fixtures

| Payload | Intended test |
| --- | --- |
| [lead.example.json](../samples/lead.example.json) | Valid lead with all five scaffold fields |
| [invalid.json](../samples/lead-capture/invalid.json) | Rejection for a malformed email |
| [duplicate.json](../samples/lead-capture/duplicate.json) | Submit after the valid fixture to test email matching after trimming and lowercasing |
| [destination-error.json](../samples/lead-capture/destination-error.json) | Fresh valid lead to submit with the Sheets destination deliberately misconfigured |

The error fixture is valid on its own. Trigger the failure by using an
inaccessible test spreadsheet or a deliberately incorrect test sheet ID.

## Account setup for the owner

- **Google Sheets.** Sign in with a Google account you can use for testing.
  Create a dedicated test spreadsheet. In a test Google Cloud project, enable
  the Google Sheets and Google Drive APIs and configure OAuth consent. If
  the app is External and in Testing, add your Google account as a test user.
  Create a Web application OAuth client and copy the exact redirect URL from
  the local n8n Google Sheets credential into the client's authorized redirect
  URIs. Enter the client ID and secret directly in n8n, then select **Sign in
  with Google** and approve access with the account that can edit the test
  spreadsheet. [n8n Google OAuth setup](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)
- **Notifications.** Gmail is a proposed test destination. If approved for
  M1, enable the Gmail API in the test Google Cloud project, create a Gmail
  OAuth2 credential in n8n, and authorize it with a test sender account.
  Choose a test recipient inbox you control. Keep the synthetic lead email
  addresses in the fixtures as data. [n8n Google OAuth setup](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)

Keep client secrets, OAuth tokens and account data out of the repository.
