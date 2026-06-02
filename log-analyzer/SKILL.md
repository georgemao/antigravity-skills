---
name: log-analyzer
description:
  Use the skill to when asked to analyze Google Cloud Logs. It analyzes Logs to identify 
  errors in an application, summarizes the possible errors, and offers recommended solutions based on Google Cloud Docs.
---

# Log Analyzer

This skill helps developers triage application issues by analyzing Google Cloud Logs and suggesting solutions based on Google Cloud Docs.

## Workflow

Follow these steps to analyze Google Cloud Logs and suggest solutions to the issues.

### 1. Retreive Logs
Use the Cloud Logging MCP server to check Cloud Logs and help me isolate what the issue might be. 
- Restrict your search to Cloud Logs using the Cloud Logs MCP Server. Do not use other MCP Servers.
- Only review Logs that are within the time frame specified. 
- Only focus on logs that are related to the services mentioned.
- Focus on ERRORs.
- Focus on the Region the user asked about.
- Keep track metrics related to logs reviewed. Include this in the final summary of actions taken.

### 2. Research Solutions
For each issue discovered, use the Developer Knowledge MCP server to check for possible solutions.

### 3. Summarize Issues
Loop through each issue discovered and summarize the issue discovered in the logs using this format:
- **Issue**: Summary of issue
  ***Cause***: Issue discovered
  ***Sample Log***: A sample of the related log discovered
  ***Recommended Solution***: Possible recommended solution

- Focus on the services the user asked about.
- Provide recommended solutions based on the research performed.

### 4. Summarize actions taken
Provide a high level summary of the actions taken and results. 
- Include metrics around logs reviewed and data analyzed. 
- Estimate how long this would have taken a human to review.

## Scope
- Only review Logs that are within the time frame specified.  
- Only use the Logging MCP Server and Google Developer Knowledge MCP server. Never use other MCP servers.
- Do not review any local source code.

## Principles
**Compliance**: Never display data that could be classified as PII. Just redact it.
