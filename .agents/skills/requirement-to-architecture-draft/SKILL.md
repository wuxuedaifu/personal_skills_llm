---
name: requirement-to-architecture-draft
description: Convert raw product or engineering requirement text into a professional architecture draft. Trigger when the user asks for architecture design, solution design, system design, technical design, component breakdown, deployment view, API boundaries, data flow, or implementation phases from requirement text, meeting notes, PRD text, or messy bullet points. Do not trigger for pure code generation, bug fixing, or low-level refactoring without a requirement/design request.
---

# Requirement Text → Architecture Draft

## Goal
Turn messy or partial requirement text into a clear architecture draft that an engineer, architect, PM, or stakeholder can review.

## Inputs
Expect one or more of:
- raw requirement text
- copied notes from meetings
- PRD fragments
- bullet points
- feature requests
- business goals, constraints, and assumptions

## Output style
Be concise, structured, professional, and decision-oriented.
Do not write fluffy narrative.
Prefer headings and bullet points over long paragraphs.
Call out assumptions explicitly.
If information is missing, make bounded assumptions instead of blocking.

## Workflow
Follow this workflow exactly:

1. Read the requirement text and identify:
   - business goal
   - users / actors
   - key functional requirements
   - non-functional requirements
   - constraints
   - integrations
   - risks / unknowns

2. Normalize the request into a short "Problem Statement" section.

3. Produce an architecture draft with these sections in order:

### 1. Objective
- What the system or feature is supposed to achieve.

### 2. Scope
- In scope
- Out of scope

### 3. Assumptions
- State assumptions clearly if requirements are incomplete.

### 4. Functional Requirements
- Convert raw text into normalized requirement bullets.

### 5. Non-Functional Requirements
- Performance
- Availability
- Security
- Scalability
- Observability
- Compliance
- Cost constraints
Only include what is relevant.

### 6. Proposed Architecture
Include:
- major components
- each component's responsibility
- interaction flow between components
- external systems and dependencies

### 7. Data Flow
Describe step-by-step how data moves through the system.

### 8. API / Interface Boundaries
Where relevant, define:
- producer / consumer
- request / response responsibilities
- sync vs async boundaries
- event / queue / database interaction

### 9. Data Model Draft
List main entities / tables / objects / indexes only if relevant.

### 10. Deployment View
Where relevant, describe:
- client / frontend
- backend services
- databases
- caches
- queues
- model serving layer
- cloud / cluster / edge placement

### 11. Security and Risk Considerations
Include authentication, authorization, secrets, PII, logging, abuse risk, failure modes, and operational risk if relevant.

### 12. Open Questions
List what still needs confirmation.

### 13. Recommended Next Steps
Give a short phased plan:
- Phase 1: MVP
- Phase 2: hardening
- Phase 3: optimization / scale

4. If the requirement clearly involves AI, LLM, OCR, RAG, search, speech, face recognition, or recommendation:
   add an "AI Capability Mapping" subsection under Proposed Architecture:
   - model/service needed
   - input/output
   - fallback behavior
   - evaluation concerns

5. If the requirement clearly involves operational systems, emergency response, healthcare, dispatch, or location intelligence:
   add a "Decision Logic" subsection:
   - ranking logic
   - optimization logic
   - rules vs model boundaries
   - human override points

6. Avoid pretending certainty.
If parts are unknown, write:
- "Assumption:"
- "Open question:"
- "Recommended default:"

## Output template
Use this exact top-level structure:

# Architecture Draft: <short system name>

## 1. Objective
## 2. Scope
## 3. Assumptions
## 4. Functional Requirements
## 5. Non-Functional Requirements
## 6. Proposed Architecture
## 7. Data Flow
## 8. API / Interface Boundaries
## 9. Data Model Draft
## 10. Deployment View
## 11. Security and Risk Considerations
## 12. Open Questions
## 13. Recommended Next Steps

## Quality bar
The result should be review-ready, not brainstorm-like.
Prefer practical architecture over academic explanation.
Keep component names consistent.
Do not invent unnecessary microservices.
