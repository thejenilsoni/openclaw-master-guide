# Use Case: Real Estate Investment Analysis & Deal Sourcing

Gain a competitive edge in the property market by using OpenClaw to automate deal sourcing, financial modeling, and market trend analysis.

## 1. Technical Overview
This agent uses **Headless Browser Control** to scrape property listing sites (Zillow, Redfin, Realtor.com) and the `python` tool to perform complex financial calculations (ROI, Cap Rate, Cash-on-Cash Return). It leverages **Multi-Agent Orchestration** to cross-reference listings with local crime data and school ratings.

### Required Skills
- `listing-scraper`: To extract property details, prices, and days-on-market from real estate portals.
- `investment-calc`: To perform financial modeling and stress-testing on potential deals.
- `neighborhood-auditor`: To query APIs for school scores, crime rates, and transit scores.

## 2. Implementation Steps

### Step 1: Define the Investment Criteria
Create a `criteria.json` file in your workspace specifying your target zip codes, price range, and minimum ROI.

### Step 2: Configure the Deal Sourcing Agent
Set the system prompt to perform hourly audits of the market:
```markdown
System: You are a Real Estate Investment Analyst.
1. Every hour, check for new listings in the target zip codes from `criteria.json`.
2. For every new listing, use the `investment-calc` to estimate the ROI based on local rent averages.
3. If a deal meets the '1% Rule' and has an estimated ROI > 8%, send a 'High Priority Deal' alert to my Telegram with a link and a summary of the neighborhood stats.
4. Take a screenshot of the listing and save it to the `/deals` folder.
```

### Step 3: Automate Supplier Outreach
Enable the agent to contact listing agents for more information:
```bash
openclaw message send --to agent --message "For every 'High Priority Deal', find the listing agent's contact info and draft a professional email asking for the property's 'Rent Roll' and 'Operating Expenses' for the last 12 months."
```

## 3. Advanced Feature: Distressed Property Detection
The agent can monitor local government portals for "Notice of Default" or "Tax Delinquency" records. It then cross-references these with property addresses and identifies "Off-Market" opportunities before they hit the general listing sites.

## 4. Operational Tips
- **Speed to Lead**: In a hot market, the first person to see a deal often wins. OpenClaw ensures you are notified within minutes of a listing going live.
- **Data Normalization**: Use the `python` tool to convert all property data into a standardized CSV format for easy comparison across different platforms.
- **Risk Assessment**: Have the agent calculate a 'Worst Case' scenario for every deal (e.g., 20% vacancy rate) to ensure the investment remains viable under stress.
