### Characteristics of a Value Set Definition Overview

#### Intended Audience

This specification is primarily intended for terminology system designers, individuals responsible for implementing standards that use terminology subsets 
and subject matter experts tasked with creating or understanding terminology artifacts. It is assumed the readers will be familiar with the terminology material 
in the current version of “Core Principles and Properties of HL7 Version 3 Models.”1 Some of the overview material will be important for less technically 
focused individuals to understand as they create terminology content for use in implemented systems.  

Those individuals looking for the highlights should focus on the Value Set Definition Specification section as this provides the overall structure of a Value Set. 
They should also review the details presented in the Content Logical Definition section. The section An HL7 Value Set Definition Expression Syntax provides a 
default set of functions that can be used (and is used for HL7 v3 Value Set definitions as published with the HL7 Version 3 Standards) to logically define the 
code content of a Value Set Expansion Code Set2. To understand how a Value Set Definition is not the same as a Value Set Expansion, see the sections Value Set 
Expansion and also Relationship Between the Value Set Definition and Value Set Expansion Code Set.  

Those readers particularly interested in understanding the set of functions used to define a Value Set Definition Content Logical Definition should study the work 
undertaken for defining a new standard describing An HL7 Value Set Definition Expression Syntax. While this is generally useful for Value Set implementers, 
it is noted that other Value Set Definition Content Logical Definition formal syntaxes are now supported (see Content Expression).

#### In Scope

This document is a normative track specification that describes the data elements that formally define and characterize (describe) how to create an HL7 conformant 
Value Set. All references to “Value Set” and “Code System” in this document, unless specifically noted, are to an HL7 Value Set as described in this standard and 
Code System as defined in HL7 Core Principles. These include:
* Metadata used to identify and define a Value Set Definition 
* The Functions that can be used to construct a Value Set Definition Expression which defines the intended coded content. This is described in the HL7 Value Set 
Definition Expression Syntax section. This expression is used in the Content Logical Definition.
* Elements to support Value Set Definition versioning  

The document also includes informative material describing “best practices” in the use of certain elements of the Value Set Definition, such as best approach 
versus allowed use of additional or alternative Concept Representations.

#### Out of Scope

The following items have been declared explicitly out of scope for this initial release of this Standard:
* Implications of the use of this Standard in evaluation of post-coordination concepts, even though support for inclusion of expressions is tacitly possible given 
the functionality described in the Content Logical Definition section, and the fact that such post-coordinated expressions can be communicated in a string.
* This Standard does not describe an exchange model or syntax. 
* Content in the Appendix is included as Informative material and is not a part of the Normative material of the specification.

#### Background

The definition of Value Sets is a required activity in completing the specification of most health information technology artifacts. To date, the approach 
for such definition has not been consistent within HL7 standards. Many of the required elements and approaches for Value Set Definition are embedded in existing 
HL7 product family artifacts (V2.x, V3, CDA and FHIR standards), but these are not applied or implemented consistently.  

In HL7 normative standard "Core Principles and Properties of HL7 Version 3 Models" section 5.1.3, it is explicitly noted that "a Value Set is only persisted as 
its Value Set Definition, which is a machine-processable set of 1 or more formalisms that permit a specific collection of coded concepts at a given point in time 
to be reliably reproduced." The HL7 Common Terminology Services Standards also describe various mechanisms and functions to produce Value Set Expansions from Value 
Set Definitions. However, to date there is not an explicit list of the precise data items needed for the Value Set Definition expressed with the imprimatur of a 
normative standard. This standard is a major step to achieve that goal.

#### Need for this Standard

Currently, an explicit list of all the fields in an HL7 Value Set Definition has surfaced only in the informatively-balloted MIF (Message Interchange Format), 
with a general description of the fields in the normative Core Principles specification, and the STU ballots in FHIR. A more accessible and standardized description 
of the required elements is necessary to facilitate interoperability and sharing of Value Set Definitions across HL7 artifacts and the Health and Clinical Research IT 
communities at large.  

This Standard is intended to provide a formal specification of the data and metadata that are needed to formally define and describe a Value Set. Particular goals include:
* Organizations within the Health and Clinical Research IT communities that implement this Standard will have clearly defined and described Value Sets, including a clear 
description of the mechanism (functions to perform) that provides the expansion of the Value Set. This enables sharing of Value Set information accurately and unambiguously 
within and between organizations.
* Since Value Sets form a vital part of the artifacts needed to facilitate semantic interoperability, implementing this Standard will support organizations in their efforts 
to achieve semantic interoperability in both internal and external communication.
* In addition, implementing this Standard for Value Set Definition in applications such as repositories will support organizations in maintaining the meaning of the 
repository content over time, facilitating data aggregation and data analysis.