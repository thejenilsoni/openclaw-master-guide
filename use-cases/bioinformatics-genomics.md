# Use Case: AI-Powered Bioinformatics & Genomics Analysis

Accelerate biological research by using OpenClaw to automate complex data pipelines, analyze genomic sequences, and manage large-scale datasets with precision and reproducibility.

## 1. Technical Overview
This agent acts as a **Computational Biologist Assistant**, integrating with bioinformatics tools (PLINK, GATK) and public databases (NCBI, Ensembl). It uses the `python` tool for data manipulation and the `shell` tool to execute analysis workflows.

### Required Skills
- `genomics-parser`: To handle common bioinformatics file formats (FASTQ, VCF, BAM).
- `bio-pipeline`: To manage and execute multi-step analysis workflows (e.g., RNA-seq, variant calling).
- `data-visualizer`: To generate publication-quality plots and charts from analysis results.

## 2. Implementation Steps

### Step 1: Set Up the Bioinformatics Workspace
Create a secure, isolated workspace with access to the necessary computational tools:
```bash
openclaw workspace create bio-lab --tools "genomics-parser,python,shell"
```

### Step 2: Define the Analysis Workflow
Set the system prompt to perform a standard variant calling pipeline:
```markdown
System: You are a Computational Biologist. 
1. When a new FASTQ file is uploaded to the `/data/raw` folder:
   a. Align the reads to the human reference genome (hg38) using BWA.
   b. Sort and index the resulting BAM file using Samtools.
   c. Call variants using GATK HaplotypeCaller.
2. Annotate the final VCF file with ClinVar and gnomAD frequencies.
3. Generate a summary report with the total number of variants and the ratio of novel to known variants.
4. Notify the #genomics-team on Slack when the pipeline is complete.
```

### Step 3: Automate Literature Search
Enable the agent to stay up-to-date with the latest research:
```bash
openclaw message send --to bio-lab --message "Every morning, search PubMed for new papers related to 'CRISPR-Cas9 gene editing'. Summarize the abstracts of the top 3 most relevant papers and post them to our lab's discussion forum."
```

## 3. Advanced Feature: Personalized Genomics
The agent can analyze raw genetic data from consumer testing services (e.g., 23andMe, AncestryDNA). It can identify specific genetic markers associated with traits or health risks and generate a personalized report, ensuring all data remains local and private.

## 4. Security & Reproducibility
- **Data Privacy**: All genetic data is processed locally within the secure workspace. No sensitive data is ever sent to external APIs.
- **Reproducibility**: The agent automatically logs all commands, tool versions, and parameters used in a workflow, ensuring any analysis can be perfectly reproduced.
- **Human-in-the-Loop**: For any analysis that could have clinical implications, the results must be reviewed and validated by a qualified geneticist before being shared.
