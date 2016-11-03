# Security sub-team kick-off

### Initial Agenda:
* Introductions
* Goals
* Development process overview
* Next Steps

### Attendees:
* Chris Bailey - IBM, Kitura and Swift.org stuff
* Cătălin Stan - Interested in Swift/server as of Swift 3. Background is Linux systems programming and Obj-C. Starting withing on a fast-cgi framework, then moved on to also include http
* Johannes Weiss - Apple iCloud/Swift Server. 
* Gregor Milos - Apple iCloud/Swift Server. Building low level tools/frameworks
* Alfredo Delli Bovi - contributions to Swift core. Background in Node.js/PHP
* Tyler Stromberg - mostly working on client apps - BE stuff with Ruby, Elixir, Go
* Luke Hiesterman - Apple in the security engineering team on security APIs
* Piers Mainwaring - web & mobile dev in Swift. JavaScript/Ruby/Python on the BE. Worked on some home-rolled Swift server frameworks
* Gelareh Taban - IBM, working on security for the Swift@IBM group

### Minutes:
_Q) What are our intended timelines:_  
* We really need to have a ”1.0” for Swift 4. Previews should/will be available way before that though.
* We’re not constrained by Swift 4.0 though since we can release as packages.

_Q) How important do we see that security is on the server side? Couldn’t you just put a reverse proxy in front?_  
* You can if you put the proxy in the same container, so HTTPS isn’t/shouldn’t be a show stopper…  
* More important for outbound, as its needed for HTTPS requests of other services
* However, code portability is a must. We want the API layer to be shared among different platforms - including iOS clients and Linux/macOS servers. The implementation doesn’t have to be the same in all cases, but the APIs should be (if at all possible).
* There are going to be challenges though - we’ll need to do so in a way that doesn’t add significant overhead, and we don’t want you to have to use the Linux/server package on iOS clients.

_Q) What level should the APIs be at? Should they be multi-purpose or implement specific (server) use cases_  
ie, if I want to make a HTTP request, I don’t want to use a socket, I want to use a convenience API
* We really want so start at the lowest level, building a multi-purpose API, to provide flexibility of use case.  
* Once we have that, we can build up one or more layers of more use case based APIs.

_Q) Should be build in Swift vs reuse existing tech?_  
* Ideally want to reuse existing components, so we don’t have to maintain complex code, deal with CVEs, etc. There’s no desire to re-invent the wheel.

_Q) If we’re reusing tech, how low a level do we start the API at? Should it be just a layer on, say, common crypto?_  
* The starting point is probably just to build a common “translation layer” in Swift, and then see if we want to build abstraction layers on top of that.  
* It’s easier to build up than it is to build down.

_Q) Which tech would we use?_  
* If we want to be consistent on iOS clients and servers, then we need to use CommonCrypto/SecureTransport/Keychain at least there, and it would therefore make sense to on macOS as well.  
* On the other platforms, OpenSSL or LibreSSL probably makes sense.  
The key is making the Swift API consistent, so applications and packages that use the API can be ported.  
* There may be some issues around IO handling, certificate handling and config though.  
* There’s already an attempt to do this kind of thing in BlueSSLService, so a walk through of that might be informative of potential issues/roadblocks/dragons as we build the new approach.

### Next Steps/Actions:
* Everyone to review minutes
* Chris to post minutes to work group Git Repo and send a link to the mailing list
* Next meeting in 2ish weeks - Gelareh to walk through BlueSSLService and issues/pitfalls found during its development.