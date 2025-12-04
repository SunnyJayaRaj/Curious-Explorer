# Architectural Decision: JWT vs. OAuth 2.0 (Opaque)

In the Apigee Lab, I have implemented two distinct security models. This document defines when to use which based on my practical experience with **Project 1 (Weather)** and **Project 2 (Banking)**.

## 1. JWT (JSON Web Token)
* **Implemented in:** Weather-Shield-Gateway
* **Analogy:** A **Passport**.
    * The passport contains your data (name, country) printed right on it.
    * The "Border Agent" (API) trusts it because of the holographic seal (Signature).
    * They do not need to call your home country's database to verify it.
* **Best Use Case:** * passing context between internal microservices.
    * High-volume APIs where database latency is a bottleneck.

## 2. OAuth 2.0 (Opaque/Reference Token)
* **Implemented in:** Secure-Bank-Access
* **Analogy:** A **Hotel Key Card**.
    * The card is just a piece of plastic with a random ID. It has no personal data on it.
    * The "Door Lock" must check with the Front Desk system (Apigee) to see if the card is valid.
* **Best Use Case:** * **Banking/Enterprise:** If a token is stolen, it can be revoked instantly at the server.
    * **Public Apps:** No internal data (PII) is exposed in the token string.

## ⚡ The Decision Matrix

| Feature | JWT (Stateless) | OAuth Opaque (Stateful) |
| :--- | :---: | :---: |
| **Revocation** | Difficult (Requires expiry wait or blacklist) | **Instant** (Server-side kill switch) |
| **Performance** | **Fast** (No DB lookup) | Slower (Requires DB lookup) |
| **Data Visibility** | Claims are visible (Base64 decoded) | **Secure** (Random string only) |
| **My Recommendation** | Use for **Internal** Service-to-Service | Use for **Public** or **Sensitive** (Banking) APIs |
