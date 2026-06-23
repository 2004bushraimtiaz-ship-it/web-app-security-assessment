# 🔴 Vulnerability Findings — OWASP Juice Shop

**Assessment Date:** June 2026  
**Tester:** Bushra — Cybersecurity Intern  
**Target:** OWASP Juice Shop (localhost:3000)

---

## Finding 1 — SQL Injection (Authentication Bypass)
- **Severity:** 🔴 CRITICAL
- **Location:** Login form — POST /rest/user/login
- **Payload Used:** `' OR 1=1--`
- **Result:** Logged in as Admin without any valid credentials
- **Impact:** Complete authentication bypass — attacker gains admin access without a password
- **Fix:** Use parameterized queries / prepared statements. Never concatenate user input into SQL queries.

---

## Finding 2 — Cross-Site Scripting (DOM-based XSS)
- **Severity:** 🟠 HIGH
- **Location:** Search field — /#/search
- **Payload Used:** `<img src=x onerror=alert('XSS')>`
- **Result:** JavaScript executed — alert popup displayed
- **Impact:** Attacker can run malicious scripts in victim's browser, steal session cookies, redirect users
- **Fix:** Sanitize and encode all user input before rendering. Implement Content-Security-Policy header.

---

## Finding 3 — Password Transmitted Over Unencrypted HTTP
- **Severity:** 🟡 MEDIUM
- **Location:** Registration request — POST /api/Users/
- **Evidence:** Browser DevTools → Network → Payload tab showed password in plaintext
- **Impact:** Password can be intercepted via Man-in-the-Middle attack on unsecured networks
- **Fix:** Enforce HTTPS/TLS across the entire application. Enable HSTS header.

---

## Finding 4 — Missing Content-Security-Policy (CSP) Header
- **Severity:** 🟡 MEDIUM
- **Location:** All HTTP responses (application-wide)
- **Detected By:** OWASP ZAP automated scan
- **Impact:** No restriction on which scripts can execute — increases XSS impact
- **Fix:** Set CSP header via helmet.js middleware: `app.use(helmet())`

---

## Finding 5 — CORS Misconfiguration (Wildcard Origin)
- **Severity:** 🟡 MEDIUM
- **Location:** API responses — Access-Control-Allow-Origin: *
- **Detected By:** OWASP ZAP + manual header inspection
- **Impact:** Any website can make cross-origin requests to the API and read responses
- **Fix:** Restrict CORS to specific trusted domains only

---

## Finding 6 — Server Timestamp Disclosure
- **Severity:** 🟢 LOW
- **Location:** HTTP response headers
- **Detected By:** OWASP ZAP automated scan
- **Impact:** Internal timestamps leak server configuration info — aids attacker reconnaissance
- **Fix:** Remove unnecessary timestamp fields from API responses

---

## Summary Table

| # | Vulnerability | Severity | Tool Used | Fixed in Week 2? |
|---|---|---|---|---|
| 1 | SQL Injection | Critical | Manual | ✅ Yes |
| 2 | DOM-based XSS | High | Manual | ✅ Yes |
| 3 | Plaintext Password over HTTP | Medium | DevTools | ✅ Yes |
| 4 | Missing CSP Header | Medium | OWASP ZAP | ✅ Yes |
| 5 | CORS Misconfiguration | Medium | OWASP ZAP | ✅ Yes |
| 6 | Timestamp Disclosure | Low | OWASP ZAP | ✅ Yes |
