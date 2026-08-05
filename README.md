# Zoe's Dream Haven — Operations Dashboard

A complete, cloud-backed business dashboard for Zoe's Dream Haven: inventory across two locations, sales, lay-bys, VAT-compliant PDF receipts, deliveries, customers, suppliers, reports, and secure link-based access — all in one `index.html` file, fully connected to a live Supabase backend.

## What this system does

- **Two-location Inventory** — Main Shop (where all supplier stock arrives) and a separate Warehouse, with one-click stock transfers between them, fully logged.
- **Pricing engine** — enter Trade Price + Markup, and Selling Price, VAT, and Total Selling Price calculate automatically. No manual math anywhere.
- **Sales** — full item cart, manual price override per line, VAT numbers for both the business and the customer, auto-updates inventory, auto-creates the customer record, auto-generates a receipt.
- **Lay-by Sales** — a simple checkbox on the Sales screen. Takes a deposit, holds stock until fully paid, accepts top-up payments, and completes automatically the moment the balance hits zero.
- **Receipts** — every receipt (sales, lay-by deposits/payments, completed lay-bys) can be **Printed**, **Downloaded as a PDF**, or **Shared on WhatsApp** — see "Receipts: Print, Download, WhatsApp" below for exactly how each works.
- **VAT Numbers** — the business's own VAT number is set once under Settings and prints on every receipt automatically. Each customer's VAT number is entered right on the Sales screen, saved to their record, and auto-fills next time they buy again.
- **Delivery Notes** — pull straight from a sale or lay-by, complete with customer details and a printable note with signature lines.
- **Reports** — leads with today's Completed Sales, Lay-by Deposits Received, and Completed Lay-bys, plus an all-time overview, trends, and stock alerts.
- **Secure, permanent login** — see "Access & Security" below.

## Receipts: Print, Download, WhatsApp

- **Print** — opens the normal print dialog, same as printing anything else.
- **Download PDF** — saves a proper, VAT-compliant PDF receipt to the device. To email a receipt, download it here and attach it in your own email as usual — there's no automatic email sending built in, by design (kept simple, no extra accounts needed).
- **Share on WhatsApp** — on a phone, this hands the PDF straight to WhatsApp in one tap. On a laptop (using WhatsApp Web/Desktop), it downloads the PDF **and** opens WhatsApp directly on that customer's chat — the only manual step left is attaching the file that just downloaded and hitting send. (No website is allowed to auto-attach and send a WhatsApp message for you — that's a deliberate WhatsApp security rule, not a limitation of this app.)

## Access & Security

This system uses a **Master + Share Access** model, not usernames/passwords handed out manually:

- **You (the developer) are the permanent Master account.** Full control, always. You're the only one who can grant or revoke access.
- To give someone access (the shop owner, staff, anyone), go to **More → Share Access → Generate Share Link**, and send that link however you like.
- The moment they open it, they set up their **own** name, email, and password and are instantly logged in — no email confirmation step, no waiting.
- You can revoke anyone's access at any time from the same screen.
- Nobody sees "Owner" or "Staff" labels — it's simply people with access, managed by you.

This means: if a client calls with a problem, you don't need them to grant you anything — you already have permanent access and can log in and check it yourself immediately.

## Tech stack

- Single file: `index.html` — no build step. Deploys as-is to Vercel, Netlify, GitHub Pages, or any static host.
- **Supabase** — Postgres database, Auth, and Edge Functions power everything. All data is real and permanent.
- **jsPDF** (via CDN) generates receipts client-side.
- Row Level Security is enabled on every table — only signed-in accounts can read or write data.

## Project structure

```
index.html   → the entire application (HTML + CSS + JS), connected to Supabase
README.md    → this file
```

## Supabase project

- Project: `zoes-dream-haven`
- Tables: `settings`, `profiles`, `suppliers`, `products`, `customers`, `sales`, `receipts`, `deliveries`, `stock_transfers`, `laybys`, `layby_payments`, `invites`
- Edge Functions: `redeem-invite`, `manage-staff` (both actively used). `send-receipt-email` and `send-receipt-whatsapp` were built earlier for a fully automated send option and remain deployed but unused — safe to ignore, or revisit later if a business domain and WhatsApp Business API get set up down the line.
