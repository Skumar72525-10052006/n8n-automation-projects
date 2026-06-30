# n8n Automation Projects

A collection of working automation systems I built using n8n and AI agents during my AI internship at Mirai School of Technology (Jan–Feb 2026). Each project solves a real workflow problem — lead scoring, appointment booking, calendar management, query routing — using AI agents, conditional logic, and integrations with Google Calendar, Google Sheets, Gmail, and Telegram.

I build by working with AI tools directly: prompting, agentic IDEs, and iterative testing inside n8n. That doesn't mean I skip the fundamentals — every workflow here has custom logic underneath it (ID generation rules, lead-scoring conditions, duplicate-prevention checks, anti-loop safety) that I designed and debugged myself. AI tools help me move fast. Understanding the system is what makes the result actually work.

All projects below were built solo.

## Projects

| Project | What it does | Folder |
|---|---|---|
| [Smart Lead Qualification System](./smart-lead-qualification-system) | Scores incoming leads as HOT / WARM / COLD based on budget and urgency, then routes each to a different automated email + internal alert flow | `/smart-lead-qualification-system` |
| [Developer Portfolio Query Bot](./developer-portfolio-query-bot) | AI-powered query handler that answers technical questions, logs every inquiry to Google Sheets, and redirects collaboration/job inquiries appropriately | `/developer-portfolio-query-bot` |
| [Calendar Booking Agent](./calendar-booking-agent) | Converts natural language requests like "block tomorrow at 2 PM" into structured Google Calendar events | `/calendar-booking-agent` |
| [Physio Appointment System](./physio-appointment-system) | A full clinic appointment booking system with automatic patient ID generation and duplicate-prevention rules — built four times across different interfaces and AI providers | `/physio-appointment-system` |

## Why four versions of the same appointment system?

The `physio-appointment-system` folder contains the same core booking logic deployed across four different surfaces:

1. **Web chat** — the original version, built for a browser-based chat trigger
2. **Lovable webhook** — adapted to work behind a webhook so it could power a custom frontend built with Lovable, including a patient lookup step the original didn't have
3. **Telegram (OpenAI)** — rebuilt for Telegram, with added anti-loop safety logic so the bot never responds to its own messages
4. **Telegram (Google Gemini)** — the same Telegram version, with the underlying LLM swapped from OpenAI to Google Gemini without breaking the booking logic

Building the same system four times wasn't about repetition — each version forced a different constraint (webhook response handling, anti-loop logic, provider-agnostic prompt design) that taught me something the previous version didn't.

## Tools used across these projects

n8n · OpenAI API · Google Gemini API · Google Calendar API · Google Sheets API · Gmail API · Telegram Bot API · JavaScript (Code nodes) · Lovable

## About me

Sonu Kumar — Diploma in Computer Science and Technology, Behala Government Polytechnic (completed June 2026, results awaited). Currently UI/UX Design Intern at FlyRank AI (FlyRank AI Internship Program, starting July 1, 2026).

[LinkedIn](https://www.linkedin.com/in/sonu-kumar-7003a5325) · Kolkata, West Bengal, India
