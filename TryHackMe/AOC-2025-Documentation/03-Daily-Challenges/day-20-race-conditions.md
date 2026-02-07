# Day 20: Race Conditions - Toy to The World

## 📋 Quick Facts
- **Date Completed:** December 20, 2025
- **Time Spent:** 1 hour
- **Difficulty:** ★★★☆ (Medium)
- **Category:** Web Application Security / Race Conditions / Burp Suite
- **Room URL:** https://tryhackme.com/room/race-conditions-aoc2025-d7f0g3h6j9

---

## 🎯 Challenge Overview

This challenge revisited **race conditions** in web applications using a Christmas-themed toy store scenario. The core idea was to exploit timing issues in how the application handled multiple simultaneous requests to gain an advantage (for example, buying items without enough balance or bypassing intended business logic). The room focused on understanding the vulnerability conceptually and then exploiting it in practice using Burp Suite.

**Learning Objectives:**
- Review what a race condition is in the context of web applications
- Understand how concurrent requests can cause inconsistent state
- Use Burp Suite to generate and send concurrent requests
- See how race conditions can lead to logic and financial abuse

---

## 💡 What I Learned

### Race Conditions – Concept Review

A **race condition** happens when:
- Two or more actions happen **very close together in time**
- The application’s behavior depends on the **order or timing** of these actions
- The developer assumed operations would happen **one at a time**, but in reality, multiple requests hit the server concurrently

In web apps, this often looks like:
- Two purchase requests at almost the same time
- Two balance updates in parallel
- Multiple submissions of the same form

If the server logic is not carefully designed with **locking, transactions, or atomic operations**, an attacker can:
- Spend the same balance twice
- Bypass stock or quantity checks
- Redeem the same coupon multiple times

This reinforced what was learned in Security+ with Professor Messer, but now with **hands-on exploitation** instead of just definitions.

### Using Burp Suite for Race Conditions

Previously, Burp Suite was used mainly to:
- Inspect HTTP traffic
- Find flags in CTFs

In this room, Burp Suite was used in a **new way**:
- Sending **multiple, nearly simultaneous requests** to the same endpoint
- Testing whether the application properly handled concurrent operations

Typical workflow:
1. Capture a normal request (e.g., purchase, balance update) in Burp.
2. Send it to a module (like Repeater or an extension) capable of firing multiple concurrent requests.
3. Launch a burst of requests at nearly the same time.
4. Observe if the application state becomes inconsistent (for example, buying more than allowed, or spending money not actually available).

This showed that even if the **business logic looks secure on paper**, timing issues can break it.

---

## 🤔 Challenges I Faced

- Mostly **review** of race conditions, which had already been covered in Security+.
- Main new part was **using Burp Suite differently**:
  - Not just passively watching traffic
  - Actively crafting and sending concurrent requests
- No major problems overall; 1 hour was enough to complete the room.

---

## ✅ How This Helps My Career

For a Blue Team / SOC / web security role, this room reinforces that:
- Web applications can be vulnerable not only due to **bad input validation**, but also due to **bad handling of concurrent operations**.
- Logs may show **multiple identical requests in a tiny time window** – this can be a sign of a race condition attack.
- Burp Suite is not just a CTF toy, but a **professional tool** for:
  - Testing web logic
  - Reproducing complex timing-based issues

This room strengthens understanding of **web app logic flaws**, which is valuable both for:
- Defenders (identifying and understanding weird behavior in logs)
- And for anyone later doing web app testing or bug bounties.
