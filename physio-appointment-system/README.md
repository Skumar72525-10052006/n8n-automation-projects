# Physio Appointment System

A full clinic appointment booking system for "Dr. Strange Physiotherapy Clinic" — an AI receptionist agent that collects patient details, generates a unique patient ID, checks calendar availability against the clinic's actual scheduling rules, books the appointment, logs everything, and sends a structured confirmation email. No human receptionist has to touch any of it.

I built this same core system four times, each version solving a different deployment problem.

## The four versions

| Version | Interface | What's different |
|---|---|---|
| [`web-chat-version`](./web-chat-version) | Browser chat trigger | The original — conversational, asks the patient questions one at a time, waits for slot confirmation before booking |
| [`lovable-webhook-version`](./lovable-webhook-version) | Webhook (powers a Lovable-built website) | Non-conversational — receives a complete patient payload in one request, has to autonomously pick the best available slot with zero back-and-forth, and adds a "Fetch The Last Patient ID" lookup step the chat version didn't need |
| [`telegram-openai-version`](./telegram-openai-version) | Telegram bot, OpenAI | Rebuilt for Telegram messaging, with added anti-loop safety logic so the bot never replies to its own messages, and patient/appointment lookup tools for returning patients |
| [`telegram-gemini-version`](./telegram-gemini-version) | Telegram bot, Google Gemini | Identical booking logic to the OpenAI Telegram version, with the underlying LLM swapped to Google Gemini |

## What stayed consistent across all four

- **Patient ID format**: `PAT-YYYYMMDD-XXX`, generated once per patient and never regenerated
- **Clinic scheduling rules**: 9:00 AM–5:00 PM, 30-minute slots, no bookings between 1:00–2:00 PM, no weekends or public holidays
- **Strict execution rules**: patient details stored only once, appointment details stored only once after booking succeeds, confirmation email sent only once
- **Structured confirmation email**: a fixed field order (Patient ID, Name, Age, Gender, Mobile, Email, Issue, Booked Date, Booked Slot) followed by a clinic note and receptionist contact details
- **Privacy rules**: never leak another patient's data, never duplicate patient records, never repeat tool calls unnecessarily

## What changed and what it taught me

**Chat → Webhook (Lovable version):** The conversational version could ask a follow-up question if something was missing. The webhook version can't — it gets one shot at a complete payload and has to normalize messy input (any human-readable date/time format) and pick the best slot autonomously. This forced me to think about defensive design: what happens when there's no human in the loop to catch an ambiguous input.

**Chat → Telegram:** Moving to Telegram introduced a new failure mode that the web chat version never had to worry about — the bot receiving its own outgoing messages as if they were new user input, creating an infinite loop. I added explicit anti-loop logic to detect and stop this.

**OpenAI → Gemini:** Swapping the LLM provider on the Telegram version without rewriting the booking logic underneath it confirmed that the actual system design — the rules, the tool definitions, the data flow — was the real engineering work, not the choice of AI model. The model is replaceable; the system design isn't.

## Tools used

n8n · OpenAI API · Google Gemini API · Google Calendar API · Google Sheets API · Gmail API · Telegram Bot API · Lovable (website builder) · JSON Schema / Webhook
