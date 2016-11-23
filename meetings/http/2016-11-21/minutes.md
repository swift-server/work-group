# HTTP sub-team kick-off

### Initial Agenda:
* Introductions
* Goals
* Development process overview
* Next Steps

### Attendees:
* Chris Bailey
* Alex Blewitt
* Ryan Collins
* Ben Cohen
* Sam Liu
* Shmuel Kallner
* Tyler Stromberg
* Robert F. Dickerson
* Logan Wright
* Tanner Nelson
* David Sperling
* Kuan Huang
* Johannes Weiss

### Minutes:

_How are we going to interface these things together, ie, how HTTP sits on networking?_
* Concurrency between now and at least Swift 5 is going to be Dispatch based. From Swift 5 and onwards there may be/will be a new concurrency model. We’ll need to transition at that time.
* Assuming Dispatch gives us the same problem as elsewhere when migrating to a new concurrency model, so we share the problem/solution
* HTTP APIs should/will be available separately from networking/concurrency, as well as a combined.

_What model are we going to use? Should request/response be value types or reference types?_  
* Hit a few issues over models, and disagreements on the HTTP models. Reference vs. value types for the request class.
* There’s some lessons learned from the openswift / swiftx experience


_HTTP 1 vs HTTP2 support_  
* HTTP2 is going to be unavoidable, so we should probably include it in the first version so we don’t risk breaking APIs


_Use cases:_  
* HTTP on server only? What about on the client for device -> device?
* Foundation has a dependency on libcUrl, we’d ideally help to allow that to be removed.


_Reference vs. value-types_
* (Logan) Vapor had success with reference types rather than value types
* (Shmuel) Kitura has issues moving NSData -> Data. Middlewares work better with reference types
* (Ben C) We should separate semantics from performance. 
* In general we are going to be passing request/response around. The question is really about whether the caller needs access to the changes from the callee.
* Middleware adds features into the request - callee returns to caller, and does so in a chain


_Encoding issues:_
* Header as ASCII vs. content-body in other encodings
* At the lowest level, we’ll just be providing bytes - the framework can deal with the contents?

_Use of C vs pure Swift parsing:_
* Swift “port” of the c-http parser: as close to the C version as possible - line for line translation. 700K requests/sec with C, vs, 500K for Swift. 
* Using pure-Swift enables deeper level of inlining, so may ultimately give greater performance
* Using Swift code may also enable a wider set of contributors/maintainers for the code from the swift community (vs. the existing community working on the C code).
* Does HTTP2 parsing affect our choice?


