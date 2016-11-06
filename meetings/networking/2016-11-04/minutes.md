# Networking sub-team kick-off

### Initial Agenda:
* Introductions
* Goals
* Development process overview
* Next Steps

### Attendees:
* Chris Bailey - IBM, Kitura and Swift.org stuff
* William Dillon (hpux735) - Swift-ARM, embedded systems, mac, linux, etc
* Alfredo Delli Bovi - contributions to Swift core. Background in Node.js/PHP
* Steve Algernon - Apple, CF, CFNetwork, NSURLSession
* Paulo Faria - Zewo
* Thiago Holanda - Zewo, iOS Developer and Python.
* Morgan Lieberthal - Mac / backend web developer
* John Lin - iOS dev, Ruby, Python & Erlang
* Illia Tykhonkov - iOS developer
* Matt DeFoor - Condrey Corporation 
* Piers Mainwaring - Backend web dev
* Tyler Stromberg – iOS/Mac dev; Ruby, Elixir, Go
* Lasse Jansen - iOS/Mac developer
* Bill Abt - IBM,  Swift@IBM - Kitura, BlueSocket, BlueSSLService
* Johannes Weiss - Apple, iCloud
* Gregor Milos - Apple, iCloud
* Scott Lessans - Full Stack/Robotics; nourish.ai
* Ben Cohen - Swift standard lib @Apple

### Minutes:

_Q) Don’t we just need a layer on POSIX? Or just the intent of the POSIX layer? How are developers going to use the APIs in the most effective way? Do they really need the low ever APIs?_  
* Devs really just want to use high lebel APIs that are focused on their use case.  
* We we take the approach of building the high level APIs, and use that to inform us of what the lower level capabilities need to be?  
* A justification for lower-level APIs is the impedance mismatch between POSIX C API and Swift.   This is especially evident in the variadic nature of fcntl, and the prevalence of bit-pattern casting of similar structs, such as sockaddr.

* Some very low level stuff that missing:
  * Errno and error handling - might be a standard library thing (POSIX lib)
  * Swift-compatible implementations of fcntl and ioctl
  * Basic address processing: resolution, conversion, equality


_Q) Whats the value of high level vs low level APIs?_  
Example: Building an interface with an embedded system. The embedded system implements a proprietary mechanism using UDP multicast.  This necessitated manually joining multicast groups, and sending and receiving multicast packets.  
An attempt was made to try to do it with Vapor's network code, but there were difficulties because of the usage assumptions in the Vapor code, such as private methods for managing internet address structures. To achieve what was required, the code had to be forked and modified.  


* We should be able to expose sockets at a fairly high level - I/O plus config plus policy.  
* But if the fuction a user needs is not there, they will have/need to “drop down” to lower level APIs.  
* Is that dropping down to platform specific C code, or to a “Swift” layer API?  
  * Dropping down to a Swift layer more is desirable and safer.  


_Q) How do we deal with platforms that have additional capabilities?_  
Does the user have to use C code there, or should we provide a way to have per-platform extensions?  
* Swift provides extensions…  
* Platform capability checking “#if os(...)”  


_Q) If we have high level abstractions, do we have to assume what the concurrency model is?
If so, will that prevent other concurrency choices being made, or do we need to provide a lower level construct (as well) that allows you to chose your own model?_ 
* We can’t assume what the concurrency model is going to be yet - because those discussions are yet to happen.  

* We could provide APIs that build up in layers:
  * Lowest level - no assumptions on concurrency. File descriptor and use your own polling.  Is blocking I/O and select() enough on this layer?
  * Start to bring in async model - Dispatch based for the “default”
    - Protocol based with a default implementation?
  * Higher level abstractions - based on what you’re trying to do.

* APIs at the lowest layers are likely to be more concrete (as they are RFC specified) - although we have to decide how to make them “Swifty”.


**Note:** We need to ensure that we use proper terminology in order to avoid confusion:  
* Async vs. Sync (API level)
* Blocking vs. Non-blocking IO (Concurrency model level)  

Also, a nice, clear definition of what being more “Swifty” means is probably needed - at least one we can agree on.