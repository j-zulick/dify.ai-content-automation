📘 Dify Workflows — Streaming Research, Scraping & Content Automation

This repository contains a suite of Dify.ai workflows that work together to automate research, scraping, content planning, and draft creation for DealNews-style streaming discount content.

It includes:

Get Webpage Content — A Firecrawl-based scraper with optional LLM cleaning

Collect Summarized Web Research — A structured fact-gathering research engine

Streaming Service Promo Code Automation — A full article planning & drafting workflow

These workflows are modular and designed to be used both independently and together as a connected system.

🚀 Overview of the Workflow System
User Query
   ↓
Collect Summarized Web Research
   ↓  (fact-level research)
   ↓
Streaming Service Promo Code Automation
   ↓  (scrapes URLs, structures outline, expands sections)
   ↓
Get Webpage Content
   ↓  (cleaned webpage content)
   ↓
Final Draft Article (SEO-ready)


The system:

Performs multi-query web research

Summarizes research into extracted facts

Scrapes top URLs and cleans page content

Generates structured, SEO-focused long-form articles

Injects internal links using a knowledge base

Outputs DealNews-style subscriber-facing content

📂 Repository Structure

A recommended layout for your repo:

/
├── workflows/
│   ├── Content Planner - Streaming Service Promo Code Automation.yml
│   ├── Get Webpage Content.yml
│   ├── Collect Summarized Web Research.yml
│
├── docs/
│   ├── README-get-webpage-content.md
│   ├── workflow-diagram-get-webpage-content.txt
│   ├── architecture-diagram-get-webpage-content.md
│   ├── README-collect-summarized-web-research.md
│   ├── workflow-diagram-collect-summarized-web-research.txt
│   ├── architecture-diagram-collect-summarized-web-research.md
│   ├── README-streaming-service-planner.md        (optional — can generate)
│   ├── diagrams/                                  (optional)
│
└── README.md   ← (this file)


You may organize differently, but this structure supports clarity and scalability.

🧩 Workflow Summaries
1. 🔍 Collect Summarized Web Research

Purpose:
Generates structured research summaries using web search + LLM fact extraction.

Key features:

Split queries with ||| for multi-topic research

Web search API (search_get)

JSON → structured links (title, URL, date, snippet)

LLM conversion into fact-level bullet summaries

Output ready for content planning

Typical Use:
Pre-populating knowledge for outlines and article generation.

Docs:
Located in docs/README-collect-summarized-web-research.md

2. 🕸️ Get Webpage Content

Purpose:
Scrape full webpage content using Firecrawl, clean/normalize results, and optionally run LLM-based content cleanup.

Key features:

Firecrawl scrape tool (markdown + HTML)

Optional custom text merging

Optional “cleanOutput” LLM pass (remove nav/header/footer/disclaimers/etc.)

Outputs structured content for deeper analysis

Typical Use:
Scraping competitor pages, vendor pages, pricing pages, or news articles.

Docs:
Located in docs/README-get-webpage-content.md

3. ✍️ Streaming Service Promo Code Automation

Purpose:
Full article-generation pipeline for pages like:

How Much Does <Vendor> Cost? Saving the Most in 2025


Key features:

Calls the Collect Summarized Web Research workflow 4× for strong coverage

Extracts URLs → scrapes each → summarizes content

Builds a detailed outline with structured headings

Expands each outline section with context-aware LLMs

Pulls internal links from your Dify knowledge base

Appends standardized DealNews trust section

Outputs a complete article ready for editing or publishing

Typical Use:
Creating SEO content around promo codes, pricing trends, and discount patterns.

🔧 Using These Workflows Together
1. Add all three workflows to Dify.ai

Upload the .yml files into Dify:

Settings → Workflows → Import Workflow

2. Set each workflow to “Available as Tool”

In Dify:

Open a workflow → Settings → “Enable Tool Workflow”

This allows one workflow to call another.

3. Configure your Search API provider

The research workflow expects a provider named “Search Web” with a tool called search_get.

Make sure your API key is configured.

4. Connect your Knowledge Base

The Streaming Content workflow references a dataset:

dataset_id: 4b16bf72-6a4b-445c-b924-a0bcf7ad8f7a


Ensure that:

The dataset exists

It contains internal links and DealNews content

The “Knowledge Retrieval” step is pointed at this dataset

5. Trigger the main workflow

Use the Streaming Service Promo Code Automation workflow and pass:

vendor_name

optional research

optional custom_scrape

knowledge

You will receive a complete markdown-style article.

💡 Example Usage

Running the main workflow with:

vendor_name = "Hulu"
knowledge = "Hulu deals"


Will generate:

Four rounds of web research

Scrape top URLs

Analyze pricing, deals, discount history

Insert internal DealNews links

Produce a polished, structured article
