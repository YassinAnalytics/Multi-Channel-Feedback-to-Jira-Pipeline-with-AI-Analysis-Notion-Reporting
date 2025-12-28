# Multi-Channel-Feedback-to-Jira-Pipeline-with-AI-Analysis-Notion-Reporting
## Description

This workflow turns scattered user feedback into a structured product backlog pipeline.

- It collects feedback from three channels (Telegram bot, Google Form/Sheets, and Gmail), normalizes it, and sends it to an AI model that:

- Classifies the feedback (bug, feature request, question, etc.)

- Extracts sentiment and pain level

- Estimates business impact and implementation effort

- Generates a short summary

- Then a custom RICE-style priority score is computed, a Jira ticket is created automatically, a Notion page is generated for documentation, and a monthly product report is sent by email to stakeholders.

It helps product & support teams move from “random feedback in multiple tools” to a repeatable, data-driven product intake process with zero manual triage.

## Context

In most teams, feedback is:

- spread across emails, forms, and chat messages

- manually copy–pasted into Jira (when someone remembers)

- hard to prioritize objectively

- nearly impossible to review at the end of the month

This workflow solves that by:

- Centralizing feedback from Telegram, Google Forms/Sheets, and Gmail

- Automatically normalizing all inputs into the same JSON structure

- Using AI to categorize, tag, summarize, and score each request

- Calculating a RICE-based priority adapted to your tiers (free / pro / enterprise)

- Creating a Jira issue with all the context and acceptance criteria

- Generating a Notion page for each feedback+ticket pair

- Sending a monthly “Product Intelligence Report” by email with insights & recommendations

The result: less manual work, better prioritization, and a clear story of what users are asking for.

## Target Users

This template is designed for:

- Product Managers and Product Owners

- SaaS teams with multiple feedback channels

- Support / CS teams that need a structured escalation path

- Project Managers who want objective, data-driven prioritization

- Any team that wants “feedback → backlog” automation without building a custom platform

## Technical Requirements

You’ll need:

- Google Sheets credential

- Gmail credential

- Telegram Bot + Chat ID

- Google Form connected to a Google Sheet 

<img width="945" height="899" alt="image" src="https://github.com/user-attachments/assets/808bc359-d212-46f5-b23e-7318a0a5bbb5" />

<img width="945" height="294" alt="image" src="https://github.com/user-attachments/assets/bc73189a-6a3a-4de8-bd15-ae3c1922bfcd" />


- Jira credential (Jira Cloud)

- Notion credential

- OpenAI/ Anthropic credential for the AI analysis node

- An existing Jira project where tickets will be created

- A Notion database or parent page where feedback pages will be stored

## Workflow Steps

The workflow is organized into four main sections:
<img width="1669" height="482" alt="image" src="https://github.com/user-attachments/assets/026e85e7-cf10-48c0-b337-11d7840d13cd" />


1) Triggers (Multi-channel Intake)

- Telegram Trigger – Listens for new messages sent to your bot

- Google Form / Sheet Trigger – Listens for new form responses / rows

- Gmail Trigger – Listens for new emails matching your filter (e.g. [Feedback] in subject)

- All three paths send their payloads into a “Data Normalizer” node that outputs a unified structure:

2) Request Treated and Enriched (AI Analysis)

- Instant Reply (Telegram only) – Sends a quick “Thanks, we’re analysing your feedback” message

- User Enrichment – Enriches user tier based on mapping

- Message a Model (AI) 

	- classifies the feedback

	- extracts tags

	- scores sentiment, pain, business impact, effort

	- generates a short summary & acceptance criteria

- JSON Parse / Merge – Merges AI output back into the original feedback object

3) Priority Calculation & Jira Ticket Creation

- Priority Calculator applies a RICE-style formula using:

	- pain level

	- business impact

	- implementation effort

	- user tier weight

	- assigns internal priority: P0 / P1 / P2 / P3

	- maps to Jira priority: Highest / High / Medium / Low

- Create Jira Issue – Creates a ticket with:

	- summary from AI

	- description including raw feedback, AI analysis, and RICE breakdown

	- labels based on tags

	- priority based on the calculator

- Post-processing  – Prepares a clean payload for notifications & logging

