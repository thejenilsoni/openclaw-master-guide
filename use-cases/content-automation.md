# Use Case: Multi-Platform Content Production & Distribution

Automate the lifecycle of content creation—from initial research and drafting to formatting and cross-platform scheduling.

## 1. Technical Overview
This agent uses **Vision Models** to analyze images/videos and **Browser Automation** to interact with social media dashboards. It utilizes the `canvas` tool to collaborate with the user on drafts before publication.

### Required Skills
- `vision-analysis`: To describe images or extract text from videos.
- `browser-control`: To post content to platforms without official APIs.
- `canvas-ui`: To present drafts for human-in-the-loop approval.

## 2. Implementation Steps

### Step 1: Research & Drafting
Configure the agent to gather trending topics:
```markdown
System: You are a Content Strategist.
1. Every Monday, browse [Subreddit X] and [Tech News Site Y] for trending topics in AI.
2. Summarize the top 3 trends and create a 'Content Idea' card on the OpenClaw Canvas.
3. Wait for my feedback on which topic to pursue.
```

### Step 2: Multi-Format Generation
Once a topic is chosen, the agent generates tailored versions:
- **X (Twitter)**: A 5-post thread with high-engagement hooks.
- **LinkedIn**: A professional, long-form post with industry insights.
- **YouTube Shorts**: A 60-second script based on the core article.

### Step 3: Automated Distribution
Using the `browser-control` tool, the agent can handle the "grunt work" of posting:
```bash
openclaw message send --to agent --message "The LinkedIn draft looks good. Use the browser to log in to my account and schedule this post for 10:00 AM tomorrow."
```

## 3. Advanced Feature: Video Triage
The agent can monitor your YouTube comments or X mentions. It uses sentiment analysis to filter out spam and presents only high-value questions for you to answer, drafting suggested responses in your voice.

## 4. Implementation Tips
- **Voice Consistency**: Provide the agent with 3-5 examples of your previous posts to help it mimic your writing style.
- **Approval Gates**: Always use the `openclaw approval` mechanism before the agent clicks "Post" on any public platform.
- **Media Handling**: Use the `media-pipeline` to automatically resize images for different platform requirements (e.g., 16:9 for YouTube, 1:1 for Instagram).
