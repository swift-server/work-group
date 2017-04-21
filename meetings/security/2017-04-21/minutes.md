wift Server APIs: Security Stream Meeting 5

Initial Agenda:
General discussion 
APIs
Hosting, committer groups, reviewers
Testing
CI
Issues
Naming
Call for participation :-)

If you have items you want to make sure are on the agenda, please add them below:

Attendees:
Gelareh Taban
Ryan Collins
Michael Chiu
Johannes Weiss
Gregor Milos
Kevin Sweeney
Chris Bailey

Minutes:
APIs have been shared with mailing list and feedback received
Pitch sent to Swift Evolution mailing list: https://lists.swift.org/pipermail/swift-evolution/Week-of-Mon-20170403/035139.html
ACTION: Gelareh to work with Luke for more security reviews of code
ACTION: Gregor to send email to Norman Maurer and get feedback on API design and how streams can be used with OpenSSL
Project repo: https://github.com/swift-server/security
ACTION: Chris Bailey to set up Teams: admin, committer (DONE)
Testing options:
Separate test project with TLS + socket 
Or bare bone socket library within Test of the TLS library → Michael’ library?
→ We will go ahead with the minimal socket library within TLS project whilst the server group’s socket library has not yet been implemented.
Goal is to use Swift CI. TBD: plugins for orgs and build setup etc.
ACTION: Chris to work with Mishal Shah to figure out how this can be set up
Short term: Not have CI/CD pipeline. Lots of local testing for reviewers and mergers.  
Naming: TLSService, TLSEngine, TLSTransport, TLSOverlay, TLS?
Call for Contributor or reviewers
Send updates to mailing list as we start implementing


