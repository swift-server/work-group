## Server APIs Work Group

The Server APIs Work Group is responsible for steering the [Swift Server APIs](http://swift.org/server-apis/) project, which is an evolving set of Swift libraries developed as part of the Swift open source project to provide fundamental capabilities for building server-oriented software.

The work group consisting of a core team, stakeholders from the server-side Swift community, and anyone who wants to get involved. The work group consists of three roles: core team member, stakeholder and contributor. Participants may have more than one role in the work group.

Everyone is welcome to contribute to the Server APIs Work Group through participating in a range of activities including joining as a stakeholder, participating in design discussions, asking or answering questions on the mailing lists, reporting or triaging bugs or by submitting pull requests to the project(s) for implementation or tests.

### <a name="focus-areas"></a>Current Focus Areas
The work group is initially focussing on the creation of API proposals are for base networking, security/encryption and HTTP parsing:

* **Base Networking**: Provide a portable interface for low level socket based network based I/O, including TCP/IP and UDP protocols, IPv4 and IPv6 support and domain name resolution. Support should be provided to create and use both synchronous and asynchronous non-blocking connections.

* **Security and Encryption**: Provide common cryptographic constants and cyphers along with keychain and certificate management, and SSL/TLS based secure transport. This must integrate with the base networking support to provide secure sockets, and with the HTTP parsing library to provide HTTPS support.

* **HTTP and WebSockets**: Provide low level HTTP parsing, including HTTP, HTTP/2 and WebSocket support making it possible, in conjunction with the security and networking APIs, to create secure HTTP and WebSocket servers.

### <a name="steering-team"></a>Steering Team
Analagous to the primary Core Team for Swift, the work group has a steering team that is responsible for providing overall technical direction, ensuring co-ordination both between the various API efforts (for example around Network, Security and HTTP integration for HTTPS) and with the wider Swift Core Libraries and language. Membership of the steering team is contribution based and is expected to evolve over time.

The initial steering team consists of:

* Chris Bailey (@seabaylea, IBM Kitura)
* Logan Wright (@LoganWright, Vapor)
* Paulo Faria  (@paulofaria, Zewo)
* Steve Algernon (@salgernon, Apple)

### <a name="stakeholders"></a>Stakeholders
The work group also has stakeholders who represent server-side frameworks or applications. They are responsible for providing early input on use cases and API design as part of the iterative design and implementation process, and to adopt the new APIs into their frameworks.

Joining and leaving the work group as a stakeholder is a straightforward process. The only requirement is to raise a Pull Request to add or remove your name from the stakeholder list in this project, which will act to add or remove you from invites to formal work group discussions.

The initial stakeholders consists of:

* Gregor Milos (@gmilos, Apple)
* Kyle Jessup (@kjessup, Perfect)
* Robert Dickerson (@rfdickerson, IBM Kitura)
* Tanner Nelson (@tannernelson, Vapor)
* Tom Doron (@tomerd, Apple)

### Additional Information
More information can be found in the [Server APIs pages](http://swift.org/server-apis/) of [swift.org](http://swift.org), or by posting to the [swift-server-dev](https://lists.swift.org/mailman/listinfo/swift-server-dev) mailing list.

