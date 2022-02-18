---
name: Matrix-Rust-SDK-Python
desc: Building Python bindings for using the Matrix Rust SDK
requirements:
# Student requirements:
 - Worked with Rust FFI
 - Familiar with building Python Bindings
difficulty: medium
issues:
# Related issues (if any)  to this project.
mentors:
# First person in contact; mentors may change before project starts.
 - Poljar
 - jplatte
initiatives:
 - GSoC
tags:
# Different technologies needed
 - Python
 - Rust
 - FFI
 - matrix-nio
---

#### Description

[matrix-nio](https://github.com/poljar/matrix-nio), a Python Matrix client
library, lacks some important features, up-to-date cryptography, the ability to
store state, support for reactions, etc. All of those missing features are
supported by the new [Matrix Rust SDK]
(https://github.com/matrix-org/matrix-rust-sdk).

This project aims to create Python bindings for the Rust SDK and integrate them
in the matrix-nio library. matrix-nio already contains multiple `Client`
classes for different use-cases, the `AsyncClient` class API is similar to the
Rust SDK API. The project should introduce a new `Client` class to `matrix-nio`
which would replace the `AsyncClient` class.

#### Milestones

##### GSOC CODING STARTS

* Initial Python bindings for Rust SDK

##### GSOC MIDTERM

* Integration into matrix-nio as a separate client implementation.

##### GSOC FINAL

* Fully working matrix-nio backed by the Rust SDK
