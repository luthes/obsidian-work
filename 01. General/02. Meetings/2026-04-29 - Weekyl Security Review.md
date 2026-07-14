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
* Brian working on Signal Monitoring Chat Bot
	* Will hit Snowflake, so that might be a problem. 
	* Customer call information t hat is Snowflake either that or in Salesforce directly
* DataOS MCP Servers
* Capabilities Checks
	* Which Capability and which tool it's specifically tied to and what that capability check is truly doing
	* Add to spreadsheet capability checks to each tool
	* One Question:
		* Authorizing Gate on which Agents are made available through Agentic Platform.
		* Each agent needs it's own security review
		* Where are we at with LangGraph?
			* Not currently authorized to use LangGraph
		* No new APIs
		* Login Context Information is good
			* Do we need System Identiies? Yes, one is being deprecated, because we're doing a Service to Service Identity -- Leverage S2S (SYstem to System) instead. But separate System Identiy that is more customer related -- 
		* Me and/or Casey should follow up with Nathan Humbert about System Identities
		* After Capabilitiy Checks Mapped to Tools we can move to staging.
			* Add System/Service Roles to the Google Spreadsheet end to end, from user to system so we can show what role that user is going to be using. 
			* It's not foolproof, there is no automation that automates access to Snowflake vs AMS system.
				* So we'd need a separate Okta group probably a lot of stuff to automate there
		* Leveraging specific service user in Snowflake?



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