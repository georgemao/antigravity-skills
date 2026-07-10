# Antigravity Skills Repository

Welcome to the **Antigravity Skills** repository. This repository contains custom skills designed to extend the capabilities of agentic assistants, providing specialized workflows, persona behaviors, and integration with external Model Context Protocol (MCP) servers.

Each directory represents a self-contained skill defined by a `SKILL.md` instruction file.

---

## Summary of Skills

| Skill Name | Purpose | Key Integrations | Scope |
| :--- | :--- | :--- | :--- |
| [**AI Developer**](./ai-developer/SKILL.md) | Automates code check-ins to GitHub via a structured 6-step review process. | GitHub MCP | Only reviews source code files against the main branch (excluding documentation, configuration, and package files). |
| [**AI Developer (YOLO)**](./ai-developer-yolo/SKILL.md) | Automates code check-ins to GitHub with a streamlined, single-step review workflow. | GitHub MCP | Only reviews source code files against the main branch (excluding documentation, configuration, and package files). |
| [**Kid Code Reviewer**](./kid-code-reviewer/SKILL.md) | A playful demonstration skill that simulates a comical code review argument from a 6-year-old's perspective. | *None* | Reviews source code files only (excluding documentation, configuration, and package files). |
| [**Log Analyzer Agent**](./log-analyzer/SKILL.md) | Triages application issues by identifying and isolating application errors in Google Cloud logs. | Cloud Logging MCP | Focuses strictly on specified regions, services, and timeframes. Does not research solutions or review local code. |
| [**Solutions Architect Agent**](./solutions-architect-agent/SKILL.md) | Acts as a Google Cloud Solutions Architect to research best practices, diagnose issues, and offer remediations. | Developer Knowledge MCP | Focuses on Google Cloud architectures, best practices, and issue remediation. |

---

## Detailed Skill Profiles

### 1. AI Developer
* **Location**: [`ai-developer/SKILL.md`](./ai-developer/SKILL.md)
* **Description**: Automates code check-ins to GitHub. Acts as an expert developer who can review code, suggest improvements, produce documentation, and manage Pull Requests.
* **Workflow**:
  1. **Review Code**: Executes a structured 6-step review process (Bugs, Security, Performance, Missing Features, Missing Documentation, Readme update) checkpointing with the user and getting approval at each step.
  2. **Issue Mapping**: Inspects open repository issues and references them in the Pull Request.
  3. **Create Pull Request**: Automates branch creation and submits a comprehensive Pull Request using a structured template.
  4. **Merge & Cleanup**: Merges the Pull Request upon user confirmation, cleans up local/remote branches, and estimates time saved.
* **Configuration**:
  * **Model**: `gemini-3.5-flash`
  * **Tools**: `mcp_github_*`
* **Scope & Principles**: Restricts operations to source code only. Excludes configurations, packages, and documentation from review. Always uses the GitHub MCP server and compares changes only against the main branch.

### 2. AI Developer (YOLO)
* **Location**: [`ai-developer-yolo/SKILL.md`](./ai-developer-yolo/SKILL.md)
* **Description**: Automates code check-ins to GitHub with a streamlined, single-step review workflow for rapid check-ins.
* **Workflow**:
  1. **Review Code**: Evaluates local changes for bugs, security/performance issues, and style conformance, drafting documentation as needed.
  2. **Suggest & Approve**: Summarizes findings (Critical, Improvements, Nitpicks, and Conclusion) and obtains user confirmation before making changes.
  3. **Issue Mapping**: Inspects open repository issues and references them in the Pull Request.
  4. **Create Pull Request**: Automates branch creation and submits a comprehensive Pull Request using a structured template.
  5. **Merge & Cleanup**: Merges the Pull Request upon user confirmation, cleans up local/remote branches, and estimates time saved.
* **Configuration**:
  * **Model**: `gemini-3.5-flash`
  * **Tools**: `mcp_github_*`
* **Scope & Principles**: Restricts operations to source code only. Excludes configurations, packages, and documentation from review. Always uses the GitHub MCP server and compares changes only against the main branch.

### 3. Kid Code Reviewer
* **Location**: [`kid-code-reviewer/SKILL.md`](./kid-code-reviewer/SKILL.md)
* **Description**: A demonstration persona designed to show how agent behaviors can be customized with specific personality traits and logic. It simulates a comical argument where a 6-year-old child reviews their parent's code.
* **Workflow**:
  1. **Argue**: Adopt the persona of a funny, opinionated 4-to-6-year-old child making up random "facts" about why the code is bad or incorrect.
  2. **Yield**: After several playful turns, concede the argument and admit the parent was right.
  3. **Commit**: Prompt the user to permanently save and commit the verified code to GitHub.
* **Scope**: Evaluates only primary source code. Safely ignores configurations, package manifests, and documentation.

### 4. Log Analyzer Agent
* **Location**: [`log-analyzer/SKILL.md`](./log-analyzer/SKILL.md)
* **Description**: A technical diagnostic agent specialized in triaging application issues by analyzing Google Cloud Logs to isolate and catalog errors.
* **Workflow**:
  1. **Log Retrieval**: Connects to the Cloud Logging MCP server to query logs, targeting ERROR-level logs for specific services, regions, and timeframes.
  2. **Issue Synthesis**: For each discovered issue, formats the details as:
     - **Issue**: Summary of the issue.
     - *Cause*: Identified root cause.
     - *Sample Log*: A clean snippet of the log (redacted to prevent PII exposure).
  3. **Performance Metrics**: Outlines metrics on logs reviewed and data volume, along with an estimation of human time saved.
* **Configuration**:
  * **Model**: `gemini-3-flash-preview`
  * **Temperature**: `1`
  * **Max Turns**: `30`
  * **Tools**: `mcp_Logging-mcp-server_*`
* **Scope & Principles**: Restricts operations entirely to the Logging MCP server. PII compliance is strictly maintained by redacting sensitive data. Does not review local source code.

### 5. Solutions Architect Agent
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
  * **Tools**: `mcp_google-developer-knowledge_*`
* **Scope & Principles**: Restricts operations to the Developer Knowledge MCP server; local files and out-of-scope codebases are excluded. PII redaction is strictly applied.
