# Use Case: AI-Driven Hospitality Revenue Management & Dynamic Pricing

Maximize RevPAR (Revenue Per Available Room) and ADR (Average Daily Rate) by using OpenClaw to automate competitor rate shopping, demand forecasting, and dynamic pricing adjustments.

## 1. Technical Overview
This agent acts as a **Hospitality Revenue Manager**, integrating with PMS (Property Management Systems), OTA (Online Travel Agency) platforms (Expedia, Booking.com), and rate-shopping APIs (OTA Insight, STR). It uses the `python` tool for demand forecasting and the `browser` tool for competitor rate audits.

### Required Skills
- `rate-shopper`: To securely retrieve real-time competitor rates and inventory levels from OTAs.
- `demand-forecaster`: To predict occupancy and demand based on historical data, events, and market trends.
- `pms-connector`: To update rates and inventory in the property's PMS and channel manager.

## 2. Implementation Steps

### Step 1: Set Up the Revenue Management Workspace
Create a secure, private workspace with access to the property and market data:
```bash
openclaw workspace create revenue-hub --tools "rate-shopper,demand-forecaster,pms-connector"
```

### Step 2: Configure the Dynamic Pricing Agent
Set the system prompt to monitor market conditions and suggest rate adjustments:
```markdown
System: You are a Hospitality Revenue Manager. 
1. Monitor the 'Competitor Rates' for the 5 'Compset Hotels' listed in `market_compset.json`.
2. Every 2 hours, use the `rate-shopper` to update the 'Market Average Rate' for the next 30 days.
3. If the 'Market Average Rate' for any 'High-Demand Date' (e.g., local concert, holiday) increases by > 10%:
   a. Use the `demand-forecaster` to calculate the 'Optimal ADR' for the property.
   b. Suggest a 'Rate Increase' of $15-25 for the 'Deluxe Room' category.
   c. Send a 'Rate Optimization Alert' to the #revenue-ops channel on Slack with the compset data and recommended ADR.
4. Generate a 'Monthly RevPAR Forecast' dashboard on the OpenClaw Canvas.
```

### Step 3: Automate Last-Minute Inventory Triage
Enable the agent to manage unsold inventory:
```bash
openclaw message send --to revenue-hub --message "Analyze the 'Occupancy Forecast' for the upcoming weekend. If 'Deluxe Rooms' are < 60% occupied, identify the 3 'High-Converting' OTAs and suggest a 'Flash Sale' discount of 15% for the remaining inventory."
```

## 3. Advanced Feature: AI-Powered Personalization & Upselling
The agent can analyze guest booking history and preferences (via the PMS). When a high-value guest books a room, the agent can automatically suggest a 'Personalized Upsell' (e.g., a suite upgrade or a spa package) via a direct WhatsApp or email message, increasing the Total Revenue Per Available Room (TrevPAR).

## 4. Operational & Financial Guardrails
- **Data Privacy**: Guest and financial data MUST be handled according to PCI-DSS and relevant data protection laws (e.g., GDPR).
- **Brand Integrity**: The agent must never lower rates below the 'Brand Floor Price' to protect long-term ADR and brand positioning.
- **Human-in-the-Loop**: Any decision to adjust rates in the PMS or launch 'Flash Sales' must be confirmed by a human Revenue Manager via the `canvas` interface.
- **Fair Play**: Ensure all rate-shopping and pricing activities comply with OTA parity agreements and local competition laws.
