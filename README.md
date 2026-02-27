# Data Preparation Agent

<div align="center">
  <a href="https://www.youtube.com/watch?v=X2XHFci0JUE" target="_blank" rel="noopener noreferrer">
    <img src="https://img.youtube.com/vi/X2XHFci0JUE/hqdefault.jpg" alt="Watch the Demo" width="700">
  </a>
  <p><em>Click to watch the demo video</em></p>
</div>

Transform messy Excel files into clean, analytics-ready data with AI. Upload a spreadsheet, describe the transformation you need in plain English, and download structured CSV files — all from a simple web interface running locally in Docker.

<details>
<summary><strong>Table of Contents</strong></summary>

- [Features](#-features)
- [How It Works](#-how-it-works)
- [Prerequisites](#-prerequisites)
- [Quick Start (3 Steps)](#-quick-start-3-steps)
- [Using the Application](#-using-the-application)
- [Tips](#-tips)
- [Support](#-support)
- [Security & Privacy Notice](#%EF%B8%8F-security--privacy-notice)
- [Managing the Container](#-managing-the-container)
- [Docker Compose (Optional)](#-docker-compose-optional)
- [Local File Storage](#-local-file-storage)
- [Troubleshooting](#-troubleshooting)
- [Security Best Practices](#-security-best-practices)
- [Legal & Security](#-legal--security)
- [Documentation](#-documentation)

</details>

---

## ✨ Features

- **Automatic Table Detection** — Finds and extracts tables from messy, multi-sheet Excel files
- **AI-Powered Transformation** — Describe what you want in plain English; the AI generates the code
- **Preview Before You Commit** — Review the transformation plan and approve before any changes are applied
- **Clean CSV Export** — Download analysis-ready CSV files from your transformed data

---

## 🔄 How It Works

1. **Upload** — Drag and drop your Excel file into the web UI
2. **Detect** — The agent automatically identifies all tables across sheets
3. **Transform** — Describe your goal in natural language (e.g., *"Get the top 10 customers by revenue"*); the AI generates a transformation plan using the Google Gemini API
4. **Review** — Preview the proposed changes before they are applied
5. **Export** — Download clean, structured CSV files ready for analysis

Your file contents are sent to the Google Gemini API for AI-powered analysis. Processed results are stored locally on your machine. See the [Security & Privacy Notice](#%EF%B8%8F-security--privacy-notice) for full details on data handling.

---

## 📋 Prerequisites

- **Docker** — [Download here](https://www.docker.com/products/docker-desktop/)
- **Gemini API Key** — [Get one free](https://aistudio.google.com/apikey)
- **4 GB RAM** minimum (8 GB recommended)
- **10 GB disk space**

---

## ⚡ Quick Start (3 Steps)

### Step 1: Get Your Free Gemini API Key

1. Go to [Google AI Studio](https://aistudio.google.com/apikey)
2. Sign in with your Google account
3. Click **"Create API Key"**
4. Copy your key (it looks like `AIzaSyC_xxxxxxxxxxxxxxxxx`)

### Step 2: Pull the Docker Image

```bash
docker pull ghcr.io/emergenceai/em-data-preparation-agent:latest
```

### Step 3: Run the Application

**Option A: Enter the API key later via the UI** (easiest)
```bash
docker run -d -p 8000:8000 --name data-prep-agent ghcr.io/emergenceai/em-data-preparation-agent:latest
```

**Option B: Provide the API key at startup**
```bash
docker run -d \
  --name data-prep-agent \
  -p 8000:8000 \
  -e GEMINI_API_KEY="your-gemini-api-key-here" \
  -v $(pwd)/data:/app/data \
  ghcr.io/emergenceai/em-data-preparation-agent:latest
```

Open your browser to **http://localhost:8000** and you're ready to go.

If you did not provide an API key at startup, you will be prompted to enter one in the UI.

---

## 🎯 Using the Application

Once the container is running, open your browser to **http://localhost:8000** and follow these steps:

1. **Upload your Excel file** — drag and drop or browse
2. **Review the auto-detected tables** across all sheets
3. **Apply transformations** using the built-in options, or describe what you want in natural language
4. **Review and confirm** the transformation plan
5. **Download** clean CSV files ready for analysis

> If you see a **"GEMINI API KEY REQUIRED"** error, enter your API key in the UI or pass it at startup with `-e GEMINI_API_KEY="your-key"`.

---

## 💡 Tips

- **First time?** Start with a small Excel file to test the workflow
- **Sample files?** Check the `data/sample_files/` folder for example spreadsheets
- **Large files?** The app handles Excel files up to 50 MB
- **Multiple tables?** The AI detects and processes each table separately
- **Need help?** Check the logs with `docker logs data-prep-agent -f`

---

## 📞 Support

### Join the Community

Connect with other users and the team on Slack — ask questions, share feedback, and get help in the **[`#data-preparation-agent`](https://link.emergence.ai/communityslack)** channel.

[Join the Slack workspace →](https://link.emergence.ai/communityslack)

### Getting Help

For community support and troubleshooting help, see our [Support Guide](SUPPORT.md).

This repository provides container access and documentation for evaluation and integration purposes. Support is provided on a best-effort basis.

#### Bug Reports

If you have found a reproducible issue, please open a GitHub Issue using the Bug Report template and include:

- Container version
- Deployment environment (OS, cloud, runtime)
- Steps to reproduce
- Relevant logs or error messages (sanitized)

Issues that cannot be reproduced or lack sufficient information may be closed.

#### Feature Requests

Feature requests and enhancement suggestions are welcome. Open a GitHub Issue using the Feature Request template and describe:

- The problem you are trying to solve
- The expected behavior
- Any relevant context or constraints

Feature requests are reviewed periodically. Implementation is not guaranteed.

#### Usage Questions

Please review the documentation in this repository before opening an issue. For questions about architecture, enterprise integration, or production deployment, please [join Slack](https://link.emergence.ai/communityslack) to contact us directly.

#### Security Issues

**Do not report security vulnerabilities through public GitHub issues.**

Email us at **security@emergence.ai** instead. See the [Security Policy](SECURITY.md) for full details.

#### Response Expectations

- Issues are reviewed periodically
- Response times are not guaranteed
- GitHub support is limited to reproducible defects and documented behavior

### Enterprise Support

For enterprise deployments, production use cases, or integration discussions, contact **support@emergence.ai**.

---

## ⚠️ Security & Privacy Notice

**Please read before using this tool.**

### What Data Is Processed
- **Your uploaded Excel files** are sent to the Google Gemini API for AI-powered analysis
- **File contents and transformation requests** are processed on Google's servers
- **No data is stored by Emergence** — processed results are saved locally, but file contents are transmitted to Google for analysis
- Review the [Google Gemini API Privacy Policy](https://policies.google.com/privacy)

### Security Considerations
- **AI Code Execution** — This tool generates and executes Python code. Only process files you trust.
- **Code Obfuscation** — The application code is obfuscated and cannot be audited
- **API Key Security** — Your Gemini API key stays in your local environment
- **Internet Required** — An active internet connection is needed for AI processing

> **Do not process sensitive, confidential, or regulated data** (PII, PHI, financial records) unless you have reviewed Google's data processing terms and your organization permits it.

Read the full **[Terms of Use](TERMS_OF_USE.md)** for complete legal details, including third-party LLM provider data handling.

---

## 🔧 Managing the Container

```bash
# Check if the container is running
docker ps

# View logs
docker logs data-prep-agent -f

# Stop the container
docker stop data-prep-agent

# Restart the container
docker start data-prep-agent

# Remove the container
docker rm -f data-prep-agent
```

---

## 🐳 Docker Compose (Optional)

The repository includes a ready-to-use `docker-compose.yaml` for easier container management. This requires [Docker Compose V2](https://docs.docker.com/compose/install/) (the `docker compose` subcommand, not the legacy `docker-compose` binary).

**1. Configure your environment (optional):**

```bash
cp env-sample .env
# Edit .env and set your GEMINI_API_KEY (or skip this and enter it via the UI)
```

> **Never commit your `.env` file to version control.** Add `.env` to your `.gitignore` if it is not already there.

**2. Start the application:**

```bash
docker compose up -d        # Start in background
docker compose logs -f      # View logs
docker compose down          # Stop and remove containers
```

The included `docker-compose.yaml` provides:

- **Health checks** — Automatic container health monitoring via `/health` endpoint
- **Named volume** (`em-data-prep-data`) — Persistent storage for uploads, processing files, and outputs
- **Configurable storage** — Optional environment variables for storage directories and cleanup policy
- **Auto-restart** — Container restarts automatically unless explicitly stopped

> **Note:** When using Docker Compose, the container is named `em-data-preparation-agent`. Adjust `docker logs` and `docker stop` commands accordingly, or use `docker compose logs` and `docker compose stop` instead.

---

## 💾 Local File Storage

All uploaded and processed files are persisted in the mounted data volume:

```
./data/
├── uploads/           # Your uploaded Excel files
├── temp_processing/   # Temporary working files
└── outputs/           # Transformed CSV outputs
```

This section describes where files are stored **on disk**. For details on how data is handled during processing — including what is sent to the Gemini API — see the [Security & Privacy Notice](#%EF%B8%8F-security--privacy-notice).

---

## ❓ Troubleshooting

### Container Fails to Start

If the container exits immediately after starting:

```bash
docker logs data-prep-agent
```

Check the logs for error messages. The API key is optional at startup — you can always enter it in the UI.

### "GEMINI API KEY REQUIRED" Error

1. Verify your `.env` file exists and contains the correct key
2. Ensure you are passing the environment variable correctly:
   ```bash
   docker run -e GEMINI_API_KEY="your-actual-key" ...
   ```

### API Returns 401/403 Errors

1. Verify your Gemini API key is valid at [Google AI Studio](https://aistudio.google.com/apikey)
2. Check whether you have exceeded the API quota
3. Ensure there are no extra spaces or quotes in the key

### Port Already in Use

If you see `Bind for 0.0.0.0:8000 failed: port is already allocated`:

```bash
docker run -d \
  -p 8001:8000 \
  --name data-prep-agent \
  ghcr.io/emergenceai/em-data-preparation-agent:latest
```

### Container Running but UI Not Loading

```bash
# Verify the container is running
docker ps

# Check logs for errors
docker logs data-prep-agent

# Test the backend API directly
curl http://localhost:8000/health
```

- If the backend responds but the UI does not load, wait 30–60 seconds for startup to complete
- Try accessing **http://127.0.0.1:8000** instead of `localhost`

---

## 🔒 Security Best Practices

For detailed security guidance — including API key protection, network hardening, and container security — see the [Security Policy](SECURITY.md).

**Key points:**

- Never commit `.env` files or API keys to version control
- Use `chmod 600 .env` to restrict file permissions
- For production deployments, use a reverse proxy with TLS and restrict network access
- Regenerate your API key immediately if it is accidentally exposed

---

## 📜 Legal & Security

Before using this software, please review:

- **[Terms of Use](TERMS_OF_USE.md)** — Legal agreement governing your use of this software
- **[Security Policy](SECURITY.md)** — How to report vulnerabilities and security best practices

By downloading or using the Data Preparation Agent, you agree to the Terms of Use.

---

## 📄 Documentation

- [Terms of Use](TERMS_OF_USE.md)
- [Security Policy](SECURITY.md)
- [Support Guide](SUPPORT.md)
- [Docker Compose Setup](#-docker-compose-optional)
- [Troubleshooting](#-troubleshooting)
- [Community Slack](https://link.emergence.ai/communityslack)

---

**Legal:** Usage subject to [Terms of Use](TERMS_OF_USE.md) | [Security Policy](SECURITY.md)
