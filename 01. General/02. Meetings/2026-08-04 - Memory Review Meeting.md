---
date: 2026-03-11
type: Meeting
meetingType: general
summary:
teams:
projects:
attendees:
  - "[[Steven]]"
tags:
---
## Preperation
- [ ] Prepare for Meeting

## Agenda & Files
- Simple Presentation
- Demo
## Notes
* Given V1 Exist, V2 is more into Reliability + Industry Standards of how Memry standard functions and platform for future memory.
	* Categorization of Memories
		* Short Term + Long Term
			* Semantic Facts - Architecture Facts, Relation is
	* Architecture - Ingest Path
		* Entry Points
			* APIs and Kafka Topics -- Should we land Direct to Kafka Topic, or should that be abstracted by API as well?
	* Ingestion Path
		* Agent has a skill that ingests the memory (Letta AI)
		* Write Paths: Agent, Chat, Manual Button
			* Amit will want to know what the API calls are for the agent
		* Question: How do we track the data? How to determine if row is valid or not?
			* Baically they're always valid
	* Background Services that Improve Memory
		* Curator service runs through Kafka, and reads data from Summarized Memory to send data to Long Term Memory. Event driven system.

![[Meetings Action Items.base]]

##### Confluence/Google Doc Template
###### Purpose
Why we are here
###### Inputs
Doc / backlog / design / decisions
###### Questions to answer
The 2–4 things that must be resolved
###### Decisions needed
What should be finalized today
###### Next steps / owners
Who does what by when