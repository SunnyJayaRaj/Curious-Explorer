# 🛑 Spike Arrest vs. Quota: What's the difference?

**Date:** Nov 27, 2025 | **Mood:** ⚖️ Balanced

## The Problem
Both of these policies "limit traffic."
* **Spike Arrest:** Limits the *rate* (Protection).
* **Quota:** Limits the *count* (Business/Monetization).
Beginners (like me) always confuse them.

## The Analogy: The Nightclub 🕺
### 1. The Bouncer (Spike Arrest)
The Bouncer stands at the door. He doesn't care who you are. He only cares about **crowd safety**.
* **Rule:** "I only let in 1 person every 10 seconds."
* **Goal:** Protect the club from catching fire (Server Crash).
* **If you fail:** He pushes you back immediately. (Default Error: HTTP 503 Service Unavailable).

### 2. The Bartender (Quota)
The Bartender knows exactly who you are. He checks your membership card (API Key).
* **Rule:** "Your Silver Membership allows 5 drinks per night."
* **Goal:** Make money and enforce business tiers.
* **If you fail:** He says "You've had enough, come back tomorrow". (Default Error: HTTP 429 Too Many Requests).

## When to use which?
| Feature | Spike Arrest | Quota |
| :--- | :--- | :--- |
| **Protects...** | The Backend Server (Infrastructure) | The Business Model (Revenue) |
| **Resets...** | Every second/minute (Smoothing) | Every day/month (Calendar) |
| **Focus...** | Preventing Peaks | Enforcement of Limits |

## TL;DR
Use **Spike Arrest** to stop hackers from crashing your server.
Use **Quota** to limit how much a user can consume based on what they paid.
