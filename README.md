# Zoe's Dream Haven — Operations Dashboard

A complete, cloud-backed business dashboard for Zoe's Dream Haven: inventory across two locations, sales, lay-bys, PDF receipts, deliveries, customers, suppliers, reports, and secure link-based access — all in one `index.html` file, fully connected to a live Supabase backend.

## What this system does

- **Two-location Inventory** — Main Shop (where all supplier stock arrives) and a separate Warehouse, with one-click stock transfers between them, fully logged.
- **Pricing engine** — enter Trade Price + Markup, and Selling Price, VAT, and Total Selling Price calculate automatically. Nobody does this math by hand.
- **Sales** — full item cart, manual price override per line (with the original price kept for records), auto-updates inventory, auto-creates the customer record, auto-generates a receipt.
- **Lay-by Sales** — a simple checkbox on the Sales screen. Takes a deposit, holds stock until fully paid, accepts top-up payments, and completes automatically (deducting stock and generating the final receipt) the moment the balance hits zero.
- **PDF Receipts** — every receipt (sales, lay-by deposits/payments, completed lay-bys) can generate a real downloadable PDF, with full business and customer details, VAT breakdown, and line items — nothing retyped.
- **Email / WhatsApp Receipt buttons** — built and wired to real backend functions, ready to go live the moment a production email/WhatsApp account is connected (see "Going Live" below).
- **Delivery Notes** — pull straight from a sale or lay-by, complete with customer details and a printable note with signature lines.
- **Reports** — leads with today's Completed Sales, Lay-by Deposits Received, and Completed Lay-bys, plus an all-time overview, trends, and stock alerts.
- **Secure, permanent login** — see "Access & Security" below.

## Access & Security

This system uses a **Master + Share Access** model, not usernames/passwords handed out manually:

- **You (the developer) are the permanent Master account.** Full control, always. You're the only one who can grant or revoke access.
- To give someone access (the shop owner, staff, anyone), go to **More → Share Access → Generate Share Link**, and send that link however you like (WhatsApp, SMS, etc.).
- The moment they open it, they set up their **own** name, email, and password and are instantly logged in — no email confirmation step, no waiting.
- You can revoke anyone's access at any time from the same screen.
- Nobody sees "Owner" or "Staff" labels — it's simply people with access, managed by you.

This means: if a client calls with a problem, you don't need them to grant you anything — you already have permanent access and can log in and check it yourself immediately.

## Tech stack

- Single file: `index.html` — no build step. Deploys as-is to Vercel, Netlify, GitHub Pages, or any static host.
- **Supabase** — Postgres database, Auth, and two Edge Functions (`redeem-invite`, `manage-staff`) power everything. All data is real and permanent.
- **jsPDF** (via CDN) generates receipts client-side — no server needed for that part.
- Row Level Security is enabled on every table — only signed-in accounts can read or write data.

## Going live with Email / WhatsApp receipts

Both buttons work end-to-end already — they just need real credentials plugged in as Supabase secrets (no code changes required):

- **Email:** create a free [Resend.com](https://resend.com) account → add `RESEND_API_KEY` as a secret on the `send-receipt-email` function.
- **WhatsApp:** create a Twilio account with WhatsApp enabled → add `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`, `TWILIO_WHATSAPP_FROM` as secrets on the `send-receipt-whatsapp` function.

Until then, clicking either button shows a clear message explaining what's needed — never a fake "sent" confirmation.

## Project structure

```
index.html   → the entire application (HTML + CSS + JS), connected to Supabase
README.md    → this file
```

## Supabase project

- Project: `zoes-dream-haven`
- Tables: `settings`, `profiles`, `suppliers`, `products`, `customers`, `sales`, `receipts`, `deliveries`, `stock_transfers`, `laybys`, `layby_payments`, `invites`
- Edge Functions: `redeem-invite`, `manage-staff`, `send-receipt-email`, `send-receipt-whatsapp`
