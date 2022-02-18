---
name: Implement Encrypted Search for Matrix
desc: Implement a searchable symmetric encryption (SSE) protocol in Matrix
requirements:
 - Knowledge of cryptography
 - Programming in a modern client-side language
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

In this project, the GSoC contributor will implement a recent searchable
encryption scheme [1] from the cryptographic research literature, using 
the Matrix client-server API to store the encrypted index structure on
the Matrix homeserver using standard Matrix data types, e.g. `m.file`.

[1] I. Demertzis and C.Papamanthou,
"Fast Searchable Encryption with Tunable Locality".
In Proceedings of ACM SIGMOD 2017, Chicago IL, May 2017.
[paper](https://idemertzis.com/Papers/sigmod17.pdf) | [slides](https://idemertzis.com/Papers/sigmod17.pptx) | [poster](https://idemertzis.com/Papers/sigmod17_poster.pdf)

#### Milestones

##### GSOC CODING STARTS

* Have read the Demertzis and Papamanthou (2017) paper
* Have sketched out a rough mapping of the SSE protocol onto Matrix messages, rooms, and client-server protocol

##### GSOC MIDTERM

* Have implemented the protocol for creating the encrypted index
* Have created example encrypted indexes for some public Matrix rooms

##### GSOC FINAL

* Have implemented the protocol(s) for searching and updating the encrypted index in Matrix
* Have done some preliminary performance evaluation
