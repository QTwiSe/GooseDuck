# GooseDuck

# 🪿 GooseDuck

> A messenger hiding behind a goose mask — but packing a seriously legit system underneath. 🔒

## ✨ What makes it special

GooseDuck runs on a **custom encryption protocol** built on top of **ECDH**, souped up with built-in tricks that let it:

- 🌐 Keep working even under sovereign/restricted internet setups (looking at you, Russia 🇷🇺)
- 🕵️ Keep your data locked away from hackers trying to snoop

No corporate spyware vibes here — just a duck-and-goose crew doing encryption right. 🦆🔒

## 🔐 The KeyLock Protocol

Meet **KeyLock** — the ECDH-based encryption protocol running the show (yeah, ECDH again, you already know the drill 😏). Here's what's under the hood:

### 1. 📦 Padding
Junk bytes get tacked onto every message so each one weighs in at **exactly 1024 bytes**, no matter what. Uniform size = no easy pattern-sniffing.

### 2. 🔑 Key Generation
A shared seed gets fed into **XChaCha20-Poly1305**, spitting out a stream of random numbers. Messages get XOR'd against that seed, turning into pure **gibberish** for anyone snooping — and on top of that, it's disguised as **TLS 1.3** traffic.

### 3. 🌍 SNI Spoofing
Via a GET request, the SNI field gets stuffed with a link to an "allowed" site — think `ozon.ru`. Blends right in with normal traffic.

### 4. ⏱️ Intermediate Seed
Between the main seeds (which rotate every **5–10 minutes**), a short-lived **intermediate seed** kicks in for **~30–60 seconds** — and yep, it gets padded too.

### 5. 💀 Dead Loop
Instead of sending 1 packet, KeyLock fires off **3** — with 2 of them being pure padding decoys.

### 6. 🗑️ Junk Traffic
Every **30–60 seconds**, the messenger blasts out junk packets with randomized pauses in between, keeping traffic patterns unpredictable.

---

TL;DR: **KeyLock doesn't just encrypt your messages — it makes your traffic look boring, random, and completely unremarkable.** 🦢🔒
