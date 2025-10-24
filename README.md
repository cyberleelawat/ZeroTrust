# ZeroTrace

ZeroTrace is a **lightweight, offline-first, privacy-respecting password obfuscation tool** with a neon/glass UI and Matrix rain aesthetic. It generates a **deterministic obfuscated string** from your input, so you only need to remember the original phrase.

> ⚠️ **Note:** This is deterministic obfuscation, **not cryptographic encryption**.

---

## Highlights

- Glassmorphism UI, neon glow, cursor-reactive effects  
- Matrix rain background with a toggle (雨) in the top-right  
- URL-safe mode toggle to avoid characters that break in URLs/forms  
- Live length counter (8–20) and input max length enforcement  
- Copy to clipboard with accessible toast notifications  
- PWA support (installable, basic offline via service worker)  
- No data stored; runs entirely client-side  

---

## New Features (Added)

### 1. Password Strength & Crack Time Estimator
- Uses **zxcvbn** (client-side) to estimate password strength and present human-readable crack-time estimates (e.g., "centuries", "hours", "instant").  
- Shows the estimated crack time next to the generated/entered password so you can judge how strong the original phrase is before obfuscation.

### 2. Email / Phone Breach Checker
- Integrates with **Have I Been Pwned (HIBP)** to check if an **email address** appears in known public breaches.  
- Phone-number breach checks are more limited (HIBP phone checks require different endpoints / paid access) — current implementation focuses on **email** checks and explains how to add phone checks if you have an appropriate API/service.
- **Important:** HIBP requires an **API key** for requests. The tool provides an input field that calls HIBP only from the client if an API key/configuration is supplied (no email data is sent anywhere else by default).

---

## How it works (high level)

The generator applies a series of **deterministic transformations** to the input (seeded by a simple hash). In short:

1. Caesar-style character shift  
2. Uppercase substitutions based on position and hash  
3. Appends code-themed characters (from a language name set)  
4. Appends a deterministic word token (e.g., `-matrix-`)  
5. Inserts a digit and a symbol at fixed positions (hash-driven)  
6. Reverse the string  
7. Insert lowercase chars at intervals (hash-driven)  
8. Deterministic permutation  
9. Trim to 8–20 characters and add a final symbol  

✅ Same input always yields the **same output**.

---

## URL-safe mode (why and when)

Certain characters (space, quotes, `%`, `&`, `?`, `#`, etc.) can break or get auto-encoded when used in URLs, QR codes, command lines, or strict forms. The **URL-safe toggle** ensures:

- Only a restricted symbol set is used for insertions (default: `-_.~@`)  
- The final output is sanitized to contain only `A–Z a–z 0–9 - _ . ~ @`  

💡 Enable URL-safe when you plan to embed the generated string inside a **URL, query parameter, QR code**, or systems that reject special characters.

---

## Matrix rain toggle

- The round icon with the character `"雨"` (top-right) toggles the **Matrix rain animation**  
- Honors `prefers-reduced-motion` and is cached for offline use  

---

## Why ZeroTrace? (use cases)

- Create consistent, memorable obfuscated strings from names/phrases you already remember  
- Avoid reusing raw passwords in public or semi‑trusted contexts by using a deterministic transformation  
- Generate tokens to paste into places that may dislike special characters (enable URL-safe mode)  
- Use fully offline without sending data to any server; **privacy by design**  

---

## Examples / Demo


**Password strength / crack-time example (using zxcvbn)**  
- `password` → Score 0 → `Estimated crack time: instantly`  
- `Leelawat@2025` → Score 3 → `Estimated crack time: years`  
- `My$Tr0ngPhr@se2025` → Score 4 → `Estimated crack time: centuries`

**Email breach example (HIBP)**  
- `user@example.com` → `Found in 3 breaches: Adobe, LinkedIn, MySpace`  
- `someone@freshdomain.xyz` → `No breaches found`

---

| Input                  | Output (obfuscated)                 | URL-safe variant                  |
|------------------------|-----------------------------------|----------------------------------|
| `Leelawat@2025`        | `kL9O-Hmatrix-S`                  | `kL9O-Hmatrix-S`                 |
| `Cyber_Leelawat`       | `mR4Q-alpha-C`                    | `mR4Q-alpha-C`                   |
| `MySecret123!`         | `pT2Z-gamma-E`                    | `pT2Z-gamma-E`                   |

> The obfuscated string is **deterministic**: same input always produces the same output.

---
Link 
https://cyberleelawat.github.io/ZeroTrust
