---
name: Implement Encrypted Search for Matrix
desc: Implement a searchable symmetric encryption (SSE) protocol in Matrix
requirements:
 - Knowledge of cryptography
 - Programming in a modern client-side language (Python/Rust/Javascript/Swift/Kotlin)
difficulty: high
issues:
 - none
mentors:
 - cvwright
initiatives:
 - GSoC
tags:
 - security
 - cryptography
---

#### Description

[Searchable symmetric encryption](http://esl.cs.brown.edu/blog/how-to-search-on-encrypted-data-searchable-symmetric-encryption-part-5/) (SSE) schemes enable a client to efficiently
create, query, and update an encrypted index structure stored on a server.
Matrix currently uses [seshat](https://github.com/matrix-org/seshat) to let users
do full-text search on their messages, but this requires that the user store the
full index on every device.
Using an SSE scheme would allow users to index and search their messages
in E2E encrypted rooms from any verified device.
This will become increasingly important as E2E encryption becomes more popular,
and as more conversations move to Matrix, increasing the size of the index.


#### Milestones

##### GSOC CODING STARTS

* Have finished a review of recent papers on searchable symmetric encryption.
* Have worked with the project mentor(s) to select one protocol for implementation, based on practicality, simplicity, security, and performance.
* Have sketched out a rough design for integrating the selected protocol in Matrix

##### GSOC MIDTERM

* Have implemented the protocol for creating the encrypted index using Matrix data structures and the Matrix client-server protocol
* Have created example encrypted indexes for some public Matrix rooms

##### GSOC FINAL

* Have implemented the protocol(s) for searching and updating the encrypted index in Matrix.
* Have published a Matrix spec change (MSC) document describing the new encrypted search mechanism so that other Matrix clients can interoperate with your work.
