---
name: "Matrix Visualisations"
desc: "Visualise the underlying replicated Directed Acyclic Graph datastructure"
difficulty: "Medium"
issues:
mentors:
 - erikjohnston
initiatives:
 - GSoC
tags:
 - Graphs
 - Synapse
---

When developing on Matrix it's often quite hard to visualise the underlying replicated Directed Acyclic Graph datastructure that describes the conversation history in a room. We've made some basic tools in the past like https://github.com/Kegsay/matrix-vis and https://github.com/matrix-org/synapse/tree/master/contrib/graph and https://github.com/erikjohnston/matrix-introspection but what would be really cool would be a real-time visualisation of the DAG to help folks understand Matrix, and help developers debug interesting edge cases and merge resolution scenarios when the DAG bifurcates. This could be written in any language, talking some combination of the server-server API or an enhanced version of the client-server API or just inspecting your synapse's database to visualise what's going on.

#### Expected Results

A realtime visualisation of the DAG of a given Matrix room, as seen from the perspective of one or more HSes.

#### Knowledge pre-req

Good knowledge of HTTP/REST APIs in general.
