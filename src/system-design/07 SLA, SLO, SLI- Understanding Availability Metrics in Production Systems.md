## SLA, SLO, SLI: Understanding Availability Metrics in Production Systems

*Making Sense of Metrics That Keep Systems Reliable*

---

### 🧠 Pop Quiz:

You’re using a ride-hailing app. The app crashes right when you’re booking a cab to the airport. You scream in frustration — but behind the scenes, engineers scramble to investigate what went wrong with the **availability targets**.

Now imagine you're the engineer responsible. You need a way to **measure**, **track**, and **guarantee** that your systems are available when users need them.

That’s where **SLAs**, **SLOs**, and **SLIs** come in.

If you’ve heard these buzzwords tossed around in production meetings or SRE playbooks but never fully understood them — don’t worry. This article will clear the fog using simple analogies, real-world examples, and actionable insights.

---

## 🧩 What Are SLA, SLO, and SLI?

At their core, these are **agreements and metrics** used to define and measure **how reliable** a system is.

Let’s define them briefly before diving deep:

| Term | Stands for | What it does |
| --- | --- | --- |
| SLI | Service Level Indicator | A measurement of performance (e.g. 99.95% uptime) |
| SLO | Service Level Objective | An internal goal (e.g. 99.9% availability) |
| SLA | Service Level Agreement | A contractual promise (e.g. 99.5% uptime with penalties) |

---

## 🍔 Analogy: Ordering at a Restaurant

Let’s say you're dining out.

- **SLI** is how **long it actually took** to get your food.
- **SLO** is the **target** the restaurant set — e.g., food within 15 minutes.
- **SLA** is the **legal agreement** — if it takes longer than 30 minutes, you get a free dessert.

> It’s all about expectations, goals, and what happens if you don’t meet them.
> 

---

## 🔍 Let's Dive Deeper

---

### 1. 📏 **SLI – Service Level Indicator**

An **SLI** is a **quantifiable measure** of some aspect of your service’s performance.

Common SLIs include:

- **Availability**: % of requests successfully served
- **Latency**: % of requests under 300ms
- **Error rate**: % of failed API calls
- **Durability**: % of data not lost or corrupted

### 📘 Example:

“Out of 1 million login requests this month, 999,700 succeeded.”

→ **Availability SLI = 99.97%**

### ✅ Why It Matters:

SLIs help you **track how the system is actually behaving**. They’re the raw data behind your reliability targets.

---

### 2. 🎯 **SLO – Service Level Objective**

An **SLO** is an **internal target or goal** based on your SLIs.

It helps teams stay focused and plan system reliability.

### 📘 Example:

“We want the login endpoint to be available **99.9% of the time** over a 30-day window.”

That means you’re allowed:

- 43.2 minutes of downtime/month
- 8.64 hours of downtime/year

SLOs are **aspirational but realistic**. They act like speed limits — not absolute, but there for guidance and safety.

### ✅ Why It Matters:

- Helps define **acceptable error budgets**
- Keeps engineers from over-engineering
- Aligns reliability with business goals

---

### 3. 📜 **SLA – Service Level Agreement**

An **SLA** is a **formal, legal agreement** between you and your customers (external or internal). It defines:

- Expected performance
- Measurement window
- Penalties if the SLA is breached

### 📘 Example:

Your cloud provider offers **99.95% uptime SLA**.

If they go below that, you might get **service credits** or discounts.

> While SLOs are internal promises, SLAs are external contracts.
> 

### 🧠 Tip:

SLAs are usually **lower than SLOs** to account for unpredictability.

| Metric | Who Uses It | Binding? | Purpose |
| --- | --- | --- | --- |
| SLI | Engineers | No | Observe & measure |
| SLO | Engineers/Product | No | Set goals & guide priorities |
| SLA | Business/Legal | Yes | Set customer expectations |

---

## 🧮 Visual Diagram: Relationship Between SLA, SLO, SLI

```
[ SLI ] ← Measures
   ↑
[ SLO ] ← Targets based on SLI
   ↑
[ SLA ] ← Legally enforces a lower version of SLO

```

---

## 💥 Real-World Examples

### ☁️ 1. Cloud Provider (e.g., AWS S3)

- **SLI**: 99.999999999% durability of objects
- **SLO**: 99.99% availability
- **SLA**: 99.9% availability with credits for breaches

### 📱 2. Mobile App Backend (e.g., Swiggy API)

- **SLI**: 99.96% of order placements succeed within 2 seconds
- **SLO**: Internal target of 99.9%
- **SLA**: External commitment of 99.5%

---

## 🛠️ Error Budget: Your Reality Check

SLOs are directly tied to the idea of an **error budget**.

If your SLO is 99.9%, you can afford:

- 0.1% errors
- ~43 minutes of downtime per month

Once you exceed that, **all new deployments may be paused** to focus on fixing reliability issues.

> It’s a balance between speed and stability.
> 

---

## 🤔 Why All This Matters in System Design

In modern software systems, especially **distributed systems**, **failure is inevitable**.

SLA/SLO/SLI frameworks help you:

- Quantify and manage risk
- Avoid overpromising reliability
- Plan for realistic goals
- Align engineering with business

---

## 💡 Trivia: Did You Know?

- Google SREs famously use **SLOs and error budgets** to decide **whether to deploy** new code.
- If an SLO breach occurs, it can override product timelines.
- Some companies even link **engineer bonuses** to SLA compliance.

---

## 🧠 Final Thoughts: Metrics With Meaning

SLIs, SLOs, and SLAs aren't just jargon — they’re the **language of reliability**.

They let engineers, product managers, and customers agree on:

- What’s acceptable
- What’s aspirational
- What’s non-negotiable

> In the world of production systems, you can’t improve what you don’t measure.
> 

And now, you know **what to measure** — and why it matters.

---

### ✅ Takeaway Challenge

- Try defining an **SLI**, **SLO**, and **SLA** for your own project.
- Example: If you have a blog, what's your **availability goal**?
    - SLI: % of uptime per week
    - SLO: 99.9%
    - SLA (for readers or clients): 99.5%

It’s a great exercise to start thinking like a Site Reliability Engineer.