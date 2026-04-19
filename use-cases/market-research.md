# Use Case: Autonomous Market Research & Competitor Intelligence

This guide details how to implement an autonomous agent that monitors competitors, analyzes pricing changes, and delivers daily executive summaries via messaging channels.

## 1. Technical Overview
The agent uses the built-in **Chromium Browser Tool** to navigate websites, bypass simple bot detection, and extract DOM elements. It leverages **Multi-Agent Routing** to separate the "Scraper" (which handles raw data) from the "Analyst" (which performs the synthesis).

### Required Skills
- `browser-control`: For web navigation and DOM interaction.
- `summarize`: For distilling long-form web content.
- `cron`: To schedule the daily research tasks.

## 2. Implementation Steps

### Step 1: Configure the Scraper Workspace
Create a new workspace for your research agent:
```bash
openclaw workspace create research-agent
```

### Step 2: Set the System Prompt
Configure the agent's behavior by editing the workspace's `SKILL.md` or system prompt:
```markdown
You are a Senior Market Research Analyst. 
Your goal is to monitor the following URLs: [Competitor A, Competitor B].
1. Use the browser to check for any new blog posts, product announcements, or pricing updates.
2. If a change is detected, take a screenshot and extract the relevant text.
3. Compare the new data with the previous version stored in your memory.
4. Deliver a concise report to the #market-intel channel on Slack.
```

### Step 3: Schedule the Task
Use the `cron` skill to automate the execution:
```bash
openclaw message send --to agent --message "Schedule a daily market research run at 08:00 AM every weekday."
```

## 3. Advanced Prompting
To improve accuracy, use a structured extraction prompt:
> "Navigate to [URL]. Identify the 'Pricing' section. Extract the monthly cost for the 'Pro' plan. If the value differs from $49.99, alert me immediately with the new value and a summary of any feature changes."

## 4. Troubleshooting
- **Bot Detection**: If blocked, configure the browser tool to use a residential proxy or a custom User-Agent string in the `config.yaml`.
- **Token Usage**: Use a model with a large context window (e.g., Claude 3.5 Sonnet) to handle large DOM trees.
