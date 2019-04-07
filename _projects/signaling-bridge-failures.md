---
name: "Signaling bridge failures"
desc: "Errors from foreign networks should be properly handled in Matrix"
difficulty: "Medium"
issues: 
mentors: "Half-Shot"
initiatives:
 - GSoC
tags:
 - Bridges
 - Synapse
 - Riot
---

Bridges in Matrix do currently have no mechanism to handle and communicate failures in the network they are bridging. This can – independent of Matrix's eventual consistency – lead to cases where only some but not all recipients get a group message. As these partially failed deliveries lead to confusion and uncertainty, users should be warned in this kind of situation.

This project enables bridges to signal failures of their network to the group. Furthermore clients and bridges are adapted to support the new failure and error states.

##### Expected Results

With the completed project users can now be sure not to mistakenly think a message has been delivered via a bridge if it has not.

- Work on The Spec to support new group message types
- Work on Synapse to support bridges with this feature
- Work on Riot Web to display to a user if a message could not be delivered to everyone (UX if there is time)
- Extend at least one bridge to support the new mechanism

#### Knowledge pre-req
Python, JavaScript, HTML, CSS
