# GooseDuck

> A messenger hiding behind a goose mask — but packing a seriously legit system underneath. 🔒
>
> <img width="1024" height="1024" alt="gooseducklogo" src="https://github.com/user-attachments/assets/7dcca4af-3874-4460-8221-1d7f363f8d63" />



## ✨ What makes it special

GooseDuck runs on a **custom encryption protocol** built on top of **ECDH**, souped up with built-in tricks that let it:

- 🌐 Stays resilient under heavy network restrictions and deep packet inspection (DPI)
- 🕵️ Keep your data locked away from hackers trying to snoop

No corporate spyware vibes here — just a duck-and-goose crew doing encryption right. 🦆🔒

## 🔐 The KeyLock Protocol

Meet **KeyLock** — the ECDH-based encryption protocol running the show (yeah, ECDH again, you already know the drill 😏). Here's what's under the hood:

### 1. 📦 Padding
Junk bytes get tacked onto every message so each one weighs in at **exactly 1024 bytes**, no matter what. Uniform size = no easy pattern-sniffing.

### 2. 🔑 Key Generation
A shared seed drives XChaCha20 to generate a keystream, which messages get XOR'd against — turning them into pure gibberish for anyone snooping. Poly1305 then adds an authentication tag on top, so tampering gets caught. All of it disguised as TLS 1.3 traffic.

### 3. 🌍 SNI Spoofing
Via a GET request, the SNI field gets stuffed with a link to an "allowed" site. Blends right in with normal traffic.

### 4. ⏱️ Intermediate Seed
Between the main seeds (which rotate every **5–10 minutes**), a short-lived **intermediate seed** kicks in for **~30–60 seconds** — and yep, it gets padded too.

### 5. 💀 Dead Loop
Instead of sending 1 packet, KeyLock fires off **3** — with 2 of them being pure padding decoys.

### 6. 🗑️ Junk Traffic
Every **30–60 seconds**, the messenger blasts out junk packets with randomized pauses in between, keeping traffic patterns unpredictable.

## 🆔 GDID — GooseDuckID (Anti-MITM System)

Meet **GDID** — a unique **6-character hash identifier**, always starting with `#` (e.g. `#A3F8B2`), auto-generated for every user **forever** at registration.

Here's the twist: **you can't see your own GDID** — you only ever see your contact's GDID. 👀

### How it stops MITM attacks

- 🔑 On registration, a **permanent keypair** is generated for the account — GDID is literally a **hash of that public key**.
- 🤝 During the handshake, both server and contact **sign their temporary key (A or B) with their permanent key**.
- 🚫 If an attacker tries to slip in and swap keys mid-handshake, the signature check fails — the interceptor **has no matching GDID** to fake it with.
- ✅ Once a contact verifies the other person's GDID **just once**, key-swapping becomes impossible after that — locked in for good.

*GDID can also include lowercase letters!

No more "trust on first use" guesswork — GDID makes sure the person you verified today is still the person you're talking to tomorrow. 🦆🔒

## ⚙️ KeyLock Subsystem (KLS)

**KLS (KeyLock Subsystem)** is the backbone of our encryption architecture, completely decoupled from the main GooseDuck (GD) application. We split the monolith into an independent, modular subsystem to achieve two major goals:

### 📦 1. Standalone Crypto Core (SDK)

The source code of the **KeyLock** protocol runs entirely separate from the GooseDuck GUI.
* **For Developers:** You can easily reference and integrate KLS into your own projects, apps, or services that require a custom, robust cryptography layer built on top of **ECDH** — without dragging the messenger's entire UI stack along with it.

### 🛡️ 2. Headless Tunneling & CLI (VPN Mode)

KLS can be deployed directly onto your machine as a lightweight background daemon.

* **For Power Users:** You can spin up the KeyLock protocol to tunnel your computer's network traffic, working effectively like a hardened VPN designed to stay resilient under heavy DPI.
* **CLI-Driven Control:** Manage your peers, routing tables, and cryptographic handshakes directly from the terminal using a clean and fast command-line interface.

---



## 🛠️ Tech Stack

| Layer | Tech |
|---|---|
| 🎨 UI/GUI | **Avalonia UI** |
| 🌐 Networking | **ASP.NET Core** |
| 🗄️ Database (SQL) | **Entity Framework Core + PostgreSQL** |
| 🔐 Encryption | **NSec** |

Cross-platform from the ground up, built with a modern .NET stack. 🦆⚡

## ❗ PAY ATTENTION ❗

The project is currently in the active development stage. We are actively implementing our ideas and resolving technical challenges as they arise.Full-scale production and regular updates are scheduled to begin during our nearest upcoming free time!
P.S - 

The code is already written but not yet published. I will publish it at the first opportunity!»

---

TL; DR: **KeyLock doesn't just encrypt your messages — it makes your traffic look boring, random, and completely unremarkable.** 🦢🔒

---

## © by QTwiSe Studio ©
