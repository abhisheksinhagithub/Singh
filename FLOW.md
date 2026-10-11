# Multiflow — Complete Website Flow

This is the full click-through journey of the site, in order — what a visitor sees, and what happens at each step.

---

## PART 1 — Marketing site (public, no login needed)

**Entry point: `index.html` (Home)**
- Hero: "One Platform. Multiple Possibilities." + animated flow-lines graphic branching into WhatsApp/SMS/RCS/Voice/Email
- "Book a Demo" and "Get Started" buttons in the nav
- Key features grid (all 9 products, one card each)
- "Why Multiflow" — stats (10M+ messages, 98.7% delivery, etc.)
- Industries grid — 8 cards, each links to that industry's anchor on Solutions page
- Testimonials
- FAQ accordion (click a question, it expands)
- Bottom CTA band → Book a Demo / WhatsApp click-to-chat
- Floating WhatsApp button (bottom-right, every page)

**Nav bar (same on every marketing page):** Home · Products · Solutions · Company · Resources · Contact | **Login** | **Get Started**

→ Clicking **Products** goes to `products.html`: detailed breakdown of all 9 products (WhatsApp API, Bulk WhatsApp, SMS, RCS, Voice, Email, AI Chatbot, Automation, API/Webhooks)

→ Clicking **Solutions** goes to `solutions.html`: 8 industry cards (Education, Real Estate, E-commerce, Healthcare, Finance, Restaurants, Agencies, SMB)

→ Clicking **Company** goes to `company.html`: mission, vision, why us, story

→ Clicking **Resources** goes to `blog.html`: guide/playbook listing (placeholder articles)

→ Clicking **Contact** goes to `contact.html`: lead form + business enquiry form + newsletter signup + direct contact (email/phone/WhatsApp)

→ Clicking **Login** goes to `login.html`
→ Clicking **Get Started** goes to `signup.html`

---

## PART 2 — Getting an account (public → app)

**`signup.html` — 4-step wizard**
1. **Account** — name, work email, password, mobile number
2. **Business details** — registered business name, business type, industry, GSTIN (optional), PAN, website, full address
3. **WhatsApp & channel setup** — WhatsApp number to onboard, display name, Facebook Business Manager ID (optional), expected monthly volume, primary use case, which channels to enable (WhatsApp is default, checkboxes for SMS/RCS/Voice/Email)
4. **Plan & review** — pick Starter/Growth/Enterprise, agree to terms, submit

→ On submit: account is created with status **"pending verification"** → redirects to `login.html` with a success banner

**`login.html`**
- Email + password fields
- Demo shortcuts: "Sign in as demo business" / "Sign in as admin"
- On success: business accounts → `dashboard.html` · admin accounts → `admin.html`

---

## PART 3 — Customer dashboard (`dashboard.html`)

Sidebar nav, always visible: **Overview · Inbox · Contacts · Templates · Campaigns · Analytics · Billing · Settings**, plus a live **channel status rail** (WhatsApp/SMS/RCS/Voice/Email health dots) at the bottom of the sidebar.

If the account is still pending verification, an orange banner shows at the top of every view: *"Your business verification is in progress..."*

- **Overview** — 4 stat cards (messages sent, delivery rate, active contacts, credits remaining), a 7-day delivery-rate chart, recent activity feed
- **Inbox** — WhatsApp-style live chat: conversation list on the left (unread badges, channel dot), chat thread on the right with message bubbles, quick-reply buttons, and a working text box — click a contact, read the thread, type and send a reply
- **Contacts** — table of all contacts with tag (Customer/Lead) and preferred channel
- **Templates** — grid of message templates, each tagged Approved/Pending/Rejected/Draft
- **Campaigns** — table of past/running/scheduled campaigns. Click **"+ New campaign"** to open the 5-step wizard:
  1. Name + choose channel
  2. Choose audience (all contacts / customers / leads / CSV upload)
  3. Choose an approved template (only shows templates approved *for that channel*)
  4. Send now or schedule for later
  5. Review summary → **Launch** → new campaign appears instantly in the table
  - Click **"View report"** on any campaign row → funnel chart (Sent → Delivered → Read → Replied, with % bars) + a 24-hour cumulative delivery line chart
- **Analytics** — volume-by-channel bar chart, delivery-rate trend line chart, channel health grid
- **Billing** — current credit balance, current plan, "Add credits" button, invoice history table
- **Settings** — business profile (all signup details displayed), connected channels list with "Configure" buttons, API key + webhook URL

---

## PART 4 — Admin / reseller console (`admin.html`)

Sidebar nav: **Overview · Verifications · All customers · Revenue · Support · Platform settings**

- **Overview** — total customers, pending verifications, approved & live, messages processed this month, 7-day platform-wide messaging chart
- **Verifications** — every pending signup shown as a card with all submitted details (business name, WhatsApp number, GSTIN, PAN, plan, volume, contact email) and **Approve** / **Reject** buttons. Approving flips their status live — if you then log in as that business, the pending banner is gone
- **All customers** — full table of every account: business, industry, plan, WhatsApp number, status, signup date
- **Revenue** — MRR, paying customers, churn, average revenue/customer, plan distribution chart
- **Support** — support ticket table (customer, topic, priority, status)
- **Platform settings** — wholesale rate table per channel (provider cost vs. customer rate vs. margin) and upstream provider credentials (Meta token, SMS aggregator key, email provider key)

---

## The full loop, end to end

```
Visitor lands on Home
   → browses Products / Solutions / Company / Blog
   → clicks Get Started
   → fills 4-step signup wizard
   → account created as "pending verification"
   → redirected to Login
   → logs in → sees Dashboard with pending banner, limited trust
   → (meanwhile) Admin logs in → Verifications tab → reviews their
     business docs → clicks Approve
   → Business logs in again → banner is gone, fully active
   → Uses Inbox to chat with a customer
   → Builds a Campaign (audience + template + schedule) → Launches it
   → Opens the Report to see delivery/read/reply funnel
   → Checks Analytics for channel-wide performance
   → Checks Billing for credits/invoices
```

---

## What's real vs. what's simulated (important)

**Genuinely working right now** (all client-side, in your browser):
- Every page, nav, form validation, animation
- Signup → pending → admin approval → live dashboard (via `localStorage`)
- Chat inbox (in-memory replies), campaign wizard, reports/funnels

**Not yet real** (needs backend work):
- No shared database — data lives only in your browser, not across users/devices
- No actual WhatsApp/SMS/RCS/Voice/Email is sent — channel integrations aren't connected
- Contact form shows a success message but doesn't send anywhere yet
