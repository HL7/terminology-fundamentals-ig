
One of the founding principles of terminology is the importance of the correct identification of elements.

### Global Uniqueness of Terminology Identifiers

For HL7 purposes, all identifiers for terminology artifacts must be unique within their namespaces to avoid misidentification.  

Globally unique identifiers may be created as either [Uniform Resource Identifiers](https://datatracker.ietf.org/doc/html/rfc8820) (URIs — see RFC 8820) or Object Identifiers (OIDs — see ITU-T X.660 or ISO/IEC 9834-3). 
OIDs are globally unique if the OID registration procedures defined by ISO in the 9834 series of standards are followed. A set of local identifiers may be made globally 
unique by prefixing them with a common global identifier. OIDs are created by an ISO Registration Authority, as specified in the ISO standards. HL7 is such a Registration 
Authority, and creates and issues OIDs for use in identifying objects in HL7 standards and implementations.

### OID Registry

For some scenarios, it is not enough that the identifier be globally unique; the identification must also be consistent among a group of systems. Some concepts must be consistently identified, 
such as Social Security Numbers in the USA. Other concepts, notably shared standards such as HL7-defined concepts, ISO standards, and ICD and SNOMED terminologies, need to be consistently identified 
by all systems. If consistent identifiers are not used then interoperability is degraded because communicating systems would have no way to realize when they were talking about the same thing.  

One way to produce common consistent identification is to maintain a central system where these identification concepts are registered. HL7 maintains an OID registry for this exact purpose. 
Any identifiers of interest to HL7 implementers may be registered on the [HL7 OID registry](https://www.hl7.org/oid/information.cfm), which includes
* OIDs created and issued by HL7 that refer to artifacts defined by HL7 and maintained internally,
* OIDs created and issued by HL7 that refer to externally defined artifacts, and
* OIDs created and issued by Registration Authorities other than HL7 that refer to externally defined artifacts.

Note that a small subset of the artifacts for which OIDs are issued are related to terminology.   

For more information about HL7 assigned OIDs, please visit the [HL7 OID registry](https://www.hl7.org/oid/information.cfm).  

HL7 best practice supports assigning an OID to each of its Code Systems, as well as to external standard coding systems that are being used with HL7 and HL7 Affiliate specifications.  

One of the primary objectives of the HL7 OID registry is to ensure that there is only one authoritative OID to be used for a given artifact in HL7 instances. For example, 
there is only one OID registered for the LOINC code system in the HL7 OID registry. While any organization that is an ISO Registration Authority and manages an OID root 
may create their own OID for the LOINC code system, these additional OIDs cannot be added to the HL7 OID registry because they would result in multiple OIDs for the same 
artifact. Furthermore, if an OID has been registered with HL7 for a given code system or identifier namespace, that OID SHALL be used when referencing that code system or 
identifier namespace in conformant HL7 instances. This ensures that HL7 conformant systems can rely on code systems and common public identifiers always being identified consistently.  
 
There is an FAQ with more information about the use of the HL7 OID registry that may be found at [OID Registry Frequently Asked Questions](https://confluence.hl7.org/display/HDH/HL7+OID+Registry+Frequently+Asked+Questions).

#### HL7 Terminology (THO)

An additional resource for terminology identifiers within HL7 is the HL7 Terminology website [https://terminology.hl7.org/](https://terminology.hl7.org/) (THO). THO provides web-based access to terminology artifacts 
referenced by HL7 published artifacts in a convenient, browsable form.   

THO includes content that is both internal and external to HL7. Internal content refers to terminology artifacts that are published by HL7. These include artifacts that have been published to 
support HL7 products. Internal THO content includes both the identifiers and the complete content.  

External content refers to terminology artifacts that are published and maintained outside of HL7. To ensure consistent use across HL7 implementations, information about the code systems 
and identifier systems are stored in THO for reference. These external records include all known identifiers for those systems as well as useful information about the systems. External 
records do not generally include the complete content, unless an agreement with HL7 has been made for republishing. The [HL7 Terminology Authority](https://confluence.hl7.org/display/TA/Terminology+Authority) maintains the external records and provides 
guidance for [Validating and Requesting Identifiers for External Code Systems and Identifier Systems](https://confluence.hl7.org/display/TA/Validating+and+Requesting+Identifiers+for+External+Code+Systems+and+Identifier+Systems).  

Note that there is significant cross-over between the identifiers being published via the HL7 OID registry and THO.  
