# 🌐 SiteAgent: The Action Protocol for the Agentic Web

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-2.0.0--beta-green.svg)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)]()

> **"Don't let AI guess your UI. Give it a map."**

SiteAgent is an intent-driven execution protocol and Web SDK designed for B2B SaaS, complex web applications, and high-frequency workflows.

In the emerging Agent Economy, traditional Graphical User Interfaces (GUIs) have become a massive barrier for machine execution. Relying on Vision-Language Models (VLMs) to visually "guess" and navigate complex web pages is brittle, expensive, and insecure—especially when dealing with cross-domain configurations (e.g., Apple Developer to Supabase) or sensitive authentication.

**SiteAgent's mission is to lay down a machine-readable infrastructure layer for every website on the internet.**

---

## ✨ Why SiteAgent?

By integrating the lightweight SiteAgent SDK and dropping an `agents.json` protocol file into your root directory, your platform instantly unlocks the following capabilities:

* 🤖 **A2A (Agent-to-Agent) Native Integration**: Allow external AI agents (like OpenAI Operator or open-source models) to interact directly with your app's workflow via a standard API, bypassing fragile DOM rendering entirely.
* 🚀 **F-Mode (Force / Headless Execution)**: Users state their intent, and the system extracts parameters via a local, encrypted form. SiteAgent then executes the sequence headless in milliseconds, ensuring sensitive data (like API keys) never hits external LLM networks.
* 🧭 **D-Mode (Guide / Immersive Handoff)**: For scenarios requiring human oversight, the system gracefully falls back to a visual guide. It uses dynamic spotlights and anti-error intercepts to walk users through complex UI mazes step-by-step.
* 🛡️ **ADDE (Authority Downgrade Decision Engine)**: When encountering high-risk actions (e.g., asset transfers, downloading secure keys), the system forces a downgrade from F-Mode to a human-in-the-loop confirmation, ensuring absolute safety.
* 🧬 **Drift Detection & Self-Healing ($S_{offset}$)**: Say goodbye to broken scripts after UI updates. By calculating semantic drift and utilizing a lightweight fallback VLM, SiteAgent automatically re-anchors targets and silently patches the protocol when your DOM structure changes.

---

## 🏗️ Core Architecture: One Protocol, Dual-Track Execution

The heart of SiteAgent is the `agents.json` file. It doesn't just tell machines how to click (F-Mode); it also instructs the UI on how to guide humans (D-Mode).

**Example: Requesting an Auth Key in Apple Developer Console**

```json
{
  "step_id": "input_key_name",
  "description": "Input the desired key name",
  "locator": {
    "selector": "input#key-name-input",
    "nearby_text": "Enter a name for your key." // Crucial for Drift Detection and Self-Healing
  },
  "f_mode": {
    "action": "input",
    "value": "{{parameters.key_name}}" // Headless parameter injection
  },
  "d_mode": {
    "action": "spotlight_input",
    "guide_text": "Please enter your desired key name here, e.g., 'Supabase Auth'." // UI rendering for human guidance
  }
}
```
## 🚀 Quick Start
Bringing SiteAgent to your SaaS platform takes just two steps:

1. Install the SDK
Install via npm or include it directly in your HTML:
<script type="module" src="[https://cdn.jsdelivr.net/npm/@siteagent/widget](https://cdn.jsdelivr.net/npm/@siteagent/widget)"></script>

2. Initialize the Advisor Gateway
import { SiteAgent } from '@siteagent/widget';

const agent = new SiteAgent({
  protocolPath: '/agents.json', // Path to your machine-readable protocol
  theme: 'dark',
  onHandoff: (context) => {
    // Handle cross-domain task continuation (e.g., carrying Apple Key ID to Supabase)
    console.log("Cross-domain handoff initiated:", context);
  }
});

agent.mount('#agent-root');

## 🗺️ Roadmap
[x] v1.0: Client-side action mapping script and basic cross-domain context.

[x] v2.0 (Current): B2B protocol standardization (F/D dual-track, A2A interface).

[ ] v2.1: Release Context Anchor relay service for seamless cross-domain handoffs.

[ ] v2.5: Open-source the Drift Detection engine and auto-recording generator (via rrweb).

[ ] v3.0: Build a global agents.json registry for major SaaS platforms.

## 🤝 Contributing
We believe the future of the internet belongs to an intent-driven Agent Economy. If you are a SaaS developer, a solopreneur, or simply passionate about the next generation of human-computer interaction, we'd love your help!

Fork the repository

Submit an Issue or PR

Help us map and adapt agents.json for the world's most vital websites

License: MIT
