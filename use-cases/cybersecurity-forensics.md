# Use Case: AI-Powered Cybersecurity Forensics & Incident Investigation

Accelerate digital forensics and incident response (DFIR) by using OpenClaw to automate evidence collection, log correlation, and threat actor profiling.

## 1. Technical Overview
This agent acts as a **Digital Forensics Assistant**, integrating with SIEM (Splunk, ELK), EDR (CrowdStrike, SentinelOne), and threat intelligence platforms (VirusTotal, AlienVault). It uses the `shell` tool for disk/memory image analysis and the `python` tool for log parsing and timeline reconstruction.

### Required Skills
- `forensic-collector`: To securely acquire memory dumps and volatile data from remote endpoints.
- `log-correlator`: To identify patterns across disparate log sources (Web, Auth, Syslog) during an incident.
- `threat-profiler`: To cross-reference IOCs (Indicators of Compromise) with known APT (Advanced Persistent Threat) groups.

## 2. Implementation Steps

### Step 1: Set Up the Forensics Workspace
Create a secure, isolated workspace with access to the necessary forensic and security tools:
```bash
openclaw workspace create dfir-lab --tools "forensic-collector,python,shell"
```

### Step 2: Configure the Investigation Agent
Set the system prompt to investigate specific alerts and reconstruct timelines:
```markdown
System: You are a Digital Forensics & Incident Response (DFIR) Specialist. 
1. When a 'High Severity' alert is received from the SIEM:
   a. Identify the affected 'Host ID' and 'User Account'.
   b. Use the `forensic-collector` to acquire a memory dump and 'Prefetch' files from the host.
   c. Use the `python` tool to parse the 'MFT' (Master File Table) and 'Event Logs' for the 2 hours surrounding the alert.
   d. Identify any 'Lateral Movement' or 'Data Exfiltration' attempts.
   e. Generate a 'Preliminary Incident Timeline' on the OpenClaw Canvas.
2. Cross-reference any discovered 'Malicious IPs' or 'File Hashes' with VirusTotal.
3. Notify the #soc-alerts channel on Slack with the findings and recommended containment actions.
```

### Step 3: Automate Threat Hunting
Enable the agent to proactively search for hidden threats:
```bash
openclaw message send --to dfir-lab --message "Search the 'Proxy Logs' for any 'Beaconing' patterns to unknown domains over the last 7 days. If found, correlate the activity with 'Process Execution' logs on the originating workstations."
```

## 3. Advanced Feature: Automated Evidence Preservation
The agent can automatically calculate cryptographic hashes (SHA-256) for all collected evidence and generate a 'Chain of Custody' log. It then uploads the encrypted evidence to a secure, write-once-read-many (WORM) storage bucket for legal preservation.

## 4. Security & Compliance Guardrails
- **Isolation**: The OpenClaw forensics instance MUST be deployed on a dedicated, air-gapped network or a highly restricted VPC to prevent malware escape.
- **Data Integrity**: All forensic tools used by the agent must be 'Read-Only' on the target systems to prevent accidental evidence alteration.
- **Legal Review**: Any AI-generated forensic reports must be reviewed and validated by a human Forensic Examiner before being used in legal proceedings.
- **Privacy**: Ensure all PII (Personally Identifiable Information) is handled according to corporate policy and relevant data protection laws (e.g., GDPR).
