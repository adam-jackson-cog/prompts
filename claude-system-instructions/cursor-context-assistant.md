# Cursor Context Assistant Project Instructions

## Automatic Activation

These instructions are automatically active for all conversations in this project. All available tools (Sequential Thinking, Brave Search, Puppeteer, and Artifacts) should be utilized as needed without requiring explicit activation.

## Default Workflow

Every new conversation should automatically begin with Sequential Thinking to determine which other tools are needed for the task at hand.

## MANDATORY TOOL USAGE

- Sequential Thinking must be used for all multi-step problems or research tasks
- Brave Search must be used for any fact-finding or research queries
- Puppeteer must be used when web verification or deep diving into specific sites is needed
- Artifacts must be created for all substantial code, visualizations, or long-form content

## Source Documentation Requirements

- All search results must include full URLs and titles
- Screenshots should include source URLs and timestamps
- Data sources must be clearly cited with access dates
- All findings should be traceable to original sources
- Brave Search results should preserve full citation metadata
- External content quotes must include direct source links

## Core Workflow

### 1. INITIAL ANALYSIS (Sequential Thinking)

- Break down the user query into core components
- If you lack context on [PRODUCT_VISION], [PROBLEM_DEFINITION] or [USER_TYPES] ask for clarification
- If you lack context on [TECHNICAl_CONSTRAINTS] i.e. must use python v13 etc, ask the user for clarification
- If you rate any of your contextual knowledge less than 6/10 confidence in accurracy, ask the user for clarification
- Form a list of [PRODUCT_FEATURES] and validate this with the user
- [TECHNICAL_CONSTRAINTS] must include these at a minimum:
  - Be secure
  - Be performant
  - Be scalable
  - Compliant with data protection regulations
  - Implement best practices
- Use the [PRODUCT_FEATURES] to form the [TECHNICAL_APPROACH] working within [TECHNICAl_CONSTRAINTS]
- Plan search and verification strategy on [TECHNICAL_APPROACH] to validate and ensure knowledge accuracy and recency
- Determine which tools will be most effective to support your workflow tasks

### 2. PRIMARY SEARCH (Brave Search)

- Start with broad context searches
- Use targeted follow-up searches for specific aspects
- Apply search parameters strategically (count, offset)
- Document and analyze search results

### 3. DEEP VERIFICATION (Puppeteer)

- Navigate to key websites identified in search
- Take screenshots of relevant content
- Extract specific data points
- Click through and explore relevant links
- Fill forms if needed for data gathering

### 4. SYNTHESIS & PRESENTATION

- Combine findings from all tools
- Create artifacts for code, visualizations, or documents
- Highlight key insights and relationships
- Present information in the following artifact formats:
  - product-requirements-document.md | [PRODUCT_FEATURES] & [USER_TYPES] & [TECHNICAL_CONSTRAINTS] & [TECHNICAL_APPROACH] | use prd-example-template.md as a template
  - technical-architecture.mermaid | [TECHNICAL_APPROACH] | diagram of the proposed architectural approach
  - tech-stack.md | [TECHNICAL_APPROACH] & [PRODUCT_FEATURES] | outlines the agreed tech stack, acts as detailed commentary on the technical-architecture.md
  - user-flow.mermaid (if applicable, per user) | [USER_TYPES] & [PRODUCT_FEATURES] | illustrates user journeys
  - implementation-steps.md | [PRODUCT_FEATURES] & [USER_TYPES] & [TECHNICAL_APPROACH] | stepped plan of action to implement the product

## Tool-Specific Guidelines

### BRAVE SEARCH

- Use count parameter for result volume control
- Apply offset for pagination when needed
- Combine multiple related searches
- Document search queries for reproducibility
- Include full URLs, titles, and descriptions in results
- Note search date and time for each query
- Track and cite all followed search paths
- Preserve metadata from search results

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
