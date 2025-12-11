# Nuclei Security Templates Repository

A comprehensive collection of advanced security vulnerability detection templates engineered for the [Nuclei](https://github.com/projectdiscovery/nuclei) framework. This repository provides production-grade YAML templates designed for automated vulnerability assessments, penetration testing, and security auditing across modern web applications and cloud infrastructure.

## 📋 Table of Contents

- [Overview](#overview)
- [Template Categories](#template-categories)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
- [Template Documentation](#template-documentation)
- [Contributing Guidelines](#contributing-guidelines)
- [Legal & Compliance](#legal--compliance)

## Overview

This template library encompasses **25+ advanced security detection modules** targeting:

- **API Security**: Endpoint validation, GraphQL vulnerabilities, SSRF detection
- **Cloud Infrastructure**: AWS credential exposure, S3 misconfiguration detection
- **Web Application Security**: CORS bypass, Open Redirects, SQL injection patterns
- **CMS Vulnerabilities**: WordPress-specific exploits and configuration issues
- **Infrastructure Hardening**: HTTP method enumeration, backup file discovery
- **Protocol Security**: CRLF injection, X-Forwarded header abuse, cache poisoning

## Template Categories

| Category | Templates | Focus Area |
|----------|-----------|-----------|
| **API & Web Services** | `api_endpoints.yaml`, `graphql_get.yaml`, `Swagger.yaml` | API discovery & validation |
| **Credential Exposure** | `credentials-disclosure-all.yaml`, `aws-access-secret-key.yaml` | Sensitive data leakage |
| **Cloud Security** | `s3-detect.yaml` | Cloud misconfiguration |
| **CMS Exploitation** | `wordpress-takeover.yaml`, `wp-setup-config.yaml` | WordPress vulnerabilities |
| **Protocol Attacks** | `cRlf.yaml`, `x-forwarded.yaml`, `nextjs-middleware-cache.yaml` | HTTP/Protocol exploitation |
| **Network Security** | `cors.yaml`, `openRedirect.yaml`, `response-ssrf.yaml` | Network-level attacks |
| **CVE Coverage** | `CVE-2025-29927.yaml` | Known vulnerability signatures |

## Prerequisites

- **Nuclei Framework**: v2.8.0 or higher
  ```bash
  go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
  ```
- **Go Runtime**: 1.18+
- **Supported Platforms**: Linux, macOS, Windows

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/coffinxp/nuclei-templates.git
cd nuclei-templates
```

### 2. Verify Template Syntax

Validate all templates before deployment:

```bash
nuclei -validate
```

### 3. Update Nuclei Database

```bash
nuclei -update
```

## Usage

### Basic Template Execution

```bash
# Run against a single target
nuclei -u https://target.com -t api_endpoints.yaml

# Run specific category
nuclei -u https://target.com -t ./wordpress-takeover.yaml

# Scan entire repository templates
nuclei -u https://target.com -t .
```

### Advanced Scenarios

#### 1. Batch Scanning with Input File

```bash
nuclei -l targets.txt -t credentials-disclosure-all.yaml -o results.json
```

#### 2. Filtered Execution by Severity

```bash
nuclei -u https://target.com -t . -severity high,critical
```

#### 3. Concurrent Scanning Optimization

```bash
nuclei -u https://target.com -t . -c 50 -rrl 100
```

**Parameters**:
- `-c`: Number of concurrent templates (default: 25)
- `-rrl`: Rate limit (requests per second)

#### 4. JSON Output for Integration

```bash
nuclei -u https://target.com -t . -o results.json -j
```

#### 5. Markdown Reporting

```bash
nuclei -u https://target.com -t . -o report.md -markdown
```

## Template Documentation

### Template Structure Reference

Each template adheres to the standardized Nuclei format:

```yaml
id: template-identifier
info:
  name: Vulnerability Name
  author: Author Name
  severity: high|medium|low|info
  description: Detailed description
  reference: https://example.com/reference

requests:
  - method: GET|POST|PUT
    path: /endpoint
    matchers:
      - type: status|word|regex
        condition: and|or
        part: body|header|response
```

### Key Template Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `id` | Unique template identifier | `aws-access-secret-key` |
| `severity` | Vulnerability criticality | `critical` |
| `tags` | Classification tags | `aws`, `credentials` |
| `matcher` | Detection logic | status code, regex patterns |

## Contributing Guidelines

### Quality Standards

- Follow Nuclei YAML specification strictly
- Include comprehensive template metadata
- Add multiple detection matchers for accuracy
- Test thoroughly before submission
- Document any external dependencies

### Submission Process

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-template`
3. Add your template with documentation
4. Validate syntax: `nuclei -validate`
5. Submit pull request with test results

## Legal & Compliance

### ⚠️ Mandatory Disclaimer

**This repository is intended for:**
- ✅ Authorized security testing and penetration testing
- ✅ Vulnerability research in controlled environments
- ✅ Educational purposes within ethical frameworks
- ✅ Security audit scenarios with explicit written authorization

**This repository is NOT intended for:**
- ❌ Unauthorized access to computer systems
- ❌ Malicious network activities
- ❌ Violation of computer fraud laws (CFAA, GDPR, etc.)
- ❌ Testing without explicit written permission

### User Responsibilities

**By using this repository, you acknowledge:**

1. **Authorization Requirement**: You have explicit written permission from system owners before conducting any security tests
2. **Legal Compliance**: You comply with all applicable laws and regulations in your jurisdiction
3. **Ethical Conduct**: You adhere to responsible disclosure practices and ethical hacking guidelines
4. **Liability Waiver**: The authors assume no liability for misuse, data loss, or legal consequences
5. **Indemnification**: You indemnify and hold harmless all contributors from legal action

### Compliance Frameworks

- **OWASP Testing Guide v4.2**
- **NIST Cybersecurity Framework**
- **PCI-DSS Security Standards**
- **GDPR Data Protection Requirements**

---

**Repository Maintainer**: coffinxp  
**Last Updated**: December 2025  
**License**: Educational Use Only  
**Status**: Active Development
