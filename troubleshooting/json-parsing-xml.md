# 🐛 Bug Report: "Unexpected token < in JSON"

**Date:** Dec 6, 2025 | **Context:** Project 3 (Mashup Logic)

## The Error
My JavaScript policy crashed with a 500 error:
> `SyntaxError: Unexpected token: <`

## The Investigation
The error happened at this line of code:
`var data = JSON.parse(context.getVariable("response.content"));`

I checked the backend URL. It was pointing to `mocktarget.apigee.net/xml`.

## The Root Cause 🔍
I was trying to parse **XML** as **JSON**.
* **XML starts with:** `<root>...`
* **JSON starts with:** `{ "root": ...`

The JavaScript engine saw the first character `<` and panicked because that is illegal in JSON. Hence: "Unexpected token <".

## The Fix
I had two options:
1.  **Convert it:** Use an `XMLToJSON` policy *before* the JavaScript step.
2.  **Change Source:** Update the Target URL to point to a JSON endpoint (`/json`).

I chose **Option 2** because it was faster for this lab.

## Lesson Learned
Always verify the `Content-Type` of your backend response before feeding it into `JSON.parse()`.
