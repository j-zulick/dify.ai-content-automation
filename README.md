<<<<<<< HEAD
📘 Dify Workflows — Streaming Research, Scraping & Content Automation

This repository contains a suite of Dify.ai workflows that work together to automate research, scraping, content planning, and draft creation for DealNews-style streaming discount content.

It includes:

# 📘 Dify Workflows & Hosting Configuration  
Streaming Research Automation • Scraping • Content Planning • Docker Deployment

This repository contains both:

1. **Dify.ai workflow documentation** for streaming research, scraping, and content automation  
2. **Dify Docker hosting configuration**, including nginx, certbot, SSRF proxy, Couchbase server, and environment setup

It is intended as a combined home for:
- Your research workflows  
- Your content automation workflows  
- The hosting stack that powers your private Dify instance

---

# 🚀 Workflow System Overview (Dify Workflows)

This repo includes three major Dify workflows:

### **1. Get Webpage Content**
Firecrawl-based scraper with optional LLM cleaning.

### **2. Collect Summarized Web Research**
A structured fact-gathering research engine.

### **3. Streaming Service Promo Code Automation**
A full article planning & drafting workflow.

### **High-Level Flow**

User Query
↓
Collect Summarized Web Research
↓ (fact-level research)
Streaming Service Promo Code Automation
↓ (scrapes URLs, outlines content, expands sections)
Get Webpage Content
↓ (cleaner webpage content)
Final Draft Article (SEO-ready)

yaml
Copy code

### **Capabilities**
- Multi-query web research  
- Fact-level summarization  
- URL scraping + text cleaning  
- SEO-focused structured article generation  
- Automatic internal linking from knowledge base  
- Output in DealNews editorial style  

---

# 📂 Recommended Repository Structure

/
├── workflows/
│ ├── Content Planner - Streaming Service Promo Code Automation.yml
│ ├── Get Webpage Content.yml
│ ├── Collect Summarized Web Research.yml
│
├── docs/
│ ├── README-get-webpage-content.md
│ ├── README-collect-summarized-web-research.md
│ ├── workflow-diagram-get-webpage-content.txt
│ ├── workflow-diagram-collect-summarized-web-research.txt
│ ├── architecture-diagram-get-webpage-content.md
│ ├── architecture-diagram-collect-summarized-web-research.md
│
└── README.md (this file)

yaml
Copy code

---

# 🧩 Workflow Summaries

## 🔍 1. Collect Summarized Web Research
- Multi-query search (`|||` splitting)
- Web search → structured JSON links
- LLM → fact extraction
- Used for article planning and workflow pre-research

Docs: `docs/README-collect-summarized-web-research.md`

---

## 🕸️ 2. Get Webpage Content
- Firecrawl scraping (HTML + markdown)
- Optional LLM cleaning pass (`cleanOutput`)
- Removes boilerplate, disclaimers, nav, etc.

Docs: `docs/README-get-webpage-content.md`

---

## ✍️ 3. Streaming Service Promo Code Automation
Generates fully written DealNews-style articles including:

- Vendor pricing breakdowns  
- Discount trends  
- Summaries of competitor pages  
- Internal link injection  
- Research synthesis  
- Structured SEO-optimized writing  

---

# 🔧 Using These Workflows Together

1. Import all .yml into Dify  
2. Mark each workflow as “Available as Tool”  
3. Configure search provider (`search_get`)  
4. Connect knowledge base datasets  
5. Run the main “Streaming Promo Code Automation” workflow

---

# 🐳 Docker Deployment (Hosting Configuration)

This repo also includes the **updated Dify docker deployment stack**, replacing legacy files.

---

## 📦 What’s New

### ✔ Certbot container
- Auto-renewing SSL certificates  
- Integrated with nginx reverse proxy  
- See: `docker/certbot/README.md`

### ✔ Unified `.env` configuration
- Centralized environment control  
- Required for running docker-compose  
- Use `.env.example` as reference

### ✔ Vector database selection
Set via:  
VECTOR_STORE=weaviate | milvus | opensearch

shell
Copy code

### ✔ Legacy support moved
Legacy docker files are in:
docker-legacy/

yaml
Copy code

---

# 🐳 How to Deploy with Docker Compose

## 1. Prerequisites
- Docker  
- Docker Compose v2+

## 2. Prepare Environment

```bash
cd docker
cp .env.example .env
Edit .env and update:

CONSOLE_API_URL

SERVICE_API_URL

APP_WEB_URL

Database settings

Redis settings

Storage (S3, Azure Blob, etc.)

Vector DB params

3. Run Dify
bash
Copy code
docker compose up -d
4. SSL Setup
See:

bash
Copy code
docker/certbot/README.md
🔧 Middleware Deployment (Optional)
Use:

Copy code
docker-compose.middleware.yaml
Create:

bash
Copy code
cp middleware.env.example middleware.env
Run:

bash
Copy code
docker compose -f docker-compose.middleware.yaml up -d
🔁 Migration from Legacy Docker
If upgrading:

Review .env.example

Transfer custom nginx/squid configs

Backup old data before migration

📝 Notes on .env
Some important sections include:

Common Variables
CONSOLE_API_URL

SERVICE_API_URL

APP_WEB_URL

FILES_URL

Database
DB_USERNAME, DB_PASSWORD, DB_HOST, DB_PORT

Redis
REDIS_HOST, REDIS_PASSWORD

Storage
STORAGE_TYPE, S3_BUCKET_NAME

Vector Databases
VECTOR_STORE

WEAVIATE_ENDPOINT

MILVUS_URI

