This implementation guide is consistent with the previously published *Characteristics of a Value Set Definition, Release 1 (VSD)* normative specification. Changes from the previous 
specification are listed in the <a href="#changes">Changes From Characteristics of a Value Set Definition, Release 1</a> section. 

The content presented in the “Characteristics of a Value Set Definition” subtabs within this IG constitutes *Characteristics of a Value Set Definition, Release 2*. Within those subtabs, references to “this standard” refer specifically to <i>Characteristics of a Value Set Definition, Release 2</i>.

### Intended Audience

This specification is primarily intended for terminology system designers, individuals responsible for implementing standards that use terminology subsets 
and subject matter experts tasked with creating or understanding terminology artifacts. It is assumed the readers will be familiar with the terminology artifacts
described in this guide. Some of the overview material will be important for less technically focused individuals to understand as they create terminology content
 for use in implemented systems.  

Those individuals looking for the highlights should focus on the <a href="valuesetdefinition.html">Value Set Definition Specification</a> section as this provides the overall structure of a Value Set. 
They should also review the details presented in the <a href="cld.html">Content Logical Definition</a> section. To understand how a Value Set Definition is not the same as a Value Set Expansion, see the sections <a href="vsexpansion.html">Value Set Expansion</a> and also <a href="valuesetdefinition.html#relationship-between-the-value-set-definition-and-value-set-expansion-code-set">Relationship Between the Value Set Definition and Value Set Expansion Code Set</a>.

Readers interested in understanding the set of functions used to define a Value Set Definition Content Logical Definition should read the <a href="https://www.hl7.org/implement/standards/product_brief.cfm?product_id=437">Characteristics of a Value Set Definition, Release 1</a> section named "An HL7 Value Set Definition Expression Syntax". Other Value Set Definition Content Logical Definition formal syntaxes are supported 
and are described in the <a href="cld.html#content-expression">Content Expression</a> section.

### In Scope

This document describes the data elements that formally define how to create a Value Set that conforms to HL7 specifications. All references to “Value Set” and “Code System” in this document, unless specifically noted, are to an HL7 Value Set and Code System defined in this standard. These include:
* Metadata used to identify and describe a Value Set Definition 
* Elements to support Value Set Definition versioning  

The document also includes material describing best practices in the use of certain elements of the Value Set Definition, such as best approach 
versus allowed use of additional or alternative Concept Representations.

### Out of Scope

The following items have been declared explicitly out of scope for this Standard:
* Implications of the use of this Standard in evaluation of post-coordination concepts, even though support for inclusion of expressions is tacitly possible given 
the functionality described in the Content Logical Definition section, and the fact that such post-coordinated expressions can be communicated in a string.
* This Standard does not describe an exchange model or syntax. 

### Background

The definition of Value Sets is a required activity in completing the specification of most health information technology artifacts. To date, the approach 
for such definition has not been consistent within HL7 standards. Many of the required elements and approaches for Value Set Definition are embedded in existing 
HL7 product family artifacts (V2.x, V3, CDA and FHIR standards), but these are not applied or implemented consistently.  

This standard has already explicitly noted that "a Value Set is only persisted as its Value 
Set Definition, which is a machine-processable set of one or more expressions that permit a specific collection of coded concepts at a given point in time to be reliably 
reproduced." The <a href="https://www.omg.org/cgi-bin/doc?formal/15-04-09.pdf">Common Terminology Services – Release 2 (CTS 2)</a> standard also describe various mechanisms and functions to produce Value Set Expansions from Value Set Definitions. This standard provides an explicit list of the precise data items needed for the Value Set Definition.

### Need for this Standard

This Standard is intended to provide a formal and accessible specification of the data and metadata that are needed to formally define and describe a Value Set. Particular goals include:
* Organizations within the Health and Clinical Research IT communities that implement this Standard will have clearly defined and described Value Sets, including a clear 
description of the mechanism (functions to perform) that provides the expansion of the Value Set. This enables sharing of Value Set information accurately and unambiguously 
within and between organizations.
* Since Value Sets form a vital part of the artifacts needed to facilitate semantic interoperability, implementing this Standard will support organizations in their efforts 
to achieve semantic interoperability in both internal and external communication.
* In addition, implementing this Standard for Value Set Definition in applications such as repositories will support organizations in maintaining the meaning of the 
repository content over time, facilitating data aggregation and data analysis.

### Data Types Used

The data types used by this specification are based upon FHIR <a href="https://build.fhir.org/datatypes.html#primitive">Primitive Type</a> data types. The previous published release of Characteristics
of a Value Set Definition used data types from R2 and ISO 21090, but FHIR data types were used here for access and visiblity. There may be nuances with data types across the product families, and it is acceptable 
to use another set of data types. The FHIR data types are intended to act as a guide.

A data type not defined by FHIR but used here is COLL, which is defined as a “Group of elements”. It is a data type composed of the components described in the subelements. 
This is similar to the <a href="https://build.fhir.org/datatypes.html#primitive">BackboneElement</a> in FHIR.

### Changes From Characteristics of a Value Set Definition, Release 1
<a name="changes"/>
 In addition to the changes to the data types mentioned in the section above, 

* Loosened constraints on Value Set Identifiers to align with current implementations
* Changed name of Workflow Status element to Workflow Status Description
* Removed HL7 Value Set Definition Expression Syntax based on feedback that this syntax is complex and can be referenced as-is in previously published specifications
