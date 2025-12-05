# 📡 Service Callouts: The "Side Quest" Policy

**Date:** Dec 6, 2025 | **Mood:** 🤹 Multitasking

## The Problem
In a standard Proxy, you have **One Target**. You send a request, get a response, and go home.
But what if I need data from **two** different places?
* *Example:* I need Product Data (Server A) AND Inventory Data (Server B).

I can't define two Target Endpoints. I need a way to make a "Side Request" in the middle of the flow.

## The Solution: Service Callout
The **Service Callout** policy lets the proxy act like a client. It pauses the main flow, calls another API, gets the answer, saves it to a variable, and then resumes the main flow.

## The Analogy: The Pizza Order 🍕
1.  **The Main Flow:** You call the Pizza Shop to order a Pepperoni Pizza.
2.  **The Problem:** The shop is out of pepperoni.
3.  **The Service Callout:** *While keeping you on the phone*, the Chef calls the Butcher Shop on a separate line.
    * "Do you have pepperoni?" (Request)
    * "Yes, sending it over." (Response)
4.  **The Resume:** The Chef comes back to your line: "Okay, your pizza is coming."

You (the Client) never knew the Chef made a second call. You just got your pizza.

## Critical Config: `continueOnError`
I learned that you should usually set `continueOnError="true"`.
* **True:** If the Butcher doesn't answer, the Chef still makes you a Cheese Pizza (Partial Success).
* **False:** If the Butcher hangs up, the Chef hangs up on YOU (500 Error).

## TL;DR
* **Target Endpoint:** The Destination (Main Logic).
* **Service Callout:** A Detour (Side Logic/Enrichment).
