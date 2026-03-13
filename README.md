# SiteAgent-Hybrid
An open-source protocol and engine defining agents.json for the Agentic Web. Enables secure, cross-domain AI-human collaboration through semantic-aware guidance and automation.

# 🚀 SiteAgent Hybrid: The Action Protocol for the Agentic Web

[MIT License] | [v1.0-alpha] | [PRs Welcome]

> **Stop building manuals. Start building pilots.** > SiteAgent Hybrid is an open-source framework and protocol (`agents.json`) that transforms isolated web silos into a seamless, machine-readable action network.

---

## 💡 Why SiteAgent?

In the era of AI Agents (like OpenAI Operator or Claude), the web is still a "Black Box":

* **The Silo Problem**: Complex tasks often span multiple platforms (e.g., Apple Dev -> Supabase), causing users and agents to lose context.
* **The Trust Wall**: Automated agents lack a standardized "handover" mechanism for sensitive legal or financial nodes.
* **UI Fragility**: Minor CSS changes break traditional automation scripts.

**SiteAgent Hybrid** fixes this by providing a semantic "Action Map" that both humans and AI can follow.

---

## ✨ Core Features

### 1. 🏝️ SiteAgent Capsule (The "Dynamic Island")
A minimalist, state-aware UI component that follows the user across domains.
* **Silent Mode**: Monitoring and protecting in the background.
* **Executing Mode**: Smoothly performing automated tasks.
* **Handover Mode**: Elegantly pausing to request human intervention for critical steps.

### 2. ⚡ Cross-Domain Orchestration (The "Handoff")
**The Killer Feature.** SiteAgent persists task context across different websites.
* **Example**: Moving from *Apple Developer* to *Supabase* to fetch a Secret Key. The Capsule stays active, guides the user through the third-party site, and provides a "One-Click Return" to the original task.

### 3. 🛡️ Authority Downgrade Decision Engine (ADDE)
A smart safety-first algorithm that calculates semantic drift:

$$Mode = \text{Agent} \to \text{Guide if } (S_{offset} \geq \text{Threshold} \lor \text{Task} = \text{Critical})$$

Ensures **100% compliance** and user control at high-risk nodes.

---

## 📄 The `agents.json` Protocol (v1.1)

Standardizing how AI interprets web actions. Now with **Orchestration** support:

```json
{
  "intent": "apple_auth_setup",
  "steps": [
    {
      "id": "init_apple",
      "action": "GUIDE",
      "description": "Start configuration on Apple."
    },
    {
      "id": "fetch_key",
      "type": "HANDOFF",
      "target_domain": "supabase.com",
      "context_anchor": {
        "source": "apple_connect",
        "needed": ["callback_url"]
      }
    }
  ]
}

```

## 📖 **Full Technical Specification:** [Read the agents.json v1.1 Draft here](./spec/PROTOCOL.md)
---

## 📅 Roadmap
[x] v0.1: Protocol Definition (agents.json v1.1).

[ ] v0.5: Open-source guide-runner.js with Semantic Self-Healing.

[ ] v0.8: SiteAgent Recorder - A browser extension to "Record once, generate roadmaps everywhere."

[ ] v1.0: Full Cross-Domain support for the "Golden Corridor" (Apple/Stripe/Supabase/AWS).        

---

## 🤝 Join the Movement

We are looking for the first **50 Seed Partners** to define the future of the Actionable Web.

* **Inquiries:** [ipanda666999@gmail.com]
* **Twitter:** [@pandyBuilds](https://x.com/pandyBuilds)
