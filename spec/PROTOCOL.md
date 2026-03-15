{
  "siteagent_schema": "2.0",
  "metadata": {
    "domain": "developer.apple.com",
    "service_name": "Apple Developer Console",
    "a2a_endpoint": "https://developer.apple.com/.well-known/agent-api"
  },
  "intents": [
    {
      "intent_id": "generate_auth_key",
      "intent_name": "Generate and Download Auth Key",
      "description": "Create a new key for APNs or third-party integration (e.g., Supabase) and download the .p8 file.",
      
      // Phase 1: Required Parameters (Extracted by Advisor A / Encrypted Form 2)
      "parameters": {
        "key_name": {
          "type": "string",
          "description": "Custom name for the key.",
          "required": true
        },
        "enable_apns": {
          "type": "boolean",
          "description": "Enable Apple Push Notification service.",
          "default": true
        }
      },

      // Phase 2: Execution Workflow (Unified F-Mode & D-Mode Orchestration)
      "workflow": [
        {
          "step_id": "nav_to_keys",
          "description": "Navigate to the Certificates, Identifiers & Profiles (Keys) page.",
          
          // Drift Monitor & Structure Perception: Multi-dimensional targeting
          "locator": {
            "url_pattern": "/account/resources/authkeys/list",
            "semantic_label": "Keys Menu Item",
            "fallback_xpath": "//a[contains(text(), 'Keys')]"
          },
          
          // F-Mode (Force/Headless): Direct navigation or background click
          "f_mode": {
            "action": "navigate",
            "target_url": "https://developer.apple.com/account/resources/authkeys/list"
          },
          
          // D-Mode (Guide): UI rendering instructions for human oversight
          "d_mode": {
            "action": "highlight",
            "guide_text": "First, click on 'Keys' in the left navigation sidebar.",
            "require_user_click": true
          }
        },
        {
          "step_id": "input_key_name",
          "description": "Input the desired key name.",
          "locator": {
            "selector": "input#key-name-input",
            "semantic_label": "Key Name Input Field",
            "nearby_text": "Enter a name for your key." // Crucial for Drift Detection ($S_offset)
          },
          "f_mode": {
            "action": "input",
            "value": "{{parameters.key_name}}" // Variable injection from the encrypted form
          },
          "d_mode": {
            "action": "spotlight_input",
            "guide_text": "Please enter your desired key name here, e.g., 'Supabase Auth'."
          }
        },
        {
          "step_id": "confirm_and_download",
          "description": "Confirm registration and download the key file.",
          "risk_level": "HIGH", // Triggers Human-in-the-Loop (HITL) Security Gateway
          "locator": {
            "selector": "button.download-btn",
            "semantic_label": "Download Key Button"
          },
          "f_mode": {
            "action": "wait_for_human", // F-Mode forcefully pauses here for human authorization
            "prompt": "Key generated. This is a highly sensitive asset. Please manually click download and store it securely."
          },
          "d_mode": {
            "action": "highlight",
            "guide_text": "Great! Finally, click here to download your .p8 key file."
          },
          // Output Extraction (List 3 Archive)
          "outputs": {
            "key_id": {"selector": ".key-id-value", "type": "string"},
            "file_status": "downloaded"
          }
        },
        {
          "step_id": "handoff_to_supabase",
          "description": "Cross-domain handoff to Supabase with the generated Key ID.",
          "type": "HANDOFF",
          "target_domain": "supabase.com",
          
          // Cross-Domain Task Token (Context Anchor)
          "context_anchor": {
            "source_intent": "generate_auth_key",
            "payload": {
              "apple_key_id": "{{outputs.key_id}}",
              "team_id": "{{account.team_id}}"
            },
            "next_suggested_intent": "configure_apple_login"
          }
        }
      ]
    }
  ]
}