- IF (Source = Telegram) – Sends a rich Telegram message back to the user with:

	- Jira key + URL

	- category, priority, RICE score, tags, and estimated handling time

	- Append to Google Sheet (Analytics Log) – Logs each feedback with:

	- source, user, category, sentiment, RICE score, priority, Jira key, Jira URL

- Create Notion Page – Creates a documentation page linking:

	- the feedback

	- the Jira ticket

	- AI analysis

	- acceptance criteria

4) Monthly Reporting (Product Intelligence Report)

- Monthly Trigger – Runs once a month

- Query Google Sheet – Fetches all feedback logs for the previous month

- Aggregate Monthly Stats – Computes:

	- feedback volume

	- breakdown by category / sentiment / source / tier / priority

	- average RICE, pain, and impact

	- top P0/P1 issues and top feature requests

	- Message a Model (AI) – Generates a written “Product Intelligence Report” with:

	- executive summary

	- key insights & trends

	- top pain points

	- strategic recommendations

- Parse Response: Extracts structured insights + short summary

- Create Notion Report Page with:

	- metrics, charts-ready tables, insights, and recommendations

	- Append Monthly Log to Google Sheet – Stores high-level stats for historical tracking

- Send Email with a formatted HTML report to stakeholders with:

	- key metrics

	- top issues

	- recommendations

	- link to the full Notion report

## Key Features

- Multi-channel intake: Telegram + Google Forms/Sheets + Gmail

- AI-powered triage: automatic category, sentiment, tags, and summary

- RICE-style priority scoring with tier weighting

- Automatic Jira ticket creation with full context

- Notion documentation for each feedback and for monthly reports

- Google Sheets analytics log for exploration and dashboards

- Monthly “Product Intelligence Report” sent automatically by email

- Designed to be adaptable: you can plug in your own labels, tiers, and scoring rules

## Expected Output

When the workflow is running, you can expect:

- A Jira issue created automatically for each relevant feedback
<img width="1459" height="564" alt="image" src="https://github.com/user-attachments/assets/c7922ca8-d439-4e0e-9515-e5dfd824c410" />

- A confirmation email
<img width="945" height="252" alt="image" src="https://github.com/user-attachments/assets/df70670f-dd64-4df1-ba1a-a8551573e6a9" />

- A Telegram confirmation message when the feedback comes from Telegram
<img width="799" height="92" alt="image" src="https://github.com/user-attachments/assets/4b475b69-d85d-42fd-a599-5365165d064c" />

<img width="692" height="536" alt="image" src="https://github.com/user-attachments/assets/12abb913-c6a0-4c14-b24d-56bbc5623335" />

- A Google Sheet filled with normalized feedback and scoring data
<img width="945" height="145" alt="image" src="https://github.com/user-attachments/assets/ba48d48a-c253-4b39-af77-fa0caaaa2bde" />

- A Notion page per feedback/ticket with AI analysis and acceptance criteria
![image.png](fileId:3325)
Every month:

- a Notion “Monthly Product Intelligence Report” page
![image.png](fileId:3324)
<img width="945" height="364" alt="image" src="https://github.com/user-attachments/assets/5ce2e811-0242-472a-a9ce-f69ac8b8df4c" />

- a summary email with key metrics and insights for your stakeholders

<img width="945" height="443" alt="image" src="https://github.com/user-attachments/assets/e022d36b-2c1c-48fc-b6e8-9e953037ad48" />


## How it works

- Trigger – Listens to Telegram / Google Forms / Gmail

- Normalize – Converts all inputs to a unified feedback format

- Enrich with AI – Category, sentiment, pain, impact, effort, tags, summary

- Score – Computes RICE-style priority and maps to Jira priority

- Create Ticket – Opens a Jira issue + Notion page + logs to Google Sheets

- Notify – Sends Telegram confirmation (if source is Telegram)

- Report – Once a month, aggregates everything and sends a Product Intelligence Report

## Tutorial Video

Tutorial video:
[Watch the Youtube Tutorial video](https://www.youtube.com/watch?v=q0Is11oU18Y)

## Template
https://n8n.io/workflows/10896-multi-channel-feedback-to-jira-pipeline-with-ai-analysis-and-notion-reporting/
