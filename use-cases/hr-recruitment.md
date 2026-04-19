# Use Case: AI-First HR Recruitment & Resume Screening

Transform your hiring process by using OpenClaw to automate candidate sourcing, resume evaluation, and interview scheduling with high-precision matching.

## 1. Technical Overview
This agent uses the `pdf-reader` to parse resumes and the `python` tool to perform skill-gap analysis. It integrates with **LinkedIn** (via browser) or **ATS APIs** (Applicant Tracking Systems) to source and manage candidates.

### Required Skills
- `resume-parser`: To extract structured data (skills, experience, education) from PDF/Docx.
- `ats-connector`: To sync candidate status with tools like Greenhouse, Lever, or a custom database.
- `calendar-scheduler`: To find mutual availability and book interviews.

## 2. Implementation Steps

### Step 1: Define the Recruitment Workspace
Create a workspace with access to the necessary parsing and scheduling tools:
```bash
openclaw workspace create hiring-hub --tools "pdf-reader,python,calendar-scheduler"
```

### Step 2: Configure the Screening Logic
Set the system prompt to evaluate candidates against a specific job description:
```markdown
System: You are a Technical Recruiter. 
1. When a resume is uploaded to the `/inbox` folder:
   a. Extract the candidate's core skills and years of experience.
   b. Compare them against the 'Senior Backend Engineer' requirements in `job_desc.md`.
   c. Assign a 'Match Score' (0-100) and highlight any missing 'Must-Have' skills.
2. If the score is > 80, use the `calendar-scheduler` to send the candidate an invite for a 15-minute screening call.
3. Update the 'Candidate Pipeline' CSV in the workspace.
```

### Step 3: Automate Sourcing
Enable the agent to find passive candidates:
```bash
openclaw message send --to hiring-hub --message "Search LinkedIn for 'Rust Developers' in 'Berlin' with at least 5 years of experience. Summarize the top 5 profiles and draft a personalized outreach message for each."
```

## 3. Advanced Feature: Interview Preparation
The agent can analyze a candidate's GitHub profile or portfolio and generate 5-10 tailored technical questions for the interviewer, focusing on the specific technologies used in the candidate's projects.

## 4. Ethical & Compliance Guardrails
- **Bias Mitigation**: Configure the agent to redact names, gender, and photos during the initial screening phase to ensure a focus on skills.
- **Data Retention**: Set an automatic deletion policy for resumes after the hiring process is complete to comply with GDPR/CCPA.
- **Human Oversight**: The agent should only "Suggest" candidates for interviews; the final "Invite" must be approved by a human recruiter via the `canvas` interface.
