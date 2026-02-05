# Security Policy

## Overview

This repository is maintained by Emergence AI and provides the Data Preparation Agent as a Docker image. We take the security of our systems and data seriously and appreciate the security community's efforts to responsibly disclose vulnerabilities.

For terms governing your use of this software, see [Terms of Use](TERMS_OF_USE.md). For installation and usage instructions, see [README](README.md).

## Supported Versions

We provide security updates for the following versions:

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |
| < Latest| :x:                |

We recommend always using the latest version of the Docker image to ensure you have the most recent security patches.

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

### How to Report

1. **Email us at**: [security@emergence.ai](mailto:security@emergence.ai)

2. **Include the following information**:
   - Type of vulnerability (e.g., authentication bypass, injection, etc.)
   - Detailed description of the vulnerability
   - Step-by-step instructions to reproduce
   - Proof of concept (if applicable)
   - Potential impact and severity assessment
   - Your contact information for follow-up

3. **Response Timeline**:
   - **Initial Response**: Within 48 business hours
   - **Status Update**: Within 5 business days
   - **Resolution Timeline**: Varies based on severity
     - Critical: 7–14 days
     - High: 14–30 days
     - Medium: 30–60 days
     - Low: 60–90 days

### What to Expect

- We will acknowledge receipt of your vulnerability report
- We will provide an estimated timeline for resolution
- We will keep you informed of our progress
- We will credit you for the discovery (unless you prefer to remain anonymous)
- We request that you do not publicly disclose the vulnerability until we have had adequate time to address it

## Security Best Practices for Users

### API Key Security

- **Never commit `.env` files** or API keys to version control
- **Use environment variables** for all sensitive configuration
- **Restrict file permissions** on files containing secrets:
  ```bash
  chmod 600 .env
  ```
- **Regenerate your key immediately** if it is accidentally exposed

### Data Protection

- **Understand what data is sent** to your LLM provider when using the Data Preparation Agent
- **Review your LLM provider's terms of service** and data handling practices
- **Do not process sensitive or regulated data** (HIPAA, FERPA, GLBA, CCPA) unless your LLM provider offers appropriate safeguards
- See the [Terms of Use](TERMS_OF_USE.md) for complete details on data handling responsibilities

### Network Security

For production deployments:

- **Run on a private network** using Docker network isolation:
  ```bash
  docker network create em-private
  docker run --network em-private ...
  ```
- **Use a reverse proxy** (nginx, Traefik) with TLS for any internet-facing deployments
- **Configure firewall rules** to restrict access to port 8000 to trusted networks only

### Container Security

- **Keep Docker images updated** — always pull the latest version:
  ```bash
  docker pull ghcr.io/emergenceai/em-data-preparation-agent:latest
  ```
- **Scan images for vulnerabilities** using tools like `docker scout`, Trivy, or Grype
- **Run containers as non-root** where possible
- **Limit container capabilities** and resources in production environments

## Compliance

Emergence AI's infrastructure and development practices comply with:

- **SOC 2 Type II** requirements
- **GDPR** for EU data processing

These standards apply to Emergence AI's internal infrastructure and development practices. Users are responsible for their own compliance obligations when using the Data Preparation Agent.

## Third-Party Dependencies

The Docker image includes third-party dependencies that are regularly scanned and updated. Emergence AI monitors for known vulnerabilities and releases updated images as needed.

## Incident Response

In the event of a security incident involving the Data Preparation Agent:

1. **Report it** to the Security Team at [security@emergence.ai](mailto:security@emergence.ai)
2. **Preserve evidence** where possible (logs, screenshots)
3. **Document** all relevant details including timestamps and affected systems

## Questions or Concerns

For any security questions or concerns, email: [security@emergence.ai](mailto:security@emergence.ai)

## Acknowledgments

We appreciate the security researchers and community members who help keep Emergence AI and our users safe. Responsible disclosure helps us maintain the security and integrity of our systems.

---

**Last Updated**: February 2026
**Policy Owner**: Chief Information Security Officer (CISO)
**Review Cycle**: Quarterly
