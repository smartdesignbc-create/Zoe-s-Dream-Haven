# Zoe's Dream Haven — Operations Dashboard

A single-page business dashboard for Zoe's Dream Haven: inventory, sales, receipts, delivery notes, customers, suppliers, reports, and staff login access — all in one lightweight `index.html` file.

## What's in this version

- **Top tab-bar navigation** — everything readable top to bottom, no side menu to open. Primary tabs (Dashboard, Sales, Inventory, Receipts, Deliveries, Customers) sit up front; Suppliers, Reports, Team & Access, and Settings live under **More**.
- **Simplified Dashboard** — only the numbers that matter day to day (Today's Sales, Pending Deliveries, Low Stock), 3 quick actions, recent sales, and alerts. Deeper stats and charts moved to **Reports**.
- **Delivery Notes** — every delivery captures customer name, surname, cell number, and address, and produces a printable Delivery Note with signature lines. Create one directly from a Receipt with one click.
- **Login screen** — the whole app is gated behind sign-in. See **Login & Access** below.
- **Full data flow** — a sale deducts stock, saves/updates the customer, generates a receipt, and can spin off a linked delivery note.
- **Toast notifications** — no browser pop-ups; confirmations and errors appear as clean on-screen messages.

## Login & Access (current state — demo mode)

This build includes a **working login screen**, but accounts are currently stored in memory in the browser (they reset on page refresh). This is intentional — it's the UI and flow the client approved, ready to be wired to real, permanent accounts.

**Demo login:**
- Email: `admin@demo.com`
- Password: `admin123`

**How it will work once connected to Supabase (next phase):**
1. You keep a permanent developer/support login, separate from the client's.
2. At handover, you use **Settings → Change Login Details** to switch the owner-level account to the client's own email and password, in front of them.
3. From **Team & Access**, the owner can add staff members (each gets a temporary password to share), reset anyone's password, or remove access — all without your involvement.
4. Your own login stays active permanently, so you can log in and confirm any issue the client reports before touching any code.

See `DEPLOYMENT.md` for the full rollout plan, including the Supabase phase.

## Tech notes

- Single file: `index.html` — no build step, no dependencies. Works as-is on GitHub Pages, Vercel, Netlify, or any static host.
- All data (products, sales, customers, receipts, deliveries, staff accounts) currently lives in memory in the browser and resets on refresh. This is expected at this stage — persistent storage (Supabase) is the next phase.
- Branding, colors, and business name are unchanged from the version the client approved.

## Project structure

```
index.html      → the entire application (HTML + CSS + JS)
README.md       → this file
DEPLOYMENT.md   → step-by-step rollout: GitHub → Vercel → Supabase
```
