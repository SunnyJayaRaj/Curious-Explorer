# 🐛 Bug Report: "Bundle contains errors" (Name Mismatch)

**Date:** Dec 4, 2025 | **Context:** Deploying Project 2

## The Error
When uploading my `apiproxy.zip` to Google Cloud, the deployment failed immediately with:

> **Violation details:**
> "The root element name attribute 'default' must match the filename 'proxy-endpoint-default.xml'"

## The Root Cause 🔍
Apigee is extremely strict about naming.
* **My File Name:** `proxy-endpoint-default.xml`
* **My Code Inside:** `<ProxyEndpoint name="default">`

In most coding languages, the filename doesn't matter. In Apigee XML, they **must match perfectly**.

## The Fix
I had to edit the XML to match the filename.

**1. Fix the Proxy Name (Top of file):**
```xml
Change lines: <ProxyEndpoint name="default"> → <ProxyEndpoint name="proxy-endpoint-default"> 
```
**2. Fix the RouteRule (Bottom of file):** Since I also renamed the Target file, I had to update the pointer in the Proxy
```xml
Change the RouteRule at the bottom: <TargetEndpoint>default</TargetEndpoint> → <TargetEndpoint>target-endpoint-default</TargetEndpoint>
```
## Lesson Learned
Always check that the `name="..."` attribute in the top XML tag matches the physical filename exactly before zipping.
