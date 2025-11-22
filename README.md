# 📘 Dify Workflows & Hosting Configuration

**Streaming Research Automation • Scraping • Content Planning • Docker Deployment**

---

## 🔥 Overview

This repository contains:

- **Dify.ai workflow documentation** for research, scraping, and content generation  
- **Docker hosting configuration**, including:
  - nginx reverse proxy
  - certbot (SSL)
  - SSRF proxy
  - Couchbase server
  - Postgres + Redis
  - `.env`-based configuration

---

## 🚀 Workflow System (Dify Workflows)

This repo includes three major workflows:

### 1️⃣ Get Webpage Content
A Firecrawl-powered scraper with:
- Markdown + HTML extraction  
- Optional LLM cleaning (`cleanOutput`)  
- Boilerplate removal  
- Structured output

---

### 2️⃣ Collect Summarized Web Research
A structured research engine that:
- Uses multi-query search (`|||`)  
- Normalizes search results into JSON  
- Extracts fact-level insights via LLM  

---

### 3️⃣ Streaming Service Promo Code Automation
Generates DealNews-style full articles:
- Research → Outline → URL scraping → Expansion  
- Internal linking with knowledge base  
- SEO-optimized structure  

---

## 🔄 High-Level Workflow

User Query
↓
Collect Summarized Web Research
↓ (fact extraction)
Streaming Promo Code Automation
↓ (outline → expansion → scrape URLs)
Get Webpage Content
↓ (cleaned text)
Final SEO-Optimized Article

---

## 📂 Recommended Repository Structure
/
├── workflows/
│ ├── Promo Code Automation.yml
│ ├── Get Webpage Content.yml
│ ├── Collect Summarized Web Research.yml
│
├── docs/
│ ├── README-get-webpage-content.md
│ ├── README-collect-summarized-web-research.md
│ ├── diagrams/...
│
└── README.md

## 🔧 How to Use These Workflows Together

1.) Upload each .yml workflow into Dify

2.) Enable Available as Tool

3.) Configure your search provider (search_get)

4.) Connect your knowledge base dataset

5.) Run Streaming Service Promo Code Automation

---

## 🐳 Docker Hosting Setup

This repo includes a full Dify Docker stack:

- nginx reverse proxy  
- Certbot (SSL auto-renew)  
- Couchbase server  
- SSRF proxy  
- Postgres + Redis  
- Unified `.env` configuration  

---

## 📦 Key Improvements in This Docker Setup
✔ Certbot Container

Automated Let’s Encrypt certificate management.
See: certbot/README.md

✔ Unified .env

One file controls:

Domain + URLs

Database configuration

Redis credentials

Storage provider settings

Vector DB selection

CORS + proxy configuration

## ✔ Vector Database Selectable

VECTOR_STORE=weaviate

Supports Weaviate, Milvus, Qdrant, OpenSearch, etc.


## 📄 License

MIT — See LICENSE for details.

## 📝 Notes on .env

Common URLs

CONSOLE_API_URL

SERVICE_API_URL

APP_WEB_URL

FILES_URL

Database

DB_USERNAME

DB_PASSWORD

DB_HOST, DB_PORT

Redis

REDIS_PASSWORD

Storage

STORAGE_TYPE=local|s3|azure-blob|google-storage|...

Vector DB

VECTOR_STORE

WEAVIATE_ENDPOINT

MILVUS_URI

---

# Full Installation Guide (Dify Workflows + Docker Hosting)

## 1. Install Docker & Docker Compose
If Docker is not installed, run:

sudo apt update
sudo apt install docker.io docker-compose-plugin -y

Enable Docker:

sudo systemctl enable docker
sudo systemctl start docker

## 2. Clone the Repository

git clone https://github.com/j-zulick/dify.ai-content-automation.git

cd dify.ai-content-automation

## 3. Create and Configure Your `.env` File
Copy the example:

cp .env.example .env

Edit `.env` and set:

### Required URLs
- `CONSOLE_API_URL=https://yourdomain.com/console/api`
- `CONSOLE_WEB_URL=https://yourdomain.com/console`
- `SERVICE_API_URL=https://yourdomain.com/v1`
- `APP_API_URL=https://yourdomain.com/api`
- `APP_WEB_URL=https://yourdomain.com`
- `FILES_URL=https://yourdomain.com/files`

### Database
- `DB_USERNAME=postgres`
- `DB_PASSWORD=yourpassword`
- `DB_HOST=db`
- `DB_PORT=5432`

### Redis
- `REDIS_PASSWORD=yourpassword`

### Vector DB
Choose one:

VECTOR_STORE=weaviate

or 

VECTOR_STORE=milvus

## 4. Start Dify Stack
Run all services:

docker compose up -d

Check logs:

docker compose logs -f

## 5. (Optional) Start Middleware Stack
If needed:

docker compose -f docker-compose.middleware.yaml up -d

## 6. Configure SSL (Certbot)
If using your domain with HTTPS:

1. Place SSL certificates in:

nginx/ssl/dify.crt
nginx/ssl/dify.key

2. Set in `.env`:

NGINX_HTTPS_ENABLED=true

Restart:

docker compose down
docker compose up -d

## 7. Access Dify
Open:

https://yourdomain.com

## 8. Use the Workflows in Dify

1. Upload all `.yml` files in `workflows/`
2. Mark each workflow as **Available as Tool**
3. Configure search (`search_get`)
4. Connect Knowledge Base
5. Run **Streaming Service Promo Code Automation**

## 9. Updating the Server
To update:

git pull
docker compose down
docker compose up --build -d

## 10. Troubleshooting

### Check Services

docker compose ps

### Restart Everything

docker compose down
docker compose up -d

### Check specific container logs

docker compose logs api
docker compose logs web
docker compose logs nginx

