# HTTP stream meeting 4

### Time: Thursday April 6th 
* 7pm CET 
* 6pm UK 
* 1pm EST 
* 10am PST

### WebEx and Agenda/Minutes doc:

WebEx:      URL:        https://ibm2.webex.com/ibm2-en/j.php?MTID=m69c1c150e3a3780f1308f0c529808ed9  
            password:   http  

Agenda:     https://docs.google.com/document/d/1GTm7mJH2vCAK-Ts4M3t8C3boJ18XqiFnCRuyp55eKJE/edit?usp=sharing  

If you'd like to add anything to the agenda ahead of time, please update the agenda document in Google Docs.

### Initial Agenda:         
* Review Johannes’ proposal, which includes:
  * HTTPHeaders as a struct, Body (stream) as a class
  * Access to the Body stream using async callbacks 
  * Link:           To be added

* Discussion points:
  * Use of struct for headers
    * Allows frameworks to be value-type based, or wrap in a class to be reference-type based
  * Sync vs. Async access to the body stream
    * Can we support both?
    * If not, should be be opinionated as state async, as Dispatch is the built-in concurrency approach?

If you'd like to add anything to the agenda ahead of time, please update the agenda document in Google Docs.
    https://docs.google.com/document/d/1OoRTWOn6c1ssMl-OGZ2Gy2tYxCbHy-WHCXLcZy4-uTs/edit?usp=sharing