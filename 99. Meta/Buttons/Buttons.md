

```button
name Update
type append template
action Meetings/Standup Update Template
templater true
color orange
```
^button-standup-update

```button
name Create New Standup  
type note(01. General/03. Standups/Standup - <% tp.date.now("YYYY-MM-DD") %>, split) template  
action Meetings/Standup Template  
templater true  
color green
```
^button-create-new-standup

```button
name Create New Meeting  
type note(01. General/02. Meetings/<% tp.date.now("YYYY-MM-DD") %>, split) template  
action Meetings/Meeting Template  
templater true  
color green
```
^button-create-new-meeting

```button
name New Person
type note(01. General/People/<% tp.system.prompt("Person name") %>, split) template
action People/People Template
templater true
color blue
```
^button-new-person

