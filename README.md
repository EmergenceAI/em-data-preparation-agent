# 🚀 Data Preparation Agent - Quick Start Guide

Transform messy Excel files into clean, analytics-ready data with AI! This guide shows you how to run the Data Preparation Agent using Docker.

---

## ⚡ Quick Start (3 Steps)

### Step 1: Get Your Free Gemini API Key

1. Go to https://makersuite.google.com/app/apikey
2. Sign in with your Google account
3. Click **"Create API Key"**
4. Copy your key (looks like: `AIzaSyC_xxxxxxxxxxxxxxxxx`)

### Step 2: Pull the Docker Image

```bash
docker pull ghcr.io/emergenceai/em-data-preparation-agent:latest
```

### Step 3: Run the Application

**Option A: Enter API key later via UI** (Easiest)
```bash
docker run -d -p 8000:8000 --name data-prep-agent ghcr.io/emergenceai/em-data-preparation-agent:latest
```

**Option B: Provide API key at startup**
```bash
docker run -d \
  --name data-prep-agent \
  -p 8000:8000 \
  -e GEMINI_API_KEY="your-gemini-api-key-here" \
  -v $(pwd)/data:/app/data \
  ghcr.io/emergenceai/em-data-preparation-agent:latest
```

**That's it!** Open your browser to http://localhost:8000

💡 **If you didn't provide the API key**, you'll be prompted to enter it in the UI when you first use the app.

---

## ⚠️ Security & Privacy Notice

**IMPORTANT - Please read before using:**

