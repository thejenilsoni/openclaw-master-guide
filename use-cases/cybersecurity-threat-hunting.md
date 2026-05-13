# Use Case: AI-Driven Cybersecurity Threat Hunting & Incident Response

Empower your SOC (Security Operations Center) by using OpenClaw to automate log analysis, threat intelligence gathering, and initial incident triage.

## 1. Technical Overview
This agent connects to security tools (SIEM, EDR) via APIs and uses the `shell` tool to run local scanning utilities. It leverages **Pattern Recognition** to identify anomalies in logs and cross-references them with real-time threat feeds.

### Required Skills
- `log-analyzer`: To parse and summarize large volumes of system or network logs.
- `threat-intel`: To query APIs like VirusTotal, AlienVault, or Shodan.
- `nmap-skill`: To perform targeted network scans for vulnerability assessment.

## 2. Implementation Steps

### Step 1: Secure the Security Agent
Given the sensitivity, the agent MUST run in a highly restricted environment:
- Use a dedicated **sandboxed container** for the OpenClaw instance.
- Enable **audit logging** for every command the agent executes.

### Step 2: Configure the Threat Hunter
Set the system prompt to monitor for specific indicators of compromise (IoCs):
```markdown
System: You are a Cybersecurity Analyst. 
1. Monitor the `/var/log/auth.log` file for repeated failed SSH login attempts.
2. If more than 5 attempts from a single IP occur within 1 minute:
   a. Extract the IP address.
   b. Query VirusTotal for the IP's reputation score.
   c. If the score is > 10, use the `shell` to add the IP to the local `iptables` blocklist.
3. Send a detailed 'Incident Triage Report' to the #security-alerts channel on Slack.
```

### Step 3: Automated Vulnerability Scanning
Schedule a weekly internal scan:
```bash
openclaw message send --to agent --message "Every Sunday at 2 AM, run an Nmap scan on the internal 192.168.1.0/24 subnet. Report any new open ports or services that weren't present last week."
```

## 3. Advanced Feature: Automated Phishing Analysis
The agent can monitor a 'phishing-report' inbox. It automatically extracts URLs/attachments, detonates them in a secure sandbox (via a specialized skill), and provides a 'Malicious/Safe' verdict to the reporting user within seconds.

## 4. Operational Guardrails
- **Read-Only Access**: Grant the agent read-only access to logs and SIEM APIs to prevent accidental data deletion.
- **Manual Block Confirmation**: For critical infrastructure, require a human "Approve" before the agent modifies firewall rules.
- **Credential Safety**: Use environment variables for API keys; never let the agent "see" the raw keys in its prompt.
