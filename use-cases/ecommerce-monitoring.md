# Use Case: E-commerce Price War & Inventory Intelligence

Stay competitive in the fast-paced e-commerce market by automating competitor price tracking, stock monitoring, and dynamic pricing alerts.

## 1. Technical Overview
This agent uses **Headless Browser Control** to navigate competitor product pages and **DOM Parsing** to extract real-time price and availability data. It uses **Multi-Agent Orchestration** to compare your prices against the market and suggest adjustments.

### Required Skills
- `browser-control`: To scrape dynamic, JavaScript-heavy e-commerce sites.
- `price-tracker`: A specialized skill for parsing currency and discount data.
- `alert-system`: To send instant notifications via Telegram/Slack when thresholds are met.

## 2. Implementation Steps

### Step 1: Target Identification
Create a list of competitor product URLs in a `targets.json` file within your workspace.

### Step 2: Configure the Monitoring Agent
Set the system prompt to perform regular audits:
```markdown
System: You are an E-commerce Strategist.
1. Every 4 hours, visit the URLs in `targets.json`.
2. Extract the current price and check if the item is 'In Stock'.
3. If a competitor's price drops below our 'Minimum Margin' (stored in `config.yaml`), send a 'Price War Alert' to the #sales channel.
4. If a competitor is 'Out of Stock', suggest increasing our ad spend for that specific product.
```

### Step 3: Dynamic Alerting
Enable the agent to provide actionable insights:
```bash
openclaw message send --to agent --message "If [Competitor X] drops their price on the 'Lobster Pro' model below $199, automatically draft a promotional email in Mailchimp with a 'Price Match' guarantee."
```

## 3. Advanced Feature: Sentiment-Based Stocking
The agent can monitor social media and review sites for "out of stock" complaints regarding competitor products. It then cross-references this with your own inventory and suggests targeted ad campaigns to capture the frustrated demand.

## 4. Technical Considerations
- **IP Rotation**: Use the `proxy-manager` skill to avoid being rate-limited or blocked by large e-commerce platforms.
- **Visual Verification**: Have the agent take a screenshot of the competitor's price as "proof" to include in the alert message.
- **Data Integrity**: Use the `python` tool to clean and normalize currency data (e.g., converting everything to USD) before comparison.
