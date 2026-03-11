

```button
name Update
type append template
action Meetings/Standup Update Template
templater true
color orange
```
^button-standup-update

```button
name Action Item
type append template
action Meetings/Standup Action Item
templater true
color purple
```
^button-standup-action-item

```button
name Action Item
type append template
action Meetings/Meeting Action Item Template
templater true
color purple
```
^button-meeting-action-item

```button
name Create New Standup  
type note(01. General/Standups/Standup - <% tp.date.now("YYYY-MM-DD") %>, split) template  
action Meetings/Standup Template  
templater true  
color green
```
^button-create-new-standup

```button
name Create New Meeting  
type note(01. General/Meetings/<% tp.date.now("YYYY-MM-DD") %>, split) template  
action Meetings/Meeting Template  
templater true  
color green
```
^button-create-new-meeting

