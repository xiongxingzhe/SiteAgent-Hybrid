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
      "intent_name": "生成并下载鉴权密钥 (Auth Key)",
      "description": "为推送通知 (APNs) 或第三方集成 (如 Supabase) 创建新的密钥并下载 .p8 文件。",
      
      // 阶段 1：任务所需参数 (Advisor A 提取 / 隐私表单 Form 2)
      "parameters": {
        "key_name": {
          "type": "string",
          "description": "密钥的自定义名称",
          "required": true
        },
        "enable_apns": {
          "type": "boolean",
          "description": "是否开启 Apple Push Notification 服务",
          "default": true
        }
      },

      // 阶段 2：执行工作流 (F模式与D模式的统一编排)
      "workflow": [
        {
          "step_id": "nav_to_keys",
          "description": "导航到证书与密钥管理页面",
          // 结构感知引擎 (Drift Monitor)：多维立体定位
          "locator": {
            "url_pattern": "/account/resources/authkeys/list",
            "semantic_label": "Keys Menu Item",
            "fallback_xpath": "//a[contains(text(), 'Keys')]"
          },
          // F-Mode (代办)：直接无头跳转或点击
          "f_mode": {
            "action": "navigate",
            "target_url": "https://developer.apple.com/account/resources/authkeys/list"
          },
          // D-Mode (导办)：UI 渲染指令
          "d_mode": {
            "action": "highlight",
            "guide_text": "首先，请点击左侧导航栏的 'Keys' 进入密钥管理。",
            "require_user_click": true
          }
        },
        {
          "step_id": "input_key_name",
          "description": "输入密钥名称",
          "locator": {
            "selector": "input#key-name-input",
            "semantic_label": "Key Name Input Field",
            "nearby_text": "Enter a name for your key." // 用于 Soffset 漂移检测
          },
          "f_mode": {
            "action": "input",
            "value": "{{parameters.key_name}}" // 直接注入加密表单的变量
          },
          "d_mode": {
            "action": "spotlight_input",
            "guide_text": "请在这里输入你想好的密钥名称，例如 'Supabase Auth'。"
          }
        },
        {
          "step_id": "confirm_and_download",
          "description": "确认注册并下载密钥文件",
          "risk_level": "HIGH", // 触发 HITL (人类介入) 安全网关
          "locator": {
            "selector": "button.download-btn",
            "semantic_label": "Download Key Button"
          },
          "f_mode": {
            "action": "wait_for_human", // F模式在此强制降级暂停
            "prompt": "密钥已生成。这是高敏感资产，请您亲自点击下载并妥善保管。"
          },
          "d_mode": {
            "action": "highlight",
            "guide_text": "太棒了！最后一步，点击这里下载你的 .p8 密钥文件。"
          },
          // 交付物归档 (List 3)
          "outputs": {
            "key_id": {"selector": ".key-id-value", "type": "string"},
            "file_status": "downloaded"
          }
        },
        {
          "step_id": "handoff_to_supabase",
          "description": "携带密钥 ID 跨域前往 Supabase 进行配置",
          "type": "HANDOFF",
          "target_domain": "supabase.com",
          // 跨域任务令牌 (Context Anchor)
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
