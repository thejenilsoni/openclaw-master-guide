# Use Case: Autonomous Academic Research & Literature Synthesis

Accelerate your scientific workflow by using OpenClaw to find, read, and synthesize academic literature with high precision and proper citation management.

## 1. Technical Overview
This agent uses specialized **Academic APIs** (Semantic Scholar, OpenAlex) to retrieve peer-reviewed papers. It employs **Recursive Summarization** to handle large sets of documents and ensures citation accuracy using the `bibtex` tool.

### Required Skills
- `academic-search`: To query Semantic Scholar or PubMed for relevant papers.
- `pdf-summarizer`: To extract key findings, methodologies, and data from academic PDFs.
- `citation-manager`: To generate and manage BibTeX entries for your bibliography.

## 2. Implementation Steps

### Step 1: Set Up the Research Workspace
Create a workspace with access to academic search and PDF tools:
```bash
openclaw workspace create research-lab --tools "academic-search,pdf-summarizer"
```

### Step 2: Define the Literature Review Workflow
Configure the system prompt for systematic review:
```markdown
System: You are a Research Assistant. 
Your goal is to perform a literature review on "Impact of Local AI Agents on Privacy".
1. Search Semantic Scholar for the top 10 most cited papers from the last 3 years.
2. Download the PDFs and extract the 'Results' and 'Conclusion' sections.
3. Create a 'Synthesis Matrix' on the OpenClaw Canvas comparing the findings of each paper.
4. Highlight any 'Gaps in Literature' you identify.
```

### Step 3: Automate Citation Tracking
Ask the agent to manage your bibliography:
```bash
openclaw message send --to research-lab --message "For every paper included in the synthesis, generate a BibTeX entry and save it to `references.bib` in the workspace."
```

## 3. Advanced Feature: Grant Opportunity Monitoring
The agent can monitor portals like Grants.gov or specific university research offices. When a new grant matches your research keywords and eligibility criteria, it alerts you and drafts a preliminary "Letter of Intent" based on your previous project descriptions.

## 4. Best Practices for Researchers
- **Source Verification**: Always have the agent provide the DOI or direct URL for every claim it makes.
- **Hallucination Check**: Use the `fact-check` skill to cross-reference AI-generated summaries with the original PDF text.
- **Collaboration**: Share your OpenClaw workspace with your lab team to maintain a centralized, searchable repository of all research findings.
