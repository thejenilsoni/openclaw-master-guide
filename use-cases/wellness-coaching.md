# Use Case: Autonomous Personalized Wellness & Health Coaching

Improve your health outcomes by using OpenClaw to integrate with wearable data, analyze nutrition, and provide proactive, personalized coaching.

## 1. Technical Overview
This agent acts as a **Personal Wellness Concierge**, integrating with health APIs (Apple Health, Oura, Garmin) and nutrition databases (FatSecret, Nutritionix). It uses the `python` tool for biometric data analysis and the `canvas` tool to present progress charts and meal plans.

### Required Skills
- `health-api-connector`: To securely retrieve data from wearables and health apps.
- `nutrition-analyzer`: To estimate caloric and nutrient density from food descriptions or photos.
- `fitness-planner`: To generate adaptive workout routines based on recovery metrics.

## 2. Implementation Steps

### Step 1: Set Up the Wellness Workspace
Create a secure, private workspace with access to your health and nutrition tools:
```bash
openclaw workspace create wellness-vault --tools "health-api-connector,nutrition-analyzer,python"
```

### Step 2: Configure the Health Coach
Set the system prompt to provide proactive, data-driven coaching:
```markdown
System: You are a Personalized Health Coach. 
1. Every morning at 7 AM:
   a. Query my Oura and Apple Health data for last night's 'Readiness' and 'Sleep' scores.
   b. If my 'Recovery' score is < 60, suggest a 'Light Active Recovery' workout (e.g., Yoga, Walking).
   c. If my 'Recovery' score is > 80, suggest a 'High Intensity' session.
2. When I upload a photo of my meal:
   a. Estimate the macronutrients (Protein, Carbs, Fats) and calories.
   b. Compare this against my daily goal in `nutrition_plan.json`.
   c. Provide a 'Meal Tip' (e.g., "Add more fiber to stay full longer").
3. Send a 'Daily Health Summary' to my private Signal account.
```

### Step 3: Automate Progress Tracking
Enable the agent to manage your long-term goals:
```bash
openclaw message send --to wellness-vault --message "Every Sunday evening, analyze my biometric data for the past week, generate a line chart of my 'Resting Heart Rate' and 'Activity Level', and suggest 2 small habit changes for next week."
```

## 3. Advanced Feature: Bio-Syncing
The agent can monitor your 'Readiness' score and automatically adjust your calendar. If your recovery is extremely low, it can suggest rescheduling high-stress meetings or blocking off an extra hour for an afternoon nap, ensuring your professional life supports your physical well-being.

## 4. Privacy & Safety Guardrails
- **Data Encryption**: All biometric and health data MUST be stored in an encrypted local workspace (AES-256).
- **Medical Disclaimer**: The agent must always include a standard medical disclaimer: "I am an AI assistant, not a doctor. Consult a medical professional before making significant health changes."
- **Consent-First**: The agent should only access health APIs after explicit, time-limited user consent is provided via the `openclaw` auth flow.
