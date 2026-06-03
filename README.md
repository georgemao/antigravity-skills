# Antigravity Skills Repository

Welcome to the **Antigravity Skills** repository. This repository contains custom skills designed to extend the capabilities of agentic assistants, providing specialized workflows, persona behaviors, and integration with external Model Context Protocol (MCP) servers.

Each directory represents a self-contained skill defined by a `SKILL.md` instruction file.

---

## Summary of Skills

| Skill Name | Purpose | Key Integrations | Scope |
| :--- | :--- | :--- | :--- |
| [**Kid Code Reviewer**](./kid-code-reviewer/SKILL.md) | A playful demonstration skill that simulates a comical code review argument from a 6-year-old's perspective. | *None* | Reviews source code files only (excluding documentation, configuration, and package files). |
| [**Log Analyzer**](./log-analyzer/SKILL.md) | Triages application issues by analyzing Google Cloud logs, matching them to solutions, and summarizing findings with metadata metrics. | Cloud Logging MCP, Developer Knowledge MCP | Restricts focus to specified regions, services, and timeframes; no local code review. |
| [**Solutions Architect Agent**](./solutions-architect-agent/SKILL.md) | Acts as a Google Cloud Solutions Architect to research best practices, diagnose issues, and offer remediations. | Developer Knowledge MCP | Focuses on Google Cloud architectures, best practices, and issue remediation. |

---

## Detailed Skill Profiles

### 1. Kid Code Reviewer
* **Location**: [`kid-code-reviewer/SKILL.md`](./kid-code-reviewer/SKILL.md)
* **Description**: A demonstration persona designed to show how agent behaviors can be customized with specific personality traits and logic. It simulates a comical argument where a 6-year-old child review's their parent's code.
* **Workflow**:
  1. **Argue**: Adopt the persona of a funny, opinionated 4-to-6-year-old child making up random "facts" about why the code is bad or incorrect.
  2. **Yield**: After several playful turns, concede the argument and admit the parent was right.
  3. **Commit**: Prompt the user to permanently save and commit the verified code to GitHub.
* **Scope**: Evaluates only primary source code. Safely ignores configurations, package manifests, and documentation.

### 2. Log Analyzer
* **Location**: [`log-analyzer/SKILL.md`](./log-analyzer/SKILL.md)
* **Description**: A technical diagnostic skill to automate the triage of application issues directly from Google Cloud Logs and map them to vetted resolutions.
* **Workflow**:
  1. **Log Retrieval**: Queries Google Cloud Logs via the Cloud Logging MCP server, targeting ERROR-level entries in specified regions and services within a precise timeframe.
  2. **Solution Research**: Cross-references isolated errors against official guidelines using the Developer Knowledge MCP server.
  3. **Structured Summary**: Formats each issue cleanly:
     - **Issue**: High-level summary of the issue.
     - *Cause*: Identified root cause.
     - *Sample Log*: Precise log snippet (with PII redacted).
     - *Recommended Solution*: Vetted resolution path.
  4. **Activity Metrics**: Quantifies logs reviewed, data analyzed, and estimates time savings compared to human operator manual triage.
* **Scope & Principles**: PII compliance is strictly maintained by redacting sensitive data. Does not touch local source code.

### 3. Solutions Architect Agent
* **Location**: [`solutions-architect-agent/SKILL.md`](./solutions-architect-agent/SKILL.md)
* **Description**: Emulates a senior Google Cloud Solutions Architect specialized in analyzing cloud architecture, researching best practices, and recommending implementation plans.
* **Workflow**:
  1. **Research & Synthesis**: Utilizes the Developer Knowledge MCP server to perform targeted research on architecture issues or design patterns.
  2. **Issue Mapping**: Formats researched solutions using the standard architectural report structure:
     - **Issue**: Summary of the challenge.
     - *Cause*: Core underlying technical reason.
     - *Sample Log*: Relevant diagnostic snippet (redacted).
     - *Recommended Solution*: Actionable, best-practice remediation.
  3. **Reporting**: Summarizes architectural actions taken, diagnostic metrics, and estimated manual labor saved.
* **Configuration**:
  * **Model**: `gemini-3-flash-preview`
  * **Temperature**: `1`
  * **Max Turns**: `30`
* **Scope & Principles**: Restricts operations to the Developer Knowledge MCP server; local files and out-of-scope codebases are excluded. PII redaction is strictly applied.
