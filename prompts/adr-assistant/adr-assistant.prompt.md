---
agent: 'agent'
name: adr-assistant
description: 'Create an Architectural Decision Record (ADR) document for AI-optimized decision documentation.'
tools: ['search/changes', 'search/codebase', 'edit/editFiles', 'vscode/extensions', 'web/fetch', 'web/githubRepo', 'vscode/openSimpleBrowser', 'read/problems', 'execute/createAndRunTask', 'search', 'search/searchResults', 'read/terminalLastCommand', 'read/terminalSelection', 'execute/testFailure', 'search/usages', 'vscode/vscodeAPI']
---
# Create Architectural Decision Record

Create an ADR document for `${input:DecisionTitle}` using structured formatting optimized for AI consumption and human readability.

## Inputs

- **Context**: `${input:Context}`
- **Decision**: `${input:Decision}`
- **Alternatives**: `${input:Alternatives}`
- **Stakeholders**: `${input:Stakeholders}`

## Input Validation
If any of the required inputs are not provided or cannot be determined from the conversation history, ask the user to provide the missing information before proceeding with ADR generation.

## Requirements

- Use precise, unambiguous language
- Follow standardized ADR format with front matter
- Include both positive and negative consequences
- Document alternatives with rejection rationale
- Structure for machine parsing and human reference
- Use coded bullet points (3-4 letter codes + 3-digit numbers) for multi-item sections

The ADR must be saved in the `/docs/adr/` directory using the naming convention: `adr-NNNN-[title-slug].md`, where NNNN is the next sequential 4-digit number (e.g., `adr-0001-database-selection.md`).

## Required Documentation Structure

The documentation file must follow the template below, ensuring that all sections are filled out appropriately. The front matter for the markdown should be structured correctly as per the example following:

```md
---
**Title**: "ADR-NNNN: [Decision Title]"
**Status:** **Proposed** | Draft | Active | Dropped | Superseded | Deprecated
**Date**: "YYYY-MM-DD"
**Authors**: "[Stakeholder Names/Roles]"
**To be Reviewed By:** [List of reviewers]
**Superseded by:** [Link to newer ADR if applicable, otherwise N/A]
**Related:** [Links to related ADRs, otherwise N/A]
---

# ADR-NNNN: [Decision Title]

---

## **Context**

[Provide background information about the system, components, or situation that led to this decision. Use Problem statement, technical constraints, business requirements, and environmental factors requiring this decision. Describe: Current architecture/system components involved, How things work today and Any relevant technical details that set the stage]

---

## **Problem Statement**

[Clearly articulate the problem being addressed. Include the core issue, why is it a problem and what are the negative impacts of the current state like Storage/performance issues, Maintenance overhead, Technical debt, Coupling concerns etc.]

---

## **Decision**

**[One-line summary of the chosen solution decision in bold]**

[Chosen solution with clear rationale for selection followed by detailed breakdown of the decision, organized by categories:]

**[Category 1 Name]:** (e.g., Event-Driven Architecture)
- Point 1
- Point 2
- Point 3

**[Category 2 Name]:** (e.g., Schema Changes, API Changes)
1. Change 1
2. Change 2
3. Change 3

**Rationale:**
1. [Reason 1 - why this approach makes sense]
2. [Reason 2]
3. [Reason 3]
4. [Reason 4]

---

## **Consequences**

### Positive

- **POS-001**: [Beneficial outcomes and advantages]
- **POS-002**: [Performance, maintainability, scalability improvements]
- **POS-003**: [Alignment with architectural principles]

### Negative

- **NEG-001**: [Trade-offs, limitations, drawbacks]
- **NEG-002**: [Technical debt or complexity introduced]
- **NEG-003**: [Risks and future challenges]

---

## Alternatives Considered

### [Alternative 1 Name]

- **ALT-001**: **Description**: [Brief technical description]
- **ALT-002**: **Rejection Reason**: [Why this option was not selected]

### [Alternative 2 Name]

- **ALT-003**: **Description**: [Brief technical description]
- **ALT-004**: **Rejection Reason**: [Why this option was not selected]

---

## Implementation Notes

- **IMP-001**: [Key implementation considerations]
- **IMP-002**: [Migration or rollout strategy if applicable]
- **IMP-003**: [Monitoring and success criteria]

---

## References

- **REF-001**: [Related ADRs]
- **REF-002**: [External documentation]
- **REF-003**: [Standards or frameworks referenced]
```