# Case Study: Calendly → Notion CRM + Auto-Onboarding — 6 APIs, One Workflow

**Client Type:** Coach / Agency / SaaS — 10 bookings/week, manual onboarding 15 min each
**Timeline:** 1.5 hours
**Tools:** Calendly API (Webhook), Notion API, Gmail API, Calendar API, Slack API, Sheets API, Gemini API, Make.com, n8n, MCP
**Cost to Run:** $0/month free tiers

### Problem
Client books on Calendly → Founder manually copies to Notion CRM → writes generic welcome email → creates calendar event → alerts team on Slack → logs in Sheets. 15 min per booking × 10/week = 2.5 hrs/week copy-paste. Forgets Notion page, sends generic email, misses Slack alert.

### Solution
Built 6-API orchestration:
1. Trigger: Calendly Invitee Created Webhook (Calendly API)
2. Transform: Notion Create Database Page (Notion API) + Gemini personalized welcome email mentioning goal (Gemini API + MCP)
3. Deliver: Gmail welcome email (Gmail API) + Calendar event (Calendar API) + Slack #onboarding alert (Slack API) + Sheets log (Sheets API)

**Flow:** Calendly Webhook → Notion CRM Page → Gemini Personalized Email → Gmail + Calendar + Slack + Sheets

### Results
- Time: 15 min/booking → 0 min, 2.5 hrs/week saved
- Errors: 0 — no forgotten Notion page, no generic email
- Experience: Personalized welcome mentioning goal — feels premium
- Tracking: Sheets log + Notion CRM with status

### What Client Gets
- Working scenario + n8n workflow + blueprint
- Loom walkthrough: how to edit Notion properties, change email copy, add new event types, adjust Slack channel
- Documentation: How to swap Forms mock to real Calendly webhook, how to get Notion Database ID + Token
- 7 days support

### Tools & Cost
- Calendly API free (webhooks), Notion API free, Gmail free, Calendar free, Slack free, Sheets free, Gemini free tier, Make.com free, n8n free
- Running cost $0

### Why Premium
Every coach/agency/SaaS has Calendly + Notion + Gmail. They all manually onboard. Shows you connect 6 APIs in one workflow — API orchestration + MCP — founders searching "Calendly Notion automation" pay $300-500.

---
Demo: [Add Link] | Portfolio: github.com/aiagentbuilderhq/automation-portfolio
