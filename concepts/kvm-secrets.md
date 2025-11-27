# 🔐 KVMs: Keeping Secrets Secret

**Date:** Nov 27, 2025  | **Mood:** 🤫 Stealthy

## The Problem
I need to connect to a backend database, and it requires a password.
**Bad Idea:** Hardcoding the password in the XML file. ` <Password>Hunter2</Password> `.
Why? Because anyone with access to the repo (or the Apigee UI) can read it.

**Solution:** Key Value Maps (KVM).

## The Analogy: The Safe Deposit Box 🏦
Imagine a bank vault.
1.  **The Box:** I put the secret password inside a secure box named `Backend-Credentials`.
2.  **The Key:** I lock it.
3.  **The Proxy:** When the proxy runs, it has a special key to open the box, take the password, and use it *milliseconds* before sending it to the backend.

The developer never sees the password. The GitHub repo never sees the password. Only the running proxy sees it.

## Encrypted vs. Unencrypted
* **Unencrypted:** Like a sticky note on a desk. Good for config (e.g., "Timeout = 500ms").
* **Encrypted:** Like the Safe Deposit Box. Good for passwords. Once written, **you cannot read it back** via UI; the proxy can only *use* it.

## How to use it?
We use the `KeyValueMapOperations` policy to retrieve the data into a variable (see Flow Variables!).

```xml
<KeyValueMapOperations mapIdentifier="SecretsVault" name="Get-Password">
    <Get assignTo="private.backend_password">
        <Key>
            <Parameter>db_pass</Parameter>
        </Key>
    </Get>
</KeyValueMapOperations>
```
## TL;DR

Never hardcode passwords. Put them in a `KVM (Key Value Map)`. It separates "Code" from "Configuration."
