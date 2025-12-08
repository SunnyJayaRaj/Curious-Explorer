# 🐛 Bug Report: GitHub Actions "Node.js 16 Deprecation"

**Date:** Dec 8, 2025 | **Context:** Project 4 (CI Pipeline)

## The Error
My workflow failed unexpectedly during the "Upload Artifact" step:

> **Error:** "This request has been automatically failed because it uses a deprecated version of `actions/upload-artifact: v3`."

## The Root Cause 🔍
Software evolves. GitHub updated their infrastructure and stopped supporting older versions of their standard actions.
* **My Code:** `uses: actions/upload-artifact@v3`
* **Reality:** v3 is deprecated and no longer allowed on new runners.

## The Fix
I had to manually bump the version number in my YAML file to the latest stable release.

```yaml
# OLD (Broken)
- uses: actions/upload-artifact@v3

# NEW (Fixed)
- uses: actions/upload-artifact@v4
```
## Lesson Learned
CI/CD pipelines are not `set and forget`. You must maintain your automation tools just like you maintain your code.
