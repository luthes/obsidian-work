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
* User Level Context
	* When user is having conversation with an agent. 
		* [Doc: Contenxt Managmenet SYstem IDD](https://newrelic.atlassian.net/wiki/spaces/CRG/pages/4600234037/In-Review+Context+Management+System+IDD)
	* Store recent history in Short Term Memory
		* summarization is based on Tokens, say 4000 tokens, that summarization is staged as a memory.
		* Summarization is owned by CRG team in CMS.
	* Memories are basically scoped to the agent, so if the user spawns 3 agents or instances of the SRE agent, it only holds that user<->agent conversation, nothing across multiple agents, etc.
* Needline in a Haystack Solution? What is this.
* Org Based Memories
	* Admin can add these memories to the Organization
	* Pop up for the user saying "save to org memory"
	* AWS Neptune (LTM) + Valkey (STM)
* Default TTL for memories, storage needs to die eventually.
	* Can the user determine the TTL for memory?
	* STM: 2 Days TTL, threads won't be open for much longer than that.
* Knowledge Base which would have relationships which would help in Semantic Search. Do we have hooks into Neptune/Algorithms?
	* When search happens, user query, short term is no semantic search. Long term, we take user query, perform semantic search on RAG/CAG system, get top k facts based on query, knowledge graph finds similar nodes, and fetches all similar nodes. Same for knowledge base as well. So Top K results.
* You can search granular memories, but it's all on semantic search for the most part.


* Front End: Siva Kumar from UI Team
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