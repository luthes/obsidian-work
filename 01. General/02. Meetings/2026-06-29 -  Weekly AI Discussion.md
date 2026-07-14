---
date: 2026-03-11
type: Meeting
meetingType: general
summary:
teams:
  - CRG
  - Siva B's Team
projects:
  - SRE Agent
  - CMS Memory System
attendees:
  - "[[Steven]]"
  - "[[Zach]]"
  - Kiran Penumarthi
  - "[[Matt Olsen]]"
tags:
---
## Notes
* Use the Spread Sheet PM & EM Assignments for AI Group
	* https://docs.google.com/spreadsheets/d/1PIScTE0LMFdyvz-kkfs3HzuklhzFmzt4FUG9WdGWbCY/edit?gid=105325218#gid=105325218
* GA planned for SRE Agent on July 22nd. 
	* Have about 3 weeks, SRE agent tracker sheet:
		* https://docs.google.com/spreadsheets/d/1btQRTEOxh16XyQDSFjZu3YuVb-QlZxXRg44l8CiegZc/edit?usp=drive_open&ouid=112100736741601387581
* Goal is that we have unified, common architecutre across the company. We don't wantto have a ton of redundancies like we do now
	* SRE + AGentic PLatform Agents
	* Multiple databases, memory systems
	* Kiran: 
		* Multiple teams have different levels of knowledge, many MCP servers
		* Long-term Memory/Short Term Memory is here
 * Matt wants to know things at the 100k foot level, not low level things. Want's to understand things across the board. So we can make sure the infrastructure/platform track aligns with things that are in the future. 
	 * SLC Rev as an example, we're close to launch, and no one has talked to them.
	 * Need better agile delivery, better communication from us, engineers, to other parts of company (like security)
 * Right now Kiran, doesn't have the clearest picture of what's happening.
 * We don't want to repeat the history of having an Agentic Platform that's "not what people need it to be".
 * Kiran on SRE Agent: 
	 * Current SRE Agent is kind of a black box. Difficult to see how a feature will impact the performance of the SRE agent.
		 * This sounds like politics
	 * How Memories are getting formed and any kind of memory in the SRE Agent.
	 * Matt: It's not unified
	 * **We're not sure about the approach, traditional coding we have integration tests, but for this agentic use case, we don't really have any testing, so we need a few attempts to get the testing part correct.** 
 * Generally we just have a horrible process. 
 * Generally we just want to align with Kiran on different things. Details on agent, details on causal engine, different projects that are a bit of black box.
 * Partha 
	 * working on projects where they were able to standardize architectures on new use case on things around the UI components around catalog. The second is around when you change one job, how it will impact other jobs. ???
	 * Amit expecting equal thing with AI and how that can happen
	 * Probably to start we have to do things manually to see how things fit with each other, and once we have a group of stuff, we can have standardized process to get out of the way so they can do things in a self service way with specs and how it interacts with other things. 
	 * there are multiple ways to figure out how to get clarity results and how things are connected.
 * Matt is more interested in Infra/DevOps/CICD/etc. how we do test/eval, performance testing, lower envs and promoting to prod. Data Catalogs would be with Partha, etc.


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