---
title: "How I Automated CloudTalk Call Analysis With Gemini 2.5 for a Shopify Brand"
seoTitle: "Automating CloudTalk Recordings With Gemini 2.5 for Shopify"
seoDescription: "How I turned CloudTalk recordings into structured ops data using Gemini 2.5, a custom brand prompt, and Google Sheets, instead of building a real app."
datePublished: 2026-04-26T07:10:56.561Z
cuid: cmoffixps00ay28jphqfv3z3t
slug: automating-cloudtalk-call-analysis-with-gemini
cover: https://cdn.hashnode.com/uploads/covers/5ff83911a538d00135153553/e0aadfe3-1850-4224-b0a5-31abd4c4fc15.png

---

The Shopify brand I help operate runs its phones on CloudTalk. Every call gets recorded, which is great in theory, except none of those recordings were doing anything for us. They were just sitting there. Hundreds of calls a week -> order issues, address corrections, mobile payment confirmations, post-delivery feedback calls -> and the only way to know what happened on any of them was to actually go listen to one.

![](https://cdn.hashnode.com/uploads/covers/5ff83911a538d00135153553/37bac4a8-f517-4747-8593-6bf75abb5382.png align="center")

I wanted that data alive. Per-call, structured, sortable. So I built a pipeline that pulls each recording, runs it through Gemini 2.5 Flash with a heavily customized brand prompt, and drops the result into a Google Sheet my non-technical team actually uses. That's the whole story. Here's how it came together.

## The Real Problem

The brand has a specific shape. Perishable product, time-sensitive shipping, a regional mobile payment app that leaves about a third of orders sitting in "pending" until someone calls to confirm, a courier that won't deliver to PO Boxes, and a customer base where most calls are in Spanish and the rest in English.

CloudTalk handled the calls fine. Shopify handled the orders fine. Gorgias handled the tickets fine. None of them talked to each other in any useful way, and the recordings -> the most information-dense thing in the entire stack -> were untouched. Our CX team would open a Gorgias ticket and have no idea the customer had also called twice. I'd ask the ops lead how an agent was doing and the answer would be a feeling, not a number. Monday reporting took two hours and nobody trusted it.

What I needed was a thin layer that would pull the recording -> run it through an LLM that actually understood our business -> write the result somewhere my team could see and act on.

## Why I Did Not Build a Web App

![](https://cdn.hashnode.com/uploads/covers/5ff83911a538d00135153553/03f4acf8-d8cb-43fb-bcba-c50d3dc058f8.png align="center")

My instinct was to build a real internal tool. Next.js, Postgres, a deploy pipeline. I've shipped that stack plenty of times and I know how to make it nice. I talked myself out of it within a day :)

A spreadsheet is in production the moment you share the link. No CI, no auth provider, no DNS, no on-call. When the ops lead asks for a new column or wants follow-ups colored red, that's a ninety-second change instead of a ticket and a deploy. My team already lives in Sheets. They sort, filter, and pivot in there every day. Asking three non-technical people to learn a new internal tool, even a beautiful one, would have introduced the kind of friction that kills adoption. The best UI is the one your team already uses.

There's a principle here I keep coming back to. In early-stage or fast-moving environments, the best system isn't the most scalable one -> it's the one that gets adopted and works immediately. Shipping a Postgres-backed React app for an internal tool that four people use is engineering vanity. I've made that mistake before. I didn't make it again.

Will this scale to ten times the volume? No. But by the time we hit ten times the volume, I'll know exactly what to build, because the Sheet will have spent a year telling me. ^\_^

## The Pipeline

The whole thing is one Apps Script project bound to a Google Sheet. Around seven hundred lines of code. Runs on a ten-minute trigger. Same flow every time:

CloudTalk API -> dedupe against the sheet -> skip non-recorded calls -> Shopify lookup by phone -> grab the most recent order (number, total, status, line items, email) -> download the audio -> send audio + order context to Gemini 2.5 Flash -> parse the JSON -> write the row -> sync an internal note to Gorgias -> reassign the ticket from CloudTalk's phantom customer to the real Shopify one.

That last step fixed a months-old data hygiene problem nobody had been willing to tackle manually. CloudTalk creates its own "customer" in Gorgias keyed off the SIP address, which meant our tickets were attached to ghost accounts with no order history. Now they're attached to the real person :)

A second sheet -> the dashboard -> gets rebuilt every time new calls come in. KPI tiles at the top, an agent leaderboard in the middle, three pie charts at the bottom. The ops lead opens it in the morning, sees who needs follow-up, sees if anyone's score dropped overnight, and acts on it before standup.

## The Prompt Is the Product

The Gemini call is technically the simplest part of the system. The prompt is the part that took the most work and matters the most.

It's roughly fifteen hundred words. It reads like an onboarding doc for a new QA analyst. It explains the business -> what we sell, where we ship, the store hours, the payment methods, the fact that our courier won't deliver to PO Boxes, the difference between a welcome call and a feedback call. It defines our tone standard explicitly: friendly and bright, empathic, clear, professional. It lists what good agent performance looks like (verifying mobile payment status on welcome calls, getting a callback number, requesting a Google review on feedback calls) and what bad performance looks like (multiple long holds, monotone delivery, abrupt endings, vague callback promises). It defines a strict taxonomy of call types and order issue types, because if I let the model pick its own labels every row would be inconsistent and the dashboard would be useless.

Then it asks for a single JSON object -> call type, sentiment, agent score, satisfaction score, outcome, follow-up flag, summary, key topics, flags, and two transcripts (original language with speaker turns, and an English translation). The dual transcript made the sheet usable for stakeholders who don't speak Spanish.

If there's one thing I'd tell anyone trying this -> domain context beats model choice. The difference between a generic "analyze this call" prompt and my fifteen-hundred-word business-context prompt was bigger than the difference between any two frontier models I tested. Pre-enriching the prompt with the Shopify order context ("this customer's order is #4521, status: pending payment, total $48.50") made the analysis sharper still. The model stops guessing and starts reasoning.

## What Broke

Three things failed in production. Worth mentioning, because every operator post that pretends nothing went wrong is lying.

I trusted Gemini's JSON output too much in the first week. About 8% of responses came back with a stray comment or a "Sure, here's the analysis" preamble that broke the parser. I tightened the prompt and added a regex fallback that extracts the JSON block before giving up. Failure rate is now under half a percent.

I forgot rate limits the first time I ran the historical backfill across thirty days of calls -> burned through Gemini quota in eight minutes -> got blocked for an hour. I now apply the same rate limiter to every entry point and never trust myself to remember twice.

One malformed CloudTalk response was crashing entire batches of a hundred calls, because Apps Script doesn't isolate errors well. So I wrote a defensive normalizer that logs and skips anything weird instead of throwing.

None of these were deep bugs. They're the kind of thing you only find on real data, which is exactly why I'm glad I shipped fast in Sheets instead of polishing a web app for a month :)

## What It Cost and What Changed

Total ongoing cost: $15–25 a month for the Gemini API. Zero new SaaS subscriptions. Zero hosting. Apps Script and Sheets come with the Workspace plan we already pay for.

The qualitative change matters more than any number. I now actually know what's happening on our calls. We caught one agent consistently scoring 5/10 on tone -> targeted coaching -> they're at 8 now. Follow-up adherence went from "I think we're doing it" -> a hard number on a dashboard. Monday reporting dropped from two hours -> under ten minutes, because because the dashboard *is* the report. Our Gorgias tickets carry call summaries automatically, so the CX team starts every conversation with full context. ^\_^

## What I'd Tell Another Operator

Start with the workflow, not the tool. The question isn't which model to use -> it's which decision gets made better when this recording gets analyzed automatically. If you can't name the decision, the AI is decoration.

Spend your time on the prompt. Write it like you're training a new hire, not querying an API. Pre-enrich your inputs with whatever context you already have sitting in Shopify or your helpdesk -> don't make the model guess what you could just tell it.

Use the spreadsheet as long as you can. Sheets + Apps Script is an absurdly powerful operational substrate, and it will outlast your assumption that you need a real app. When concurrent edits get painful, when row counts crash performance, when you genuinely need real-time updates -> that's when you graduate. Not before.

Don't automate what your team should be deciding. The AI in our system surfaces, summarizes, and routes. It doesn't auto-resolve tickets, auto-issue refunds, or auto-respond to customers. That line will move over the next year, but I'm in no rush to move it.

Eventually this pipeline will outgrow Sheets. The data model will need a real database, the dashboard will need real-time updates, we'll add agent-facing tools with their own UI. That's fine. When we get there the migration will be easy, because the Sheet will have spent its life telling me exactly what fields and what workflows actually matter.

For now, the most sophisticated piece of AI automation in the company is a Google Sheet processing CloudTalk recordings through a brand-tuned Gemini prompt -> and it's working :)

If you're staring at a similar problem, my honest advice: skip the platform, skip the web app. Wire your existing tools together with a thin AI layer and a sheet your team already trusts. Ship it this week. Iterate next week. Worry about scale when scale is actually the thing that's broken.