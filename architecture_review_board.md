# Architecture Review Board

## What is an ADR(Architecture Decision Record)
An architecture decision record (ADR) is a document that captures an important architectural decision made along with its context and consequences.
The goal of this document is to provide a fast overview of ADRs, how to create them, and where to look for more information.
### Suggestions for writing good ADRs
Characteristics of a good ADR:
* Point in Time - Identify when the architectural decision was made.
*	Rationality - Explain the reason for making the particular architectural decision.
*	Immutable record - The decisions made in a previously published ADR should not be altered.
*	Specificity - Each ADR should be about a single Architectural Decision.
#### Characteristics of a good context in an ADR:
*	Explain your organization's situation and business priorities
*	Include rationale and considerations based on social and skills makeups of your teams
#### Characteristics of good Consequences in an ADR:
*	Right approach - "We need to start doing X instead of Y"
*	Wrong approach - Do not explain the AD in terms of "Pros" and "Cons" of having made the particular AD
#### A new ADR may take the place of a previous ADR:
*	When an AD is made that replaces or invalidates a previous ADR, a new ADR should be created

#### ADR Template

---

### ADR 000

### Background
What is the background that is the driver for this particular ADR? What is the problem?
### Requirements
Anything that we need to achieve this, any prerequisites or external dependencies?
### The solution
What is the actual solution to the problem?
### Design/Architecture
What is the actual change in more depth? How is it going to affect the current system?
Good place for some diagrams (you can use draw.io or Visio)
### Options considered
What other options have we considered?
### Supporting Information
Any supporting information around the change, things that the ARB needs to know in order to make an informed decision.
Main Benefits
Drawbacks and risk
### Outcome
What is going to change after we execute on this ADR?

---

## Governance
### Who is on the ARB
There are two organizational models that can be a fit depending on the team and project.
#### Democratic ARB
A democratic setup usallly involes the whole team and has votes distributed equaly amongs them, to pass an ADR it has to collect 50%+1 of the vote by the end of the review period.

The review period for such a setup can be two weeks and be aligned with traditional SCRUM sprints.
The Sprint Demo is going to be a good place to notify the team what is the status of the ADR's for the last sprint.

This setup is recommended for teams that are 5+ people, with a small team.
#### Authoritive ARB


