📘 Dify Workflows & Hosting Configuration

Streaming Research Automation • Scraping • Content Planning • Docker Deployment

This repository contains both:

Dify.ai workflow documentation for streaming research, scraping, and content automation

Dify Docker hosting configuration, including nginx, certbot, SSRF proxy, Couchbase server, and environment setup

It serves as a combined home for:

Research workflows

Content automation workflows

The hosting stack that powers your private Dify instance

🚀 Workflow System Overview (Dify Workflows)

This repo includes three major Dify workflows:

1. Get Webpage Content

A Firecrawl-powered webpage scraper with:

Markdown + HTML extraction

Optional LLM "cleanOutput" content cleaning

Removal of navigation, headers, disclaimers, and boilerplate

Structured output ready for downstream summarization

2. Collect Summarized Web Research

A structured research engine that:

Uses multi-query search (||| splitting)

Converts search results into normalized JSON

Extracts fact-level findings with an LLM

Outputs clean research summaries used by planning workflows

3. Streaming Service Promo Code Automation

A DealNews-style long-form content generator that:

Runs four rounds of structured web research

Scrapes URLs and cleans competitor content

Builds a detailed SEO outline

Expands each section via LLM

Adds internal links from your Dify knowledge base

Produces a polished markdown article

🔄 High-Level Workflow Flow
User Query  
   ↓  
Collect Summarized Web Research  
   ↓ (fact extraction)  
Streaming Promo Code Automation  
   ↓ (outline → expansion → scrape URLs)  
Get Webpage Content  
   ↓ (cleaned text)  
Final SEO-Optimized Article  

📂 Recommended Repository Structure
/
├── workflows/
│   ├── Content Planner - Streaming Service Promo Code Automation.yml
│   ├── Get Webpage Content.yml
│   ├── Collect Summarized Web Research.yml
│
├── docs/
│   ├── README-get-webpage-content.md
│   ├── README-collect-summarized-web-research.md
│   ├── workflow-diagram-get-webpage-content.txt
│   ├── workflow-diagram-collect-summarized-web-research.txt
│   ├── architecture-diagram-get-webpage-content.md
│   ├── architecture-diagram-collect-summarized-web-research.md
│
└── README.md  ← (this file)

🔧 How to Use These Workflows Together

Upload each .yml workflow into Dify

Set each workflow to Available as Tool

Configure your search provider (search_get)

Connect your knowledge base dataset

Run “Streaming Service Promo Code Automation” with your vendor name

🐳 Docker Hosting Configuration (Included in Repo)

This repo includes the full Dify hosting stack:

nginx (reverse proxy)

certbot (SSL + auto-renewal)

SSRF proxy (security layer)

Couchbase server

Postgres + Redis via docker-compose

Environment management via .env.example

📦 Key Improvements in This Docker Setup
✔ Certbot container

Integrated LetsEncrypt certificate management.
See: certbot/README.md

✔ Unified .env

One environment file controls:

URLs

DB settings

Redis

Storage providers

Vector databases

CORS

Proxy behavior

Sandbox settings

✔ Vector Database Configurable

Set via:

VECTOR_STORE=weaviate


Supports: Weaviate, Milvus, OpenSearch, Qdrant, etc.

🐳 How to Deploy
1. Prepare environment
cp .env.example .env


Edit values to match your domain + credentials.

2. Launch services
docker compose up -d

3. SSL (optional)

See certbot/README.md

4. Middleware (optional)
docker compose -f docker-compose.middleware.yaml up -d

📝 Notes on .env

Important areas include:

Common URLs

CONSOLE_API_URL

SERVICE_API_URL

APP_WEB_URL

Database

DB_USERNAME, DB_PASSWORD

Redis

REDIS_PASSWORD

Storage

STORAGE_TYPE=local|s3|azure-blob|...

Vector DB

VECTOR_STORE

WEAVIATE_ENDPOINT

MILVUS_URI
