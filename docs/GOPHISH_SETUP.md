# Gophish Setup Guide

## What is Gophish?

Open-source phishing framework for security awareness testing. Runs via Docker Compose with an admin panel and phishing server.

## Prerequisites

- Docker and Docker Compose
- Google account with **App Password** enabled:
  1. Enable 2FA on your Google account
  2. Go to https://myaccount.google.com/apppasswords
  3. Generate an app password for "Mail"

## Quick Start

```bash
# Start
docker compose up -d

# Get initial password
docker compose logs | grep "Please login"

# Stop
docker compose down
```

## Access

- **Admin Panel**: http://localhost:3333
- **Phishing Server**: http://localhost:80

## First Steps

1. Login and **change default password**
2. Configure SMTP settings (Settings → Sending Profiles):
   - **Name**: Gmail SMTP
   - **Host**: smtp.gmail.com:587
   - **Username**: your.email@gmail.com
   - **Password**: your-app-password (not regular password)
   - **From**: your.email@gmail.com
   - Enable "Use TLS"
3. Create email template (Email Templates)
4. Create landing page (Landing Pages)
5. Add target users (Users & Groups)
6. Launch campaign (Campaigns)

## Local Testing with MailHog

For fully local testing without external email servers, use MailHog to catch all emails.

### Configuration

**SMTP Settings in Gophish:**
- **Name**: MailHog Local
- **Host**: mailhog:1025 (or localhost:1025 if running outside Docker)
- **Username**: (leave empty)
- **Password**: (leave empty)
- **From**: test@example.com
- **Disable TLS**

**Access MailHog Web UI**: http://localhost:8025

All emails sent by Gophish will be captured in MailHog instead of being sent to real addresses.

## Important

- Get authorization before testing
- Change default credentials immediately
- Use Google App Password, not your regular password
- Keep isolated from production networks

## Troubleshooting

```bash
docker compose logs -f        # View logs
docker compose restart        # Restart
docker compose down -v        # Full cleanup
```