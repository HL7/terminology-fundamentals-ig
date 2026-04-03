
The following material describes the relationship of the Value Set Definition Standard to other HL7 standards.

### HL7 Version 3 (V3)

The V3 HL7-defined Value Sets were previously specified in the HL7 Vocabulary section of the <a href="https://www.hl7.org/implement/standards/product_brief.cfm?product_id=454">HL7 
V3 Normative Edition (Foundation Chapter)</a>. The HL7-defined Value Sets published in the HL7 V3 Normative Edition were migrated to the <a href="https://terminology.hl7.org/">HL7 Terminology (THO)</a> in 2020. 

A detailed description of Value Sets (HL7 and other) and their relationships to the other aspects of the V3 Standard is provided 
in <a href="https://www.hl7.org/implement/standards/product_brief.cfm?product_id=481">Core Principles and Properties of HL7 Version 3 Models</a>, much of which is described 
in a product-agnostic approach in this IG.  

In HL7 V3, a Value Set (a collection of concepts drawn from one or more Code Systems grouped together for a specific purpose) is one of the key defined 
vocabulary structures, typically associated with a coded Model Element (in a message or document) through a vocabulary binding from its associated Concept 
Domain (for Context binding) or directly from the Model Element (for Model binding). In addition to the descriptions in the <a href="valuesetdefinition.html">Value Set Definition Specification</a> 
section of this document, the V3 vocabulary structures and their usage is described in further detail in the <a href="valuesets.html">Value Sets</a> section. 
The <a href="conformance.html">Terminology Conformance</a> section discusses Vocabulary Conformance as originally described in Core Principles and the 
<a href="bindings.html">Terminology Binding</a> provides a discussion of Terminology Binding.

The V3 HL7 Vocabulary included a large number of (> 1800) HL7-defined Value Sets – the detailed contents and descriptions are found in the HL7 V3 Normative Edition
and now published as FHIR Value Sets in the <a href="https://terminology.hl7.org/">HL7 Terminology (THO)</a>. The “source of truth” for the V3 HL7 Vocabulary 
(including the value sets) was previously the MIF (viewable using the RoseTree tool). In addition to the V3 HL7 Value Sets, there 
are many other Value Sets defined by organizations outside of HL7 (and within different product families) that are not represented or referenced directly in the MIF or Normative Edition, but still may 
be used in HL7 messages and documents. The same HL7 vocabulary binding machinery is also used for specifying these “non-HL7” Value Sets in message and document instances.  

The Data Types: Abstract R2 specification (used in the HL7 V3 RIM) contains references to Value Sets. The CD (Concept Descriptor) data type 
(and its CV flavor) contains properties for valueSet and valueSetVersion, which are used to specify the Value Set and Version that applied when the specific CD 
instance was created. It should be noted that the earlier Data Types: Abstract (R1) specification does not explicitly reference Value Sets in the CD data type 
(or elsewhere). This has potentially important implications, because the earlier R1 data types are still being widely used in the CDA R2 Standard (see the CDA 
below).

The R2 CD valueSet property is a UID (UniqueIdentifierString), which is intended to identify an object “in a globally unique and timeless manner”, and may be 
populated with either an OID (Object Identifier) or UUID (Universally Unique Identifier). This should always be populated with the Value Set Identifier.  

The R2 Data Types specification also requires that the version of the Value Set also be provided. The valueSetVersion property is a string (ST.SIMPLE), 
and its value “must properly identify a particular version of the Value Set following the rules defined by the Value Set or its publisher.” For HL7 defined 
Value Sets, the version shall be the date/time that the Value Set Definition was published in a ballot. This date will match the expectation that the 
valueSetVersion property be populated with the Value Set Expansion: from the Value Set Expansion Code Set used to populate the code component of the CD.

### HL7 Version 2 (V2)

HL7 Version 2 (V2) manages terminology through Tables, which are bound to specific data elements. The relationship between V2 and the Value Set Definition (VSD) standard is defined by the current table-based model and the evolving V2+ framework.

#### Current Table-Based Model (V2.x)

In current versions of the standard (up to v2.9.1), terminology is published as tables within the standard's narrative. These tables serve as the normative source of truth for conformance. V2 historically conflates the concepts of Code System and Value Set, as tables serve dual roles without a clean separation between the two. Additionally, some tables—particularly User-Defined tables—do not represent implementable terminology at all and instead function as concept domains.

The standard defines several table types based on content ownership and maintenance, which align with the VSD concepts of Stewardship and Scope:

* HL7-Defined: Values are published by HL7 and are universally applicable. While the values themselves may not be redefined, the tables are often extensible to allow for local additions.
* User-Defined: Values are locally or site-defined to accommodate institutional variations (e.g., patient locations). HL7 may provide suggested values as a starter set, but the governance of the final expansion rests with the implementer. Some User-Defined tables function as concept domains, containing either no codes or only illustrative examples that are not intended for direct implementation.
* HL7-External (HL7-EXT): Content is maintained by HL7 but hosted outside the V2 maintenance space (e.g., in V3 or FHIR repositories).
* External, Referenced, and Imported: These tables represent content from external standards organizations (e.g., ISO, LOINC, UCUM).

Most V2 tables are extensional (explicit lists). Intensional logic is found in Referenced or External tables, where the definition is a pointer to an external authority (e.g., "All valid codes from ISO 3166") rather than a static list within the V2 publication.

Terminology constraints are enforced via data types. CNE (Coded with No Exceptions) implies a Required binding to a specific value set, while CWE (Coded with Exceptions) allows for local extensions or text, aligning with Extensible binding principles. When V2 profiles or implementation guides constrain table values for specific use cases, the resulting artifacts more closely resemble formal Value Sets as defined by this Implementation Guide.

#### V2+: The Evolution to Computable Terminology

V2+ represents a transition in the authoring and publication of the standard, moving from narrative documents to a computable, web-based format. While the resulting web publications are versioned and static, the underlying terminology is managed as discrete, computable artifacts.

* Formal Value Set Recognition: V2+ moves toward formal recognition of terminology as Value Sets, allowing for clearer separation between the data element (the field) and the terminology constraint (the Value Set) applied to it.
* Source of Truth: For V2+, the source of truth is transitioning to formal FHIR-based artifacts, including Value Sets maintained in HL7 Terminology (THO) and V2-specific artifacts maintained in the V2+ publication repository.
* Alignment of Binding Strengths: V2+ provides an opportunity to harmonize legacy table-type distinctions with formal binding strengths (Required, Extensible, etc.) and coding strength principles defined in this Implementation Guide and other modern HL7 standards.

### HL7 V3 Model Interchange Format (MIF)

HL7’s V3 Model Interchange Format (MIF) originally defined most (though not all) of the content formal Value Set structure described in Characteristics of a Value Set Defition, including 
the formal definition, support for partitions, Code System Supplements, control over post-coordination, etc. As such, MIF is a conformant implementation of this guide.  

MIF had previously been exercised by HL7 as the primary publication mechanism (and tooling support mechanism) for HL7 V3 vocabulary maintained by HL7 International for over 
10 years. It was the format consumed by tooling such as the V3 Generator and RoseTree. It has also been used by at least some HL7 affiliates, meaning that much of the 
content documented in this specification has been subject to implementation experience and stems from real-world use cases.  

Because MIF is used specifically for HL7 use-cases, there are some constraints on what it can do. Examples include:
* No support for version identifiers other than dates or date-time values
* No support for multiple Value Set Expansion Code Sets, maintaining Value Set Expansion Code Sets or the level of detail supported in this specification for Value Set Expansion Code Sets.

### HL7 Clinical Document Architecture (CDA)

Clinical Document Architecture Release 2 (CDA R2) is one of the HL7 V3 family standards; however, CDA R2 uses Release 1 of the Data Types –Abstract specification, 
which does not include explicit references to Value Sets and versions in the CD (Concept Descriptor) or other coded data types. In particular for implementation guides 
where references to Value Sets are required, such as QRDA (<a href="https://www.hl7.org/implement/standards/product_brief.cfm?product_id=35">HL7 Implementation Guide for 
CDA® Release 2: Quality Reporting Document Architecture – Category I</a>), it may be necessary to use a CDA extension in order to represent this data – for QRDA, 
this extension is the sdtc:valueSet attribute (note that there is no extension currently being used in QRDA to represent the value set version).  

The CDA R2 base Standard includes the specification of a large number of Value Sets that are defined in tables contained within the CDA R2 Standard document itself (<a href="http://www.hl7.org/implement/standards/product_brief.cfm?product_id=7">HL7 Clinical Document Architecture, Release 2.028</a>). The majority of these Value Sets 
are enumerations (extensional definitions), but some are defined by rather simple intensional rules – an example is “Table 31: Value set for RelatedEntity.classCode (CNE)”, 
which is defined as “all subtype of RoleClassMutualRelationship”.

### HL7 Fast Health Interoperable Resources (FHIR)

Fast Health Interoperable Resources (FHIR) is the newest HL7 specification for data exchange. It includes a specific <a href="https://build.fhir.org/valueset.html">ValueSet resource</a> 
that corresponds with much of the content found here. The ValueSet resource is a first-order structure like any other resource and can be conveyed in instances along with clinical 
data and can be queried and maintained using FHIR RESTful services.  

The design of the core ValueSet resource is limited to those features and capabilities expected to be used by most systems, so a considerable amount of the capability 
found in this specification is not supported directly by the resource. However, FHIR makes use of a profiling structure in which extensions can add capabilities 
(and constraints) not found in the base resource. Several profiles that strictly  with the capabilities defined in this document have been developed to provide guidance 
to FHIR implementers who wish to create more sophisticated Value Set Definitions. Those ValueSet profiles are part of the Canonical Resource Management Infrastructure (CRMI) 
Implementation Guide and can be found in the <a href="http://hl7.org/fhir/uv/crmi/profiles.html">Profiles</a> section.

FHIR’s ValueSet goes beyond the capabilities documented here, in that ValueSet can also be used define Code Systems “on the fly”. This is done as an implementer 
convenience as frequently Code Systems and Value Sets are created on a 1..1 basis for things like answers to questions in questionnaires, for structural codes 
and other purposes. This behavior falls outside of the scope of this document as formally, Value Set Definitions do not include the definition of Code Systems, Code System Supplements, etc.

### Common Terminology Services 2 (CTS 2)

The <a href="https://www.omg.org/cgi-bin/doc?formal/15-04-09.pdf">Common Terminology Services – Release 2 (CTS 2) specification</a> is intended to mediate among disparate 
terminology sources by defining a common information model and 
computational model. The information model specified in the CTS 2 Platform Independent Model (PIM) outlines the structural definition, attributes and associations of the 
elements common across structured terminologies and terminology elements such as Value Sets. CTS 2 does not mandate specific terminology components, but provides the 
infrastructure to support a diverse array of structured terminology representations.  

The metadata elements specified in this document could be mapped to the CTS 2 PIM. There is no evidence that it would be difficult to define how HL7 Value Sets would be 
represented in CTS 2 in accordance with the Value Set Definition Project.
