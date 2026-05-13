# Use Case: Intelligent Smart Home & IoT Concierge

Integrate OpenClaw with your local IoT ecosystem (e.g., Home Assistant) to create a natural language interface for your physical environment.

## 1. Technical Overview
This use case leverages OpenClaw's **Webhooks** and **API Fetching** capabilities. By acting as a gateway, OpenClaw can translate human intent into structured API calls for local IoT hubs.

### Required Skills
- `api-fetch`: To communicate with Home Assistant or Zigbee2MQTT.
- `voice-wake`: (Optional) For hands-free interaction on macOS/iOS.
- `image-processing`: To analyze security camera feeds.

## 2. Implementation Steps

### Step 1: Connect to Home Assistant
Obtain a **Long-Lived Access Token** from your Home Assistant profile. Add it to your OpenClaw environment variables:
```bash
export HASS_TOKEN="your_token_here"
export HASS_URL="http://homeassistant.local:8123"
```

### Step 2: Define the IoT Skill
Create a custom skill in `~/.openclaw/skills/iot_home/SKILL.md`:
```markdown
# Smart Home Skill
I can control the following devices:
- `light.living_room`: Dimmable LED.
- `switch.coffee_maker`: Smart plug.
- `lock.front_door`: Smart lock.

When the user asks to "Turn on the lights," send a POST request to `${HASS_URL}/api/services/light/turn_on` with the entity_id.
```

### Step 3: Natural Language Workflows
You can now send complex, context-aware requests:
- **Intent**: "I'm leaving for work."
- **Execution**: OpenClaw locks the front door, turns off all lights, and sets the thermostat to "Eco" mode.
- **Intent**: "Is there anyone at the door?"
- **Execution**: OpenClaw pulls the latest frame from the doorbell camera, uses a vision model to identify if a person is present, and describes the scene to you on Telegram.

## 3. Advanced Automation: Energy Optimization
Combine the `market-research` skill with `iot-integration`:
1. OpenClaw monitors real-time electricity prices via a utility API.
2. During "Peak" hours, it automatically dims non-essential lights and delays the dishwasher cycle.
3. It sends you a summary of the money saved at the end of the month.

## 4. Security Recommendations
- **Local Network**: Keep your IoT agent on a separate VLAN if possible.
- **Encryption**: Always use HTTPS for internal API calls to prevent credential sniffing.
- **Pairing Only**: Never set your IoT channel to `dmPolicy="open"`.
