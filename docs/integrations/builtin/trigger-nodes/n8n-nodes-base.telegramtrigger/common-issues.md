---
#https://www.notion.so/n8n/Frontmatter-432c2b8dff1f43d4b1c8d20075510fe4
title: Telegram Trigger node common issues
description: Documentation for common issues and questions in the Telegram Trigger node in n8n, a workflow automation platform. Includes details of the issue and suggested solutions.
contentType: integration
priority: critical
---

# Telegram Trigger node common issues

Here are some common errors and issues with the [Telegram Trigger node](/integrations/builtin/trigger-nodes/n8n-nodes-base.telegramtrigger/) and steps to resolve or troubleshoot them.

## Stuck waiting for trigger event

When testing the Telegram Trigger node with the **Test step** or or **Test workflow** buttons, the execution may appear stuck and unable to stop listening for events. If this occurs, you may need to exit the workflow and open it again to reset the canvas.

Stuck listening events often occur due to issues with your network configuration outside of n8n. Specifically, this behavior often occurs when you run n8n behind a reverse proxy without configuring websocket proxying.

To resolve this issue, check your reverse proxy configuration (Nginx, Caddy, Apache HTTP Server, Traefik, etc.) to enable websocket support.

<!-- vale off -->
## Bad request: bad webhook: An HTTPS URL must be provided for webhook
<!-- vale on -->

This error occurs when you run n8n behind a reverse proxy and there is a problem with your instance's webhook URL.

When running n8n behind a reverse proxy, you must [configure the `WEBHOOK_URL` environment variable](/hosting/configuration/configuration-examples/webhook-url/) with the public URL where your n8n instance is running. For Telegram, this URL must use HTTPS.

To fix this issue, configure TLS/SSL termination in your reverse proxy. Afterward, update your `WEBHOOK_URL` environment variable to use the HTTPS address.