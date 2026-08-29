# Validate email deliverability via DNS MX records over a webhook

**Validate email addresses for free — no paid verification service, no API key, no credentials.** This workflow exposes a webhook that checks whether an email's domain can actually receive mail by resolving its **MX records over DNS-over-HTTPS**, and returns a clean JSON verdict.

## Who's it for

Anyone pre-screening emails before they enter a funnel — sign-up and lead forms, CRM enrichment, list cleaning — to drop typo, parked, and fake domains early. It uses only **core nodes**, so it runs on n8n Cloud and self-hosted.

## How it works

* The **Webhook** accepts an address as `?email=` (GET) or a JSON body.
* A **syntax gate** requires one `@` and a dotted domain, else it returns `400`.
* **Google DNS-over-HTTPS** looks up the domain's MX records.
* If Google times out or errors, it **automatically falls back to Cloudflare** DoH.
* It responds `200` with `valid: true/false`, a `reason`, and which resolver answered.

## How to set up

1. Import the workflow.
2. Open the **Webhook (email in)** node and copy its Production URL.
3. Call it, e.g. `GET /webhook/email-validation?email=jane@acme.com`.
4. Activate the workflow.

## Requirements

* An n8n instance (Cloud or self-hosted). **No credentials or paid API needed** — Google and Cloudflare DoH are free public endpoints.

## How to customize the workflow

Add an **A-record fallback** for domains with no MX, filter **disposable or role-based** addresses against a block-list before the DNS step, or reshape the response into your own schema. Note: MX presence proves the *domain* accepts mail, not that the exact mailbox exists.
