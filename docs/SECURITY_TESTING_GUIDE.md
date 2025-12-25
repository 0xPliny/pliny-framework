# Security Testing Guide

**Version:** 1.0.0  
**Last Updated:** 2025-01-XX  
**Purpose:** Guide to using Pliny Framework for security testing and vulnerability assessment.

---

## Overview

Pliny Framework includes security testing capabilities inspired by Shannon AI Pentester. Use the **Sentinel** persona and **security_testing** domain module to perform comprehensive security assessments.

---

## Quick Start

### 1. Activate Sentinel Persona

Load the Sentinel persona into your AI assistant:

```bash
cat personas/sentinel.md | pbcopy  # Copy to clipboard
# Then paste into your AI assistant
```

Or use the CLI:

```bash
pliny --persona sentinel --framework rise --task "Security assessment of https://example.com"
```

### 2. Load Security Testing Module

```bash
pliny module load security_testing
```

### 3. Run Security Assessment

```bash
pliny security assess https://example.com /path/to/repo
```

---

## 5-Phase Security Testing Workflow

### Phase 1: Pre-Reconnaissance

External scanning and code analysis:

- Port scanning (nmap)
- Subdomain discovery (subfinder)
- Technology stack identification (whatweb)
- Static code analysis (CodeQL, Semgrep)

**Output:** Port scan results, subdomains, tech stack, code analysis

### Phase 2: Reconnaissance

Attack surface mapping:

- API endpoint discovery
- Authentication mechanism analysis
- Input point identification
- Data flow mapping

**Input:** Pre-recon results, source code  
**Output:** Attack surface map, entry points, API endpoints

### Phase 3: Vulnerability Analysis

Identify potential vulnerabilities (parallel execution):

- Injection vulnerabilities (SQL, Command, LDAP, XPath)
- Cross-Site Scripting (XSS) - Reflected, Stored, DOM-based
- Authentication flaws (bypass, weak passwords, session issues)
- Authorization flaws (IDOR, privilege escalation, forced browsing)
- Server-Side Request Forgery (SSRF)

**Output:** Vulnerability findings with confidence ratings

### Phase 4: Exploitation

Validate vulnerabilities with proof-of-concept (parallel execution):

- Create reproducible exploits
- Demonstrate impact
- Capture evidence (screenshots, logs, data)
- Document steps to reproduce

**Input:** Vulnerability findings  
**Output:** Exploitation evidence

### Phase 5: Reporting

Document findings with remediation guidance:

- Executive summary for stakeholders
- Technical details for developers
- Proof-of-concept demonstrations
- Remediation recommendations

**Input:** All findings and evidence  
**Output:** Executive and technical reports

---

## Vulnerability Types Covered

### Injection

- **SQL Injection** - Database query manipulation
- **Command Injection** - OS command execution
- **LDAP Injection** - LDAP query manipulation
- **XPath Injection** - XPath query manipulation

**Severity:** Critical

### Cross-Site Scripting (XSS)

- **Reflected XSS** - Non-persistent, reflected in response
- **Stored XSS** - Persistent, stored in database
- **DOM-based XSS** - Client-side manipulation

**Severity:** High

### Authentication

- **Authentication Bypass** - Circumventing authentication
- **Weak Passwords** - Predictable or default passwords
- **Session Fixation** - Session hijacking
- **Credential Stuffing** - Automated login attempts

**Severity:** Critical

### Authorization

- **IDOR** - Insecure Direct Object References
- **Privilege Escalation** - Gaining unauthorized privileges
- **Forced Browsing** - Accessing unauthorized resources
- **Insecure Direct Object References** - Direct access to objects

**Severity:** High

### Server-Side Request Forgery (SSRF)

- **Internal Access** - Accessing internal services
- **Cloud Metadata** - Accessing cloud instance metadata
- **Port Scanning** - Scanning internal network ports

**Severity:** High

---

## Using Sentinel Persona

### Activation

Paste the Sentinel persona into your AI assistant:

```
I need you to perform a security assessment of [target]
```

### Output Format

Sentinel provides findings in a standardized format:

```markdown
## [SEVERITY] Vulnerability Title

**Confidence:** [1-10]

### Description
[What the vulnerability is]

### Proof of Concept
[Steps to reproduce]

### Impact
[What an attacker could do]

### Remediation
[How to fix it]

### References
[OWASP, CVE, etc.]
```

---

## Configuration

### Security Testing Config

```yaml
task:
  name: "Security Assessment"
  domain: "security_testing"

execution:
  framework: "rise"
  parallel: true

phases:
  - name: vulnerability-analysis
    parallel: true
    agents: [injection, xss, auth, authz, ssrf]
```

---

## Standards and Methodology

### OWASP Testing Guide

Follow OWASP Testing Guide methodology for comprehensive assessments.

### CVSS Scoring

Use CVSS 3.1 to rate vulnerability severity:

- **Critical (9.0-10.0)** - Immediate action required
- **High (7.0-8.9)** - Address within 30 days
- **Medium (4.0-6.9)** - Address within 90 days
- **Low (0.1-3.9)** - Address in next release

### Reporting Standards

- **Executive Summary** - High-level overview for stakeholders
- **Technical Report** - Detailed findings for developers
- **Proof of Concepts** - Reproducible demonstrations
- **Remediation Guidance** - Step-by-step fixes

---

## Templates

Use security templates for consistent reporting:

- [Vulnerability Report](../templates/security/vulnerability_report.md) - Individual vulnerability documentation
- [Pentest Report](../templates/security/pentest_report.md) - Comprehensive penetration test report
- [Security Assessment](../templates/security/security_assessment.md) - Quick security assessment

---

## Related Documentation

- [Security Testing Module](../modules/security_testing.yaml) - Domain standards and patterns
- [Sentinel Persona](../personas/sentinel.md) - Security testing persona
- [R-I-S-E Framework](../frameworks/universal_rise.md) - Research → Identify → Synthesize → Execute
- [C-A-R-E Framework](../frameworks/universal_care.md) - Context → Analyze → Respond → Evaluate
- [MCP Integration](../integrations/mcp_integration.md) - Browser automation for testing
- [Browser Automation](../integrations/browser_automation.md) - Web application interaction

