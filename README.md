# Project 7: Calendly → Notion CRM + Auto-Onboarding Sequence (Make.com + n8n + MCP + API Orchestration)

> **One-liner:** When someone books on Calendly, Notion CRM page is created, Google Calendar event confirmed, Gemini writes personalized welcome email, Gmail sends it, Slack alerts team, Sheets logs — onboarding time 1 hour → 5 minutes.

[![Calendly API](https://img.shields.io/badge/Calendly%20API-Booking%20Webhook-blue)](https://developer.calendly.com)
[![Notion API](https://img.shields.io/badge/Notion%20API-CRM%20Database-black)](https://developers.notion.com)
[![Gmail API](https://img.shields.io/badge/Gmail%20API-Welcome%20Email-red)](https://developers.google.com/gmail/api)
[![Gemini](https://img.shields.io/badge/Gemini%20API-Personalized%20Welcome-blue)](https://aistudio.google.com)
[![Make.com](https://img.shields.io/badge/Make.com-Automation-blue)](https://make.com)
[![n8n](https://img.shields.io/badge/n8n-Workflow-red)](https://n8n.io)
[![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-purple)](https://modelcontextprotocol.io)

**Live Hub:** [automation-portfolio](https://github.com/aiagentbuilderhq/automation-portfolio) | **Other Projects:** [Sheets → Gmail](https://github.com/aiagentbuilderhq/sheets-gmail-automation) · [Shopify Cart Recovery](https://github.com/aiagentbuilderhq/shopify-cart-recovery) · [RAG Bot](https://github.com/aiagentbuilderhq/rag-telegram-bot) · [AI Inbox](https://github.com/aiagentbuilderhq/ai-inbox-assistant)

## 🎯 Problem Founders Face (Coaches, Agencies, SaaS — Manual Onboarding Kills Time)

- Client books on Calendly → Founder manually copies name/email to Notion CRM → manually creates welcome email → manually creates calendar event → manually alerts team on Slack → manually logs in Sheets
- **Time:** 15 min per booking × 10 bookings/week = 2.5 hrs/week on copy-paste
- **Errors:** Forgets to create Notion page, sends generic welcome email, misses Slack alert, double-books
- **No personalization:** Generic "Thanks for booking" email, not mentioning their business or goal

## ✅ Solution — Calendly Webhook → Notion + Gmail + Calendar + Slack + Sheets + Gemini (6 APIs, One Workflow)

**Make.com / n8n Flow:**

1. **Trigger — Calendly Booking Webhook (Calendly API)**
   - Calendly → Integrations → Webhooks → Create Webhook → Event: Invitee Created → URL: Make.com/n8n Webhook URL
   - Free Demo for Portfolio: Use Google Forms mock + Webhook (if no Calendly account) — same pattern, swap to Calendly webhook for real client

2. **Transform — Create Notion CRM Page + Generate Personalized Welcome Email (MCP + LangChain)**
   - Notion API → Create Database Page → Database: Client CRM → Properties: Name, Email, Booking Date, Goal, Status = New
   - Gemini API → Prompt: "You are onboarding specialist for [Coach/Agency]. Client: {{Name}} booked {{Event Type}} on {{Date}} for goal: {{Goal from Calendly questions}}. Write personalized welcome email: mention their name, their goal, what to prepare, calendar link, excited tone. Output: SUBJECT: [subject] | BODY: [body]" — MCP: Model (Gemini) + Context (Booking data from Calendly API + Notion) + Protocol (Gmail + Slack)

3. **Deliver — Multi-Channel Onboarding**
   - Gmail API → Send personalized welcome email to client
   - Google Calendar API → Create calendar event with client details (if not already created by Calendly)
   - Slack API → Post to #sales or #onboarding: "🎉 New booking: {{Name}} ({{Email}}) — {{Event Type}} on {{Date}} — Goal: {{Goal}} — Notion CRM created, welcome email sent"
   - Sheets API → Log to `Onboarding Log`: Name, Email, Booking Date, Event Type, Notion Page URL, Email Sent At

**Architecture:**
```
[Calendly Webhook: Invitee Created — Calendly API + Webhook]
        ↓
[Notion: Create Database Page — Notion API — CRM with Name, Email, Booking Date, Goal]
        ↓
[Gemini: Generate Personalized Welcome Email — Gemini API + MCP + LangChain]
Prompt: "Client {{Name}} booked {{Event Type}} for goal {{Goal}}. Write personalized welcome email"
        ↓
[Router]
  ├─→ [Gmail: Send Welcome Email — Gmail API — Personalized]
  ├─→ [Google Calendar: Create Event — Calendar API — Optional if Calendly already did]
  ├─→ [Slack: Alert #onboarding — Slack API — Booking details + Notion link]
  └─→ [Sheets: Log Onboarding — Sheets API — Track onboarding]
```

**n8n Version:**
```
[Webhook Trigger: Calendly Booking] → [Notion Node: Create Page] → [AI Agent Node: Gemini Welcome Email + MCP] → [Gmail Node: Send Email] → [Slack Node: Alert Team] → [Sheets Node: Log] → [Calendar Node: Create Event]
```

## 📈 Results

- **Before:** 15 min per booking manual copy-paste × 10 bookings/week = 2.5 hrs/week
- **After:** 0 min manual — instant Notion page + personalized email + Slack alert + log
- **Time Saved:** 2.5 hrs/week + zero errors (no forgotten Notion page, no generic email)
- **Client Experience:** Personalized welcome email mentioning their goal — feels premium, not generic
- **Build Time:** 1.5 hours (both Make.com + n8n versions)

## 🛠️ Tools Used — Premium Founder-Searched Skills

- **APIs:** Calendly API (Webhook) · Notion API (Database) · Gmail API · Google Calendar API · Slack API · Google Sheets API · Gemini API · Groq fallback · Webhooks · REST/JSON
- **Automation:** Make.com · n8n (Webhook nodes, Notion nodes, AI Agent nodes) · Error Handling · Router
- **AI & Advanced:** MCP (Model Context Protocol) · LangChain pattern (Retrieve booking → Augment prompt → Generate email) · Prompt Engineering (personalized onboarding) · API Orchestration (6 APIs in one flow) · Human-in-the-loop (human reviews Notion page)
- **Why This Project Sells:** Every coach, agency, SaaS founder has Calendly + Notion + Gmail. They all manually onboard. This project shows you connect Calendly API + Notion API + Gmail API + Calendar API + Slack API + Sheets API + Gemini — 6 APIs, one workflow. Founders searching "Calendly Notion automation", "Notion API n8n", "auto onboarding", "MCP onboarding" want exactly this.

## 🎥 Demo Video Script (50 sec)

0-5s: Title: "Calendly → Notion CRM + Auto-Onboarding — 15 min/booking → 0 min — Make.com + n8n + Calendly API + Notion API + Gmail API + MCP"

5-15s: Show Trigger — Calendly Booking (Free Demo via Forms if no Calendly)
- Calendly booking page → Book test event: Test Client, test@client.com, Goal: Need automation for lead follow-up
- Explain: "For portfolio, Calendly webhook — free demo via Forms mock, same pattern"

15-35s: Show Multi-Channel Onboarding
- Make.com/n8n scenario run: Webhook → Notion Create Page → Gemini Generate Welcome Email → Gmail Send → Slack Alert → Sheets Log
- Show Notion CRM database: New page created with Name, Email, Booking Date, Goal, Status = New
- Show Gmail sent: Personalized welcome email: "Hi Test Client, excited for your goal: Need automation for lead follow-up — here's what to prepare..."
- Show Slack #onboarding: "🎉 New booking: Test Client — Need automation for lead follow-up — Notion CRM created, welcome email sent"
- Show Sheets log: Logged with Notion page URL

35-50s: Closer
- Static: "15 min per booking → 0 min — 6 APIs, one workflow — Calendly API + Notion API + Gmail API + Calendar API + Slack API + Sheets API + Gemini API + Make.com + n8n + MCP — API Orchestration + Personalized AI"

Upload: YouTube Unlisted

## 🚀 How To Build — Actual Steps (Free Stack)

**Free Demo Setup (No Paid Calendly Needed for Portfolio):**

1. **Create Notion CRM Database (10 min):**
   - Notion → New Page → Database → Table → Name: Client CRM → Properties: Name (Title), Email (Email), Booking Date (Date), Event Type (Select), Goal (Text), Status (Select: New, Onboarded, Closed), Notion Page URL (URL)
   - Copy Database ID: Open database → URL → Copy ID after last / and before ? — Save for API
   - Notion → Settings → Connections → Create integration → Name: CRM Automation → Copy Internal Integration Token → Share database with integration (Share → Add integration)

2. **Make.com Scenario (40 min):**
   - New Scenario → Webhooks → Custom Webhook → Create → Copy Webhook URL → This is your Calendly webhook URL (for real client, paste in Calendly → Integrations → Webhooks → Invitee Created)
   - For portfolio free demo: Add Google Forms → Watch Responses → Form: Booking Mock (Name, Email, Goal) → This mocks Calendly
   - Add Notion → Create a Database Item → Connection: Paste Notion Internal Integration Token → Database ID: Paste ID → Map Name, Email, Booking Date, Goal, Status = New
   - Add Gemini → Generate Text → Model: gemini-1.5-flash → Prompt:
     ```
     You are onboarding specialist for coach/agency. Client: {{Name}} booked {{Event Type}} on {{Date}} for goal: {{Goal}}. Write personalized welcome email: mention name, goal, what to prepare, calendar link, excited tone. Output: SUBJECT: [subject] | BODY: [body]
     ```
   - Add Gmail → Send an Email → To: {{Email}} → Subject: {{Gemini Subject}} → Body: {{Gemini Body}}
   - Add Slack → Create a Message → Channel: #onboarding → Message: `🎉 New booking: {{Name}} ({{Email}}) — {{Event Type}} on {{Date}} — Goal: {{Goal}} — Notion CRM: {{Notion Page URL}} — Welcome email sent`
   - Add Sheets → Add a Row → Sheet: Onboarding Log → Map fields + Notion Page URL
   - Run Once → Test with fake booking → Verify Notion page created + Gmail sent + Slack alert + Sheets logged
   - Screenshot: Make.com scenario + Notion page + Gmail sent + Slack alert + Sheets log

3. **n8n Version (30 min):**
   - n8n → New Workflow → Webhook Trigger → Copy URL → Use as Calendly webhook
   - Add Notion Node → Create Page → Database ID + Token → Map fields
   - Add AI Agent Node → Gemini → Same prompt
   - Add Gmail Node → Send Email → Map subject/body
   - Add Slack Node → Alert #onboarding
   - Add Sheets Node → Log
   - Activate → Test → Screenshot n8n workflow

4. **Real Calendly Swap (Explain in README):**
   - For real client: Replace Forms Watch Responses with Webhook Trigger → Calendly → Integrations → Webhooks → Create Webhook → Event: Invitee Created → URL: Your Make.com/n8n Webhook URL
   - Calendly API docs: https://developer.calendly.com/how-to-use-webhooks — same nodes, different trigger

**Total Build Time:** 1.5 hours portfolio proof (free stack)

## 💼 Client Pitch

> "Every booking you manually copy to Notion + email + Slack = 15 min. 10 bookings/week = 2.5 hrs/week on copy-paste. I automate: Calendly booking webhook → Notion CRM page created with goal → Gemini writes personalized welcome email mentioning their goal → Gmail sends it → Slack alerts team → Sheets logs. 15 min → 0 min, zero errors, personalized experience. Built with Calendly API + Notion API + Gmail API + Calendar API + Slack API + Sheets API + Gemini + Make.com + n8n + MCP — 6 APIs, one workflow. For portfolio, mocked via Forms, real client swap to Calendly webhook, same nodes. That's API orchestration + MCP — what founders searching 'Calendly Notion automation' want."

## 🔒 Security

- No API keys, fake data only, .gitignore blocks .env, Notion token never committed

## 📄 Case Study

See `case-study.md`

---
**Built by Isaac — aiagentbuilderhq | [Full Portfolio Hub](https://github.com/aiagentbuilderhq/automation-portfolio) | Tech: Make.com + n8n + Calendly API + Notion API + Gmail API + Calendar API + Slack API + Sheets API + Gemini API + Groq + MCP + Webhooks + API Orchestration**
