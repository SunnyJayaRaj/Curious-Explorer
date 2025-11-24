# 🛡️ What is an API Proxy?

**Date:** Nov 24, 2025  
**Mood:** 💡 Clarified

## The Concept
Before today, I thought an API was just a URL you hit to get data. But in the enterprise world, you never let users talk directly to your backend server. That’s dangerous.

Instead, you put a **Proxy** in the middle.

## The Analogy: The Waiter 🍽️
I like to think of an API Proxy like a **Waiter** in a restaurant.
1. **The Customer (Client App)** sits at the table and orders food.
2. **The Waiter (Proxy)** takes the order to the kitchen.
3. **The Kitchen (Backend Database)** cooks the raw food.
4. **The Waiter** checks the food, maybe adds some garnish (formatting), and brings it to the customer.

If the customer tries to walk into the kitchen (talk to the backend directly), they get kicked out. The Waiter protects the Kitchen.

## Why use Apigee?
Apigee is just a very smart Waiter. It can:
- **Check IDs:** (Security / API Keys)
- **Limit Orders:** "Sorry, only 5 orders per minute." (Traffic Spikes)
- **Translate:** Convert the Kitchen's messy XML into clean JSON.

## My First Code Snippet
In Apigee, we define this relationship using XML. Here is a basic `ProxyEndpoint` definition I learned:


```xml
<ProxyEndpoint name="default">
    <HTTPProxyConnection>
        <BasePath>/v1/weather</BasePath> 
    </HTTPProxyConnection>
    <RouteRule name="default">
        <TargetEndpoint>default</TargetEndpoint>
    </RouteRule>
</ProxyEndpoint>
```
**TL;DR**

A Proxy is a facade. It decouples the `Consumer` from the `Service`, allowing me to change the backend without breaking the frontend app.
