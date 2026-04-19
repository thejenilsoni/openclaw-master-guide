# Use Case: AI-Powered Event Management & Guest Coordination

Maximize event attendance and streamline logistics by using OpenClaw to automate guest communication, RSVP tracking, and vendor coordination.

## 1. Technical Overview
This agent acts as a **Centralized Command Center** for events, integrating with messaging platforms (WhatsApp/SMS) and event platforms (Eventbrite, Luma). It uses **Omnichannel Messaging** to ensure high response rates and **Calendar Integration** to manage the event schedule.

### Required Skills
- `rsvp-tracker`: To monitor and update guest lists in real-time from messaging platforms.
- `omnichannel-messaging`: To reach guests on their preferred channel (WhatsApp, Signal, SMS).
- `vendor-manager`: To track and communicate with event vendors (catering, AV, venue).

## 2. Implementation Steps

### Step 1: Set Up the Event Workspace
Create a workspace with access to the necessary communication and scheduling tools:
```bash
openclaw workspace create event-ops --tools "rsvp-tracker,omnichannel-messaging,calendar-scheduler"
```

### Step 2: Define the Guest Coordination Logic
Set the system prompt to handle guest inquiries and confirmations:
```markdown
System: You are an Event Coordinator for [Event Name]. 
1. When a message is received from a guest:
   a. Check their name against the 'Guest List' CSV.
   b. If they are confirming attendance, update the 'RSVP' status and ask for dietary restrictions.
   c. If they ask for event details (time, location, parking), provide the standard 'Event Brief'.
2. 24 hours before the event, send a 'Final Confirmation' message to all 'Confirmed' guests with the QR code for entry.
3. Update the 'Guest Dashboard' on the OpenClaw Canvas.
```

### Step 3: Automate Vendor Communication
Enable the agent to manage vendor logistics:
```bash
openclaw message send --to event-ops --message "Every Monday at 9 AM, send an email to the 'Catering' vendor with the updated 'Guest Count' and 'Dietary Restrictions' from the workspace."
```

## 3. Advanced Feature: Real-Time Event Support
During the event, the agent can act as a "Virtual Concierge" for guests. If a guest sends a message like "Where is the main stage?" or "What time is the next speaker?", the agent provides the information instantly, reducing the need for physical support staff.

## 4. Operational Tips
- **Personalized Outreach**: Use the guest's first name and reference their previous interactions to make the messages feel more personal.
- **Urgent Escalation**: Configure a keyword (e.g., "EMERGENCY") that immediately pings the event organizer's phone and provides the guest's location and contact details.
- **Post-Event Surveys**: Automatically send a 'Thank You' message and a link to a feedback survey to all 'Attended' guests 2 hours after the event ends.
