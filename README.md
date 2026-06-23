# 🔐 Web Application Security Assessment
### OWASP Juice Shop — Cybersecurity Internship | Week 1

![Security](https://img.shields.io/badge/Security-Assessment-red)
![Tools](https://img.shields.io/badge/Tools-OWASP%20ZAP%20%7C%20Browser%20DevTools-blue)
![Status](https://img.shields.io/badge/Status-Completed-green)

---

## 📋 Overview

This repository contains the Week 1 Security Assessment conducted on the **OWASP Juice Shop** — an intentionally vulnerable web application used for cybersecurity training. The goal was to identify and document common web application vulnerabilities using both manual testing techniques and automated scanning tools.

---

## 🎯 Target Application

| Field | Details |
|---|---|
| Application | OWASP Juice Shop v20.0.0 |
| Type | Intentionally Vulnerable Web App |
| Environment | Local — http://localhost:3000 |
| Purpose | Security Training & Assessment |

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **OWASP ZAP 2.17.0** | Automated vulnerability scanning |
| **Browser Developer Tools** | Manual network inspection & payload testing |
| **Manual Testing** | XSS & SQL Injection payloads |

---

## 🔍 Vulnerabilities Found

| # | Vulnerability | Severity | Status |
|---|---|---|---|
| 1 | SQL Injection — Authentication Bypass | 🔴 Critical | Confirmed |
| 2 | Cross-Site Scripting (DOM-based XSS) | 🟠 High | Confirmed |
| 3 | Password Transmitted Over HTTP (No HTTPS) | 🟡 Medium | Confirmed |
| 4 | Missing Content-Security-Policy Header | 🟡 Medium | Confirmed |
| 5 | CORS Misconfiguration — Wildcard Origin | 🟡 Medium | Confirmed |
| 6 | Server Timestamp Disclosure | 🟢 Low | Confirmed |

---

## 🧪 Testing Methodology

### 1. Manual XSS Test
Injected the following payload into the search field:
```
<img src=x onerror=alert('XSS')>
```
**Result:** JavaScript executed successfully — alert popup triggered ✅

### 2. SQL Injection Test
Injected the following payload into the login email field:
```
' OR 1=1--
```
**Result:** Successfully logged in as Admin without valid credentials ✅

### 3. Network Inspection
Used Browser DevTools → Network tab to inspect registration request.
**Result:** Password transmitted in plaintext over HTTP ✅

### 4. Automated Scan
Ran OWASP ZAP Automated Scan against `http://localhost:3000`
**Result:** 4 alert categories found — CSP missing, CORS wildcard, timestamp disclosure ✅

---

## 📁 Repository Structure

```
web-app-security-assessment/
├── README.md
├── reports/
│   └── Security_Assessment_Report.pdf
├── screenshots/
│   ├── xss-vulnerability.png
│   ├── sql-injection-bypass.png
│   └── zap-scan-results.png
└── findings/
    └── vulnerabilities.md
```

---

## 📄 Report

The full professional security assessment report is available in the `/reports` folder. It includes:
- Executive Summary
- Scope & Methodology
- Detailed findings with evidence
- Impact analysis
- Remediation recommendations

---

## ⚠️ Disclaimer

This assessment was conducted on a **local, intentionally vulnerable application** (OWASP Juice Shop) for **educational purposes only** as part of a Cybersecurity Internship training task. No real systems were tested or harmed.

---

## 👩‍💻 Author

**Bushra** — Cybersecurity Intern  
Week 1 — Security Assessment Task  
June 2026
