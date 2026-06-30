# Physio Appointment — Telegram Version (Google Gemini)

The same Telegram booking system as the OpenAI version, with the underlying language model swapped to Google Gemini. Every piece of business logic — patient ID generation, slot rules, anti-loop safety, returning-patient lookups — stayed exactly the same. Only the model changed.

![Physio Appointment Telegram Gemini version workflow diagram](../../images/physio-telegram-gemini-version.png)

## How it works

This version is functionally identical to the [OpenAI Telegram version](../telegram-openai-version): same greeting rule, same anti-loop safety check, same patient registration and ID generation flow, same clinic scheduling rules, same returning-patient lookup tools, same structured confirmation email. The only difference is the language model node powering the AI Agent — Google Gemini instead of OpenAI.

## Why I built this version

After getting the OpenAI Telegram version working reliably, I wanted to confirm that the system's design — the rules, the tool definitions, the strict execution order — wasn't accidentally dependent on something specific to OpenAI's model behavior. Swapping in Gemini and having the same booking logic, anti-loop protection, and patient lookups continue to work correctly confirmed that the actual engineering (the system prompt, the tool architecture, the data flow) was the reusable part. The model itself is a swappable component.

## What I actually built (not just configured)

The system prompt, tool definitions, and execution rules are unchanged from the OpenAI version — which is the point. The work here was verifying that a different LLM provider, with different prompt-following behavior and different tool-calling conventions, could be dropped into the same agent architecture without requiring the underlying logic to be rewritten.

## Tools used

n8n · Google Gemini API · Google Calendar API · Google Sheets API · Telegram Bot API · LangChain Agent · Memory Buffer Window

## Workflow file

[`Physio_Appointment_With_Telegram__1_.json`](./Physio_Appointment_With_Telegram__1_.json) — import directly into n8n to see the full node graph.