### What Data is Processed
- **Your uploaded Excel files** are sent to Google Gemini API for AI-powered analysis
- **File contents and your transformation requests** are processed on Google's servers
- **No data is stored by us** - everything stays local except API calls to Google
- Review [Google Gemini API Privacy Policy](https://policies.google.com/privacy)

### Security Considerations
- **AI Code Execution**: This tool generates and executes Python code. Only process trusted files.
- **Code Obfuscation**: The application code is obfuscated and cannot be audited
- **API Key Security**: Your Gemini API key stays in your local environment
- **Internet Required**: Active internet connection needed for AI processing

⚠️ **Do not process sensitive, confidential, or regulated data** (PII, PHI, financial records) unless you've reviewed Google's data processing terms and your organization allows it.

---

## 📋 What You Need

✅ **Docker** - [Download here](https://www.docker.com/products/docker-desktop/)  
✅ **Gemini API Key** 
✅ **4GB RAM** minimum (8GB recommended)  
✅ **10GB disk space**

---

## 🎯 Using the Application

Once the container starts:

1. **Open your browser** to http://localhost:8000
2. **Upload your Excel file** (drag & drop)
3. **System will auto detect all the tables and show**
4. **You can clean or optimize the data using the transformation options**
5. **Describe what you want** - e.g., "Get the top 10 customers by revenue"
6. **Review and confirm** the transformation plan
7. **View clean CSV** files ready for analysis!

**Features:**
- 📊 Automatically detects tables in messy Excel sheets
- 🤖 Emergence GEN-AI-powered task transformation.
- ✅ Preview and approve before transforming
- 💾 Export to clean CSV files

---

## 🔄 Managing the Container

### Check if it's running
```bash
docker ps
```

### View logs
```bash
docker logs data-prep-agent -f
```

### Stop the container
```bash
docker stop data-prep-agent
```

### Restart the container
```bash
docker start data-prep-agent
```

### Remove the container
```bash
docker rm -f data-prep-agent
```

---

## 💾 Your Data is Safe

All your files are saved in the `./data` folder on your computer:

```
./data/
├── uploads/           # Your uploaded Excel files
├── temp_processing/   # Temporary working files
└── outputs/           # Transformed CSV outputs
```

## 🔧 Advanced: Docker Compose (Optional)

If you prefer Docker Compose for easier management:

**1. Create `.env` file:**
```bash
echo 'GEMINI_API_KEY="your-gemini-api-key-here"' > .env
```

**2. Create `docker-compose.yml`:**
```yaml
version: '3.8'

services:
  data-prep-agent:
    image: ghcr.io/emergenceai/em-data-preparation-agent:latest
    container_name: data-prep-agent
    ports:
      - "8000:8000"
    environment:
      - GEMINI_API_KEY=${GEMINI_API_KEY}  # Optional - can also be entered in UI
    volumes:
      - ./data:/app/data
    restart: unless-stopped
```

💡 **Note**: The `GEMINI_API_KEY` environment variable is optional. If not provided, you'll be prompted to enter it in the UI.

**3. Run:**
```bash
docker-compose up -d      # Start
docker-compose logs -f    # View logs
docker-compose down       # Stop
```

---

## ❓ Troubleshooting

### Issue: Container Fails to Start

**Error**: Container exits immediately after starting

**Solution**:
```bash
# Check logs for error message
docker logs data-prep-agent

# Note: API key is optional - you can enter it in the UI
# Only set GEMINI_API_KEY if you want to pre-configure it
```

### Issue: "GEMINI API KEY REQUIRED" Error

**Error**: Large error message about missing API key

**Solution**:
1. Verify your .env file exists and contains the correct key
2. Check that you're passing the environment variable correctly:
   ```bash
   docker run -e GEMINI_API_KEY="your-actual-key" ...
   ```

### Issue: API Returns 401/403 Errors

**Error**: Authentication failures when making API calls

**Solution**:
1. Verify your Gemini API key is valid at https://makersuite.google.com/app/apikey
2. Check if you've exceeded API quota (unlikely with free tier)
3. Ensure no extra spaces or quotes in the API key

### Issue: Port Already in Use

**Error**: `Bind for 0.0.0.0:8000 failed: port is already allocated`

**Solution**:
```bash
# Use different ports
docker run -d \
  -p 8001:8000 \  # Changed from 8000
  --name data-prep-agent \
  ghcr.io/emergenceai/em-data-preparation-agent:latest
```

### Issue: Container Running but UI Not Loading

**Diagnosis**:
```bash
# Check if container is running
docker ps

# Check logs for errors
docker logs data-prep-agent

# Test backend API directly
curl http://localhost:8000/health
```

**Solution**:
- If backend responds but UI doesn't load, wait 30-60 seconds for startup
- Check if port 8000 is accessible from your browser
- Try accessing http://127.0.0.1:8000 instead of localhost

---

## 🔒 Security Best Practices

### Protecting Your API Key

1. **Never commit .env files to git**
   ```bash
   echo ".env" >> .gitignore
   ```

2. **Use environment variable**
   ```bash
   # Set in your shell profile or systemd service
   export GEMINI_API_KEY="your-key"
   ```

3. **Restrict file permissions**
   ```bash
   chmod 600 .env  # Only owner can read/write
   ```

### Network Security

For production deployments:

```bash
# Run on private network
docker network create em-private
docker run --network em-private ...

# Use reverse proxy (nginx, traefik) for SSL
# Expose only ports 443 and 80 to internet
```

### Keep Your API Key Safe

**Don't:**
- ❌ Share your API key publicly
- ❌ Commit it to GitHub
- ❌ Post it in screenshots

**Do:**
- ✅ Use `.env` files (more secure than command line)
- ✅ Keep `.env` files out of version control
- ✅ Regenerate your key if accidentally exposed

---

## 💡 Tips

- **First time?** Start with a small Excel file to test
- **Sample files?** Check the `data/sample_files/` folder for example Excel files to try
- **Big files?** The app can handle up to 50MB Excel files.
- **Multiple tables?** The AI detects and processes them separately
- **Need help?** Check the logs with `docker logs data-prep-agent -f`

---

## 📞 Support

Thank you for your interest in the Data Preparation Agent. This repository provides container access and documentation for evaluation and integration purposes. Support is provided on a best-effort basis.

### Getting Help

#### Bug Reports

If you believe you have found a reproducible issue, please open a GitHub Issue using the Bug Report template and include:

- Container version
- Deployment environment (OS, cloud, runtime)
- Steps to reproduce
- Relevant logs or error messages (sanitized)

Issues that cannot be reproduced or lack sufficient information may be closed.

#### Feature Requests

Feature requests and enhancement suggestions are welcome. Please open a GitHub Issue using the Feature Request template and describe:

- The problem you are trying to solve
- The expected behavior
- Any relevant context or constraints

Feature requests are reviewed periodically. Implementation is not guaranteed.

#### Usage Questions

Please review the documentation in this repository before opening an issue. If your question relates to architecture, enterprise integration, or production deployment, please contact us directly.

#### Security Issues

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, email us at: **support@emergence.ai**

Include a detailed description of the issue so our team can investigate promptly.

#### Response Expectations

- Issues are reviewed periodically
- Response times are not guaranteed
- Support via GitHub is limited to reproducible defects and documented behavior

### Enterprise Support

For enterprise deployments, production use cases, or integration discussions, please contact: **support@emergence.ai**

---

**Last Updated**: February 2026  
**Version**: Latest
