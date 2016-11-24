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
* Concurrency between now and at least Swift 5 is going to be Dispatch based. From Swift 5 and onwards there may be a new concurrency model. We’ll need to transition at that time.
* Assuming Dispatch gives us the same problem as elsewhere when migrating to a new concurrency model, so we share the problem/solution
* HTTP APIs should be available separately from networking/concurrency, as well as a combined.

_What model are we going to use? Should request/response be value types or reference types?_  
* The Open Swift effort hit a few issues over models, and disagreements on the HTTP models. Reference vs. value types for the request class.
* There’s some lessons learned from the openswift / swiftx experience - should be reviewed in the next meeting.


_HTTP 1.x vs HTTP/2 support_  
* HTTP2 is going to be unavoidable, so we should probably include it in the first version so we don’t risk breaking APIs


_Use cases:_  
* HTTP on server only? What about on the client for device -> device?
* Foundation has a dependency on libcurl, we’d ideally help to allow that to be removed.


_Reference vs. value-types_
* (Logan) Vapor had success with reference types rather than value types
* (Shmuel) Kitura had issues moving NSData -> Data, resulting in a ~20% performance reduction. Middlewares work better with reference types
* (Ben C) We should separate semantics from performance. 
* In general we are going to be passing request/response around. The question is really about whether the caller needs access to the changes from the callee.
* Middleware adds features into the request - callee returns to caller, and does so in a chain


_Encoding issues:_
* Header as ASCII vs. content-body in other encodings
* At the lowest level, we’ll just be providing bytes - the framework can deal with the contents?

_Use of C vs pure Swift parsing:_
* Swift “port” of the Node.js c-http parser done by Dave Sperling
   * https://github.com/smithmicro/HTTPParser
   * As close to the C version as possible - line for line transliteration.
   * Use of UnsafePointer is already in place
   * Significant time is still being spent in reference counting - would benefit from an expert in Xcode Instruments reviewing the codebase.
   * Vanilla c-http parser achieved 700K requests/sec, vs 500K for the Swift "port" - so c-http is currently ~40% faster. 
* Using pure-Swift has the potential to enables deeper level of inlining, so may ultimately give greater performance
* Helge Heß has done similar C vs Swift implementation comparisons:
   * https://github.com/helje5/http-c-vs-swift/
   * c-http parser almost exclusively uses macros to inline everything.
   * Tried to replicate using the unofficial `@inline(__always)` which improves perf quite a bit. BUT it has also been very fragile, i.e. the Swift 3 compiler would often just crash etc.
   * Found similar results: c-http parser us much faster than the Swift implementation.
* Using Swift code may also enable a wider set of contributors/maintainers for the code from the swift community (vs. the existing community working on the C code).
   * However if we reuse then it's something the Swift community needn't maintain at all.
* Does HTTP2 parsing affect our choice?


