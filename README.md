# Multiflow — complete website (WhatsApp Marketing + Automation launch)

Production-structured build of the full Multiflow platform: public marketing
site, working signup/login (with email OTP + password reset), a complete
client dashboard, and an admin console — focused on the two launch products:
**WhatsApp Marketing** and **WhatsApp Automation** (SMS, RCS, Voice, Email
are shown as "coming soon").

**Zero-setup demo mode:** everything runs on browser `localStorage` so every
flow works immediately by opening the files. Swap in the included Supabase
backend when going live (see below).

## Open it

Open `index.html` in a browser. For best results serve over http:
`npx serve .`

## Demo accounts

- `demo@business.com` / `demo1234` — individual business (approved)
- `demo@agency.com` / `demo1234` — reseller (approved, has a Clients tab + 3 sample clients)
- `admin@multiflow.co.in` / `admin123` — admin console

## The complete loop

1. **Signup** (`signup.html`) — 4-step wizard (Individual vs Reseller, email OTP `123456`, Silver/Gold/Platinum/Diamond plan) → account created as **pending verification**
2. **Admin** (`admin.html`) — Verifications tab shows the new signup → Approve/Reject
3. **Login** (`login.html`) — tabs, password reset flow (OTP `123456`), demo shortcuts
4. **Dashboard** (`dashboard.html`) — full client panel:
   - **WhatsApp**: Overview, Templates (create → Pending review), Campaigns (5-step wizard with Marketing/Utility category → launch → funnel report), Contacts (add), Inbox (live chat), Catalog
   - **Automation**: Overview, Workflows (create/pause), AI Assistant, Execution Logs
   - **Analytics**: Overview charts, Campaign/Message/Agent reports
   - **Reseller** (agency accounts only): Clients tab — add/suspend sub-accounts
   - **Team**: Members (invite), Roles & Permissions
   - **Developers**: API keys, Webhooks, Integrations
   - **Billing**: Credits, Recharge (Marketing/Utility packs + Automation plans — mirrors pricing page), Transactions, GST Invoices
   - **Workspace**: Notifications, Activity logs, Help & Support (raise ticket), Settings (saves your name/phone for real)
5. Fully responsive — collapsible sidebar on mobile/tablet.

## Pricing model (pricing.html)

- WhatsApp **Marketing** packs (one-time): 10K ₹8,600 · 50K ₹41,000 · 1L ₹80,000
- WhatsApp **Utility** packs (one-time): 10K ₹3,000 · 50K ₹9,000 · 1L ₹15,000
- **Automation** subscription (monthly): Starter ₹999 · Growth ₹1,999 · Pro (AI) ₹3,999
- Combined bundles with first-month totals, comparison table, FAQ

## Going live (real backend)

`assets/supabase-client.js` + `supabase/schema.sql` are included. Steps:
1. Create a Supabase project, run `supabase/schema.sql`
   (fix note: replace the admin-read RLS policy on `profiles` with a
   `security definer is_admin()` helper to avoid recursion, and column-restrict
   the owner-update policy on `businesses` so customers can't set their own status)
2. Put the project URL + anon key in `assets/supabase-client.js`
3. Swap `assets/app.js` for `assets/supabase-client.js` in the four app pages
4. Connect Meta WhatsApp Cloud API + Razorpay on the backend for real
   messaging and payments

## What's real vs demo

Working with persistence (localStorage): signup → OTP → pending → admin
approve → login → dashboard; password reset; reseller clients; account
settings. Interactive with sample data: campaigns, templates, inbox,
automation, analytics, billing. No real messages are sent and no real
payments are taken in demo mode.
