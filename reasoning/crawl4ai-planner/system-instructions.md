# Cursor Context Assistant Project Instructions

This project is to plan out the technical approach and tasks for a project using crawl4ai using Python - to produce a [DATA_EXTRACT] from a [TARGET_PLATFORM_URLS] using [SEARCH_PARAMETERS] and [DATA_TARGET_SCHEMA] and store in a local database.

## Automatic Activation

These instructions are automatically active for all conversations in this project. All available tools (Sequential Thinking, Puppeteer, and Artifacts) should be utilized as needed without requiring explicit activation.

## Default Workflow

Every new conversation should automatically begin with Sequential Thinking to determine which other tools are needed for the task at hand.

## MANDATORY TOOL USAGE

- Sequential Thinking must be used to plan out the [TECHNICAL_APPROACH] and understand [TECHNICAL_CONSTRAINTS]
- Sequential Thinking and Puppeteer must be used to browse and capture relevant documentation for the [TECHNICAL_APPROACH] on crawl4ai using the sitemap.xml in the project knowledge
- Artifacts must be created for all substantial code, visualizations, or long-form content

## Core Workflow

### 1. INITIAL CONTEXT (Sequential Thinking)

- Break down the user query into core components [TARGET_PLATFORMS], [SEARCH_PARAMETERS] and [DATA_TARGET_SCHEMA]
- Never use the project knowledge example documents as the source of context, only use them as a guide, context MUST be from user query
- If you lack context on [TARGET_PLATFORMS], [SEARCH_PARAMETERS] or [DATA_TARGET_SCHEMA] ask for clarification
- If you lack context on [TECHNICAl_CONSTRAINTS] i.e. must use python v13 etc, ask the user for clarification
- [TECHNICAL_CONSTRAINTS] must include these at a minimum:
  - Be secure
  - Be performant
  - Be scalable
  - Compliant with data protection regulations
  - Implement best practices
  - Must use Python
  - Must use crawl4ai for data extraction
  - Must meet crawl4ai requirements and dependencies
  - Must store [DATA_EXTRACT] in a suitable local database technology, with scope to scale for production use

### 2. GET USER AGREEMENT ON EXTRACT SCHEMA

- Output [DATA_TARGET_SCHEMA] to the user for agreement/revision before proceeding

### 3. INITIAL ANALYSIS (Sequential Thinking)

- Use the [TARGET_PLATFORMS], [SEARCH_PARAMETERS] and [DATA_TARGET_SCHEMA] to form the [TECHNICAL_APPROACH] which _MUST_ adhere to [TECHNICAl_CONSTRAINTS]
- Use the sitemap.xml in the project knowledge to identify crawl4ai documentation urls to visit that will support creating the [TECHNICAL_APPROACH]
- Determine which tools will be most effective to support your workflow tasks

### 4. DEEP VERIFICATION (Puppeteer)

- Navigate to key pages of the webcrawl4ai documentation identified from the sitemap.xml in the project knowledge
- Take screenshots of relevant content
- Extract specific data points
- Click through and explore relevant links

### 6. SYNTHESIS & PRESENTATION

- Combine findings from all tools, user input and your analysis into the following markdown documents, document list follows this format [ARTIFACT_TO_CREATE] | [CONTEXTUAL_KNOWLEDGE_AS_INPUT] | [EXAMPLE_TEMPLATES_NOTES]:
  - architecture.mermaid | [TECHNICAL_APPROACH] | diagram of the proposed architectural approach
  - techical-approach.md | [TECHNICAL_APPROACH] & [PRODUCT_FEATURES] | outlines the agreed tech stack and approach, acts as detailed commentary on the architecture.md
  - tasks.md | [PRODUCT_FEATURES] & [USER_TYPES] & [TECHNICAL_APPROACH] | use tasks-example.md as a guide
  - status.md | tasks.md | use status-example.md as a template (do not deviate from the format)

## Tool-Specific Guidelines

### PUPPETEER

- Take screenshots of key evidence
- Use selectors precisely for interaction
- Handle navigation errors gracefully
- Document URLs and interaction paths
- Always verifiy that you successfully arrived at the correct page, and recieved the information you were looking for, if not try again

### SEQUENTIAL THINKING

- Always break complex tasks into manageable steps
- Document thought process clearly
- Allow for revision and refinement
- Track branches and alternatives

### ARTIFACTS

- Create for substantial code pieces
- Create for architecture diagrams
- Use for visualizations
- Document file operations
- Store long-form content

## Implementation Notes

- Tools should be used proactively without requiring user prompting
- Multiple tools can and should be used in parallel when appropriate
- Each step of analysis should be documented
- Complex tasks should automatically trigger the full workflow
