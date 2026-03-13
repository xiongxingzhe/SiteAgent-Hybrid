# 📄 agents.json: Machine-Readable Action Protocol (Standard Draft v1.1)

## 1. Protocol Metadata
Defines the core identity and compatibility of the site. This acts as the "Passport" for external AI Agents to recognize and interact with the platform.

```json
{
  "protocol_info": {
    "name": "SiteAgent Action Protocol",
    "version": "1.1.0",
    "schema_version": "2026-03-13",
    "last_updated": "2026-03-13T10:00:00Z"
  },
  "site_identity": {
    "site_name": "Apple Developer Connect",
    "domain": "developer.apple.com",
    "security_tier": "High"
  }
}
```
## 2. Intent & Atomic ActionsMaps 
ambiguous UI elements to definitive semantic actions, enabling deterministic execution for LLMs.

risk_level: Determines execution mode. If $Risk\_Level \geq High$, the system forces "Guide Mode" (Human-in-the-loop).

visibility: Privacy instructions. In Blind mode, sensitive data is processed in-memory and wiped immediately after execution to ensure user privacy.

```json
"intents": [
  {
    "id": "enroll_developer_program",
    "description": "Enroll in the Apple Individual Developer Program",
    "workflow": [
      {
        "step_id": "select_entity",
        "action_type": "DOM_SELECT",
        "semantic_label": "entity_type_dropdown",
        "expected_values": ["Individual", "Company"],
        "automation_allowed": true
      },
      {
        "step_id": "identity_verification",
        "action_type": "HUMAN_SIGNATURE_REQUIRED",
        "visibility": "Visible",
        "risk_level": "High",
        "description": "Requires legal signature. Mode must switch to human-guided for liability."
      }
    ]
  }
]
```
## 3. Cross-Domain Orchestration (v1.1 Feature)
Handles "Handoff" tasks across different platforms—the key to bridging the web's silos and maintaining task continuity.

HANDOFF: Defines the logic for leaving the current domain and initiating a task on a third-party site.

context_anchor: Persistent task data that travels with the agent to the destination site to prevent context loss.

```json
"orchestration": {
  "external_dependencies": [
    {
      "step_id": "fetch_supabase_key",
      "type": "HANDOFF",
      "target_domain": "supabase.com",
      "trigger_action": "REDIRECT_OR_NEW_TAB",
      "context_anchor": {
        "source_task": "apple_auth_config",
        "required_fields": ["callback_url", "client_secret"]
      },
      "guide_hint": "Navigating to Supabase to retrieve keys. SiteAgent will continue guidance at the destination."
    }
  ]
}
```
## 4. A2A (Agent-to-Agent) Interface
A semantic "Fast-Lane" optimized for external LLM Agents (e.g., OpenAI Operator, Claude Computer Use).

semantic_bridge: Direct mapping for LLMs to bypass brittle CSS selectors and interact with high-level business logic.

fallback_logic: Defines the recovery path when an external agent encounters a UI mismatch or timeout.

```json
"a2a_interface": {
  "llm_support_vlm": true,
  "hint_tokens": {
    "submit_btn": "[data-testid='enroll-submit']",
    "input_field": "[name='legal-entity-id']"
  },
  "error_recovery": {
    "on_dom_change": "REQUEST_RESCAN_OR_DOWNGRADE",
    "on_timeout": "ACTIVATE_GUIDE_MODE"
  }
}
```
## 5. Extensibility & Site-Specific Logic
Allows platform owners to define custom business logic and regional compliance without breaking the global protocol standard.

```json
"extensions": {
  "custom_site_logic": {
    "biometric_required": false,
    "regional_compliance": "GDPR-V2",
    "partner_metadata": {
      "integrated_with": ["Stripe", "Supabase", "Auth0"]
    }
  }
}
```
## 6. Security & Authority Downgrade (ADDE)
This core algorithm ensures safety by monitoring Semantic Drift ($S_{offset}$) between the current UI and the protocol definition.

![Security & Authority Downgrade (ADDE) Formula](./path/to/formula_render.jpg)


© 2026 SiteAgent Hybrid Project. Distributed under the MIT License.

