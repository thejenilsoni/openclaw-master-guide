# Use Case: HIPAA-Compliant Healthcare Administration & Scheduling

Improve patient experience and reduce administrative burden by using OpenClaw to manage appointments, patient inquiries, and billing workflows in a secure environment.

## 1. Technical Overview
This agent acts as a secure interface between patients (via encrypted channels like Signal) and the clinic's **Electronic Health Record (EHR)** system. It prioritizes **Data Privacy** and follows strict HIPAA-compliant data handling protocols.

### Required Skills
- `ehr-connector`: To securely read/write to systems like Epic or Athenahealth (via FHIR APIs).
- `secure-messaging`: Integration with Signal or encrypted web portals.
- `audit-logger`: To maintain a detailed, tamper-proof log of all data access for compliance.

## 2. Implementation Steps

### Step 1: Deploy in a Compliant Environment
OpenClaw MUST be deployed on a **HIPAA-compliant cloud instance** (e.g., AWS with a Business Associate Agreement) or a local server within the clinic's secure network.

### Step 2: Configure the Patient Concierge
Set the system prompt to handle administrative tasks without exposing PII (Personally Identifiable Information):
```markdown
System: You are a Medical Administrative Assistant. 
1. When a patient asks to book an appointment:
   a. Verify their identity using the 'Secure Verification' skill (DOB + Last 4 of SSN).
   b. Query the EHR for available slots in the 'General Practice' department.
   c. Present 3 options and confirm the booking.
2. If a patient asks a medical question, provide a standard 'Disclaimer' and offer to route the message to their primary care physician.
```

### Step 3: Automate Billing Inquiries
Enable the agent to assist with insurance and billing:
```bash
openclaw message send --to agent --message "If a patient asks about their balance, check the billing database and provide the total amount due and a link to the secure payment portal."
```

## 3. Advanced Feature: Post-Visit Follow-Up
The agent can automatically send a secure message to patients 24 hours after their visit: "Hi [Name], how are you feeling today? Remember to take your prescribed medication. If you experience [Symptom X], please call our emergency line immediately."

## 4. Security & Compliance Requirements
- **Encryption at Rest**: All patient data stored in the OpenClaw workspace must be encrypted using AES-256.
- **Access Control**: Use Multi-Factor Authentication (MFA) for any staff member accessing the OpenClaw management console.
- **De-identification**: For any data used in 'Insight Reports' (e.g., average wait times), the agent must automatically remove all PII.
