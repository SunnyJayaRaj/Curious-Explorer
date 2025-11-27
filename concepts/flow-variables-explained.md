# 🧠 Flow Variables: The Sticky Notes of Apigee

**Date:** Nov 27, 2025 | **Mood:** 🕵️‍♂️ Detective

## The Concept
When a request enters Apigee, it’s not just a static piece of data. Apigee creates a "Session" for that request. Inside this session, you can store data, read data, and pass data between policies. These storage spots are called **Flow Variables**.

If you don't understand Variables, you can't write logic.

## The Analogy: The Medical Clipboard 📋
Imagine a patient (The Request) entering a Hospital (Apigee).
1.  **The Intake Nurse:** Checks the ID and writes "Blood Pressure: 120/80" on a **Clipboard**.
2.  **The Doctor:** Reads the clipboard. She doesn't ask the patient again; she just reads the variable `patient.blood_pressure`.
3.  **The Surgeon:** Adds a new note: `surgery.status = "success"`.
4.  **The Billing Dept:** Reads the status and prints the bill.

The **Clipboard** is the Flow. The **Notes** are the Variables.

## Common Variables I Learned
* `request.header.Authorization`: The token the user sent.
* `request.queryparam.city`: What the user asked for (e.g., `?city=London`).
* `response.status.code`: Did the backend say 200 OK or 500 Error?
* `client.ip`: The IP address of the user.

## How to use them?
You use them in **Conditions** to make decisions:

```xml
<Step>
    <Name>Spike-Arrest-Policy</Name>
    <Condition>(client.ip = "192.168.1.5")</Condition>
</Step>
```

## TL;DR
Flow Variables are `Sticky Notes` attached to the request as it moves through the proxy. They let policies talk to each other without modifying the actual message.
