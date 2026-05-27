# 🔐 SecureVault

### Secure Login System — Project #4

> A production-inspired authentication system built with browser-native APIs only — no auth frameworks, no crypto libraries, no dependencies.

---

## 📚 Table of Contents

* [About](#-about-the-project)
* [Features](#-features)
* [Screenshots](#-screenshots)
* [Security Architecture](#-security-architecture)
* [Tech Stack](#-tech-stack)
* [How It Works](#-how-it-works)
* [Security Measures](#-security-measures)
* [Getting Started](#-getting-started)
* [What I Learned](#-what-i-learned)
* [Roadmap](#-roadmap)
* [Links](#-links)

---

# 🚀 About The Project

SecureVault is **Project #4** in my web development journey — a fully functional secure login system implementing real-world security standards used in production applications.

Most tutorials stop at building login forms. This project goes deeper by implementing:

* Password hashing
* Session security
* Timing attack prevention
* TOTP-based 2FA
* CSRF protection
* Rate limiting
* Secure authentication flows

All implemented using **browser-native APIs only**.

### 🎯 Challenge

Build a complete authentication system with:

* ❌ No bcrypt package
* ❌ No JWT library
* ❌ No authentication framework
* ❌ No npm dependencies

### ✅ Result

A fully working authentication system featuring:

* PBKDF2-SHA256 hashing
* TOTP 2FA
* Rate limiting
* CSRF protection
* Secure session handling
* Input sanitization
* Anti-timing attack protection

---

# 🌐 Live Demo

## 🔗 Demo URL

```bash
https://claude.ai/public/artifacts/2a420bc4-679a-4615-864d-482c32076a8c
```

## 🧪 Demo Credentials

| Field    | Value       |
| -------- | ----------- |
| Username | `demo`      |
| Password | `Demo@1234` |

> 💡 All data is stored in-memory only. Refreshing the page resets the demo.

---

# ✨ Features

## 🔐 Password Hashing

* PBKDF2-SHA256
* 100,000 iterations
* Unique random salt per user
* Browser-native Web Crypto API

## 📱 Two-Factor Authentication

* RFC 6238 compliant TOTP
* Compatible with:

  * Google Authenticator
  * Authy
  * Bitwarden

## 🚫 Rate Limiting

* Account lockout after 5 failed attempts
* 30-second cooldown
* Protection against brute force attacks

## ⏱ Session Management

* Cryptographically secure session tokens
* Sliding 30-minute expiry
* Secure logout handling

## 🛡 Timing Attack Prevention

* Password hashing occurs even for invalid usernames
* Prevents username enumeration through response timing

## 🔒 CSRF Protection

* Cryptographically random CSRF token
* Bound to active session

## ✅ Input Validation

* XSS character stripping
* Real-time validation
* Sanitized user inputs

## 📊 Security Dashboard

* Session details
* Security score
* Activity log
* 2FA status

---

# 📸 Screenshots

## 🔑 Login Screen

* Secure sign-in form
* Remember device option
* Password visibility toggle
* Security indicators

## 📝 Registration Screen

* Live username validation
* Password strength meter
* Optional 2FA setup

## 📱 2FA Setup

* QR code generation
* Manual secret support
* TOTP verification flow

## 📊 Dashboard

* Active session details
* Security score
* Activity tracking
* 2FA management

---

# 🏗 Security Architecture

## Registration Flow

```text
User Input
   ↓
Validate & Sanitize
   ↓
PBKDF2-SHA256 Hashing
   ↓
Store Hash + Salt
   ↓
Optional TOTP Setup
```

## Login Flow

```text
Login Attempt
   ↓
Rate Limit Check
   ↓
PBKDF2 Password Compare
   ↓
2FA Verification
   ↓
Create Secure Session
```

---

# 🧰 Tech Stack

| Technology        | Purpose                   |
| ----------------- | ------------------------- |
| HTML5             | Semantic markup           |
| CSS3              | UI styling & animations   |
| JavaScript ES2020 | Core application logic    |
| Web Crypto API    | Native cryptography       |
| PBKDF2-SHA256     | Password hashing          |
| TOTP RFC 6238     | Two-factor authentication |
| GitHub Pages      | Deployment                |

---

# ⚙️ How It Works

## 🔐 Password Hashing (PBKDF2)

```javascript
// Each user gets a unique cryptographic salt
const salt = generateSalt();

// PBKDF2 with 100,000 iterations
const hash = await crypto.subtle.deriveBits({
  name: "PBKDF2",
  salt,
  iterations: 100000,
  hash: "SHA-256"
}, keyMaterial, 256);
```

---

## 📱 TOTP Authentication

```javascript
// counter = floor(unix_timestamp / 30)
const counter = Math.floor(timeStep / 30);

const key = await crypto.subtle.importKey(
  "raw",
  base32ToBytes(secret),
  { name: "HMAC", hash: "SHA-1" },
  false,
  ["sign"]
);
```

---

## ⏱ Timing Attack Prevention

```javascript
// Always hash even for invalid usernames
if (!user) {
  await hashPassword(password, 'dummysalt');
}

const hash = await hashPassword(password, user.salt);
```

---

# 🛡 Security Measures

| Measure            | Implementation                    | Protects Against     |
| ------------------ | --------------------------------- | -------------------- |
| PBKDF2-SHA256      | 100k iterations + unique salt     | Brute force attacks  |
| TOTP 2FA           | RFC 6238 HMAC-SHA1                | Credential theft     |
| Rate Limiting      | 5 failed attempts → cooldown      | Credential stuffing  |
| Anti-Timing        | Constant-time authentication flow | Username enumeration |
| CSRF Tokens        | Random session-bound tokens       | CSRF attacks         |
| Input Sanitization | Strip dangerous characters        | XSS injection        |
| Session Expiry     | Sliding expiration window         | Session hijacking    |

---

# 🚀 Getting Started

 Open Directly:
https://claude.ai/public/artifacts/2a420bc4-679a-4615-864d-482c32076a8c

# 📖 What I Learned

## 1. Crypto Is Nuanced

PBKDF2 is more than hashing + salt. Iteration count and entropy matter.

## 2. Timing Attacks Are Real

Even tiny response time differences can leak sensitive information.

## 3. TOTP Is Elegant

2FA is fundamentally HMAC + time-based counters.

## 4. Defense In Depth Matters

No single security layer is enough.

## 5. Browser Crypto APIs Are Powerful

Modern browsers include serious cryptographic capabilities.

---

# 🗺 Roadmap

## ✅ Completed

* PBKDF2 password hashing
* Input sanitization
* Rate limiting
* Session management
* CSRF protection
* TOTP 2FA
* Security dashboard

## 🔄 Planned

* IndexedDB persistence
* OAuth login (Google/GitHub)
* WebAuthn / Passkeys
* WCAG accessibility improvements

---

# 🔗 Links

## 🚀 Live Demo

```bash
https://claude.ai/public/artifacts/2a420bc4-679a-4615-864d-482c32076a8c
```

## 💻 GitHub Repository

```bash
https://github.com/Ayan773/SecureVault-Secure-Login-System
```

## 👨‍💼 LinkedIn

```bash
https://www.linkedin.com/in/ayan-saifi
```

## 📧 Contact

```bash
ayansaifibca@gmail.com
```

---

# ⭐ Support

If you found this project helpful:

* ⭐ Star the repository
* 🍴 Fork the project
* 🛠 Contribute improvements
* 🐛 Report issues

---

# 📜 License

This project is licensed under the MIT License.

---

# ❤️ Final Note

> “Security isn't a feature — it's a mindset baked into every line of code.”

Built with ❤️ as part of my Web Development Journey.

---

