# Standup
`button-create-new-standup`
## Notes
```dataview
TABLE date AS "Date", summary AS "Summary", projects AS "Projects", teams AS "Teams"
FROM "01. General/Standups"
WHERE type = "meeting" AND meetingType = "standup"
SORT date DESC
LIMIT 5
```
## Action Items 
```dataview
TASK
FROM "01. General/Standups"
WHERE type = "meeting" AND meetingType = "standup"
WHERE !completed
SORT file.day DESC
```

# Meetings
`button-create-new-meeting`

## Notes
```dataview
TABLE date AS "Date", meetingType AS "Kind", summary AS "Summary", projects AS "Projects", teams AS "Teams"
FROM "01. General/Meetings"
WHERE type = "Meeting" AND meetingType != "standup"
SORT date DESC
LIMIT 5
```

## Action Items
```dataview
TASK
FROM "01. General/Meetings"
WHERE type = "meeting" AND meetingType != "standup"
WHERE !completed
SORT file.day DESC
```


```tasks
not done
tag includes #standup-action
path includes 01. General
sort by due
```
