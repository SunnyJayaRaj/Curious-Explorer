# 🐛 Bug Report: The "Site Can't Be Reached" Error

**Date:** Dec 1, 2025 | **Context:** First Cloud Deployment

## The Error
I successfully deployed my proxy to Google Cloud. I got the Green Checkmark ✅.
But when I clicked the provided URL (`https://...apigee.net`), I got this browser error:

> **ERR_NAME_NOT_RESOLVED**
> "This site can't be reached. Server IP address could not be found."

## The Investigation
1.  **Was the proxy down?** No, Apigee said it was "Deployed".
2.  **Was the internet down?** No.
3.  **The Clue:** I checked **Admin > Environments > Groups**.

## The Root Cause 🔍
I was trying to use a generic hostname that Google assigns by default, but my specific Evaluation Organization hadn't set up the DNS for it yet.
Instead, Google had assigned me a **`nip.io`** address (a wildcard DNS service that points directly to an IP address).

* **Bad URL:** `resonant-amulet...apigee.net` (DNS lookup failed)
* **Good URL:** `35.186.244.11.nip.io` (Points directly to the Load Balancer IP)

## The Fix
Always check the **Environment Group Hostnames** list. Do not assume the URL pattern.
Once I switched to the `.nip.io` address, the API responded immediately.

## Lesson Learned
Just because the code is deployed doesn't mean the **Door (DNS)** is open. Always check the Hostname configuration first.
