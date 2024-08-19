
The following material describes the relationship of the Value Set Definition Standard to other HL7 standards is provided as an INFORMATIVE supplement.

### Version 3

The HL7-defined Value Sets are specified in the HL7 Vocabulary section of the HL7 V3 Normative Edition (Foundation Chapter). A detailed description of Value Sets 
(HL7 and other) and their relationships to the other aspects of the V3 Standard is provided in Core Principles and Properties of HL7 Version 3 Models26.  

In HL7 V3, a Value Set (a collection of concepts drawn from one or more Code Systems grouped together for a specific purpose) is one of the key defined 
vocabulary structures, typically associated with a coded Model Element (in a message or document) through a vocabulary binding from its associated Concept 
Domain (for Context binding) or directly from the Model Element (for Model binding). In addition to the descriptions in Chapter 5 of this document, the V3 
vocabulary structures and their usage is described in further detail in Chapter 5 - Coded Model Elements and their Vocabularies of Core Principles and Properties 
of HL7 Version 3 Models. Section 5.1.3 of Core Principles… describes Value Sets and their attributes and associated rules (the descriptions in Core Principles… 
should be in alignment with the specifications in this document – and, where not, this is expected to be addressed in an upcoming Core Principles… release). 
Section 5.2 discusses Vocabulary Conformance. Section 5.3 provides a detailed discussion of Vocabulary Binding, including the definitions, specifications 
and rules for Model and Context (i.e. realm-specific) Binding.  

The HL7 Vocabulary includes a large number of (> 1800) HL7-defined Value Sets – the detailed contents and descriptions are found in the HL7 V3 Normative Edition. 
The “source of truth” for the HL7 Vocabulary (including the value sets) is the MIF (viewable using the RoseTree tool). In addition to the HL7 Value Sets, there 
are many other Value Sets defined by organizations outside of HL7 that are not represented or referenced directly in the MIF or Normative Edition, but still may 
be used in HL7 messages and documents. The same HL7 vocabulary binding machinery is also used for specifying these “non-HL7” Value Sets in message and document instances.  

The Data Types: Abstract R2 specification (used in current versions of the HL7 V3 RIM) contains references to Value Sets. The CD (Concept Descriptor) data type 
(and its CV flavor) contains properties for valueSet and valueSetVersion, which are used to specify the Value Set and Version that applied when the specific CD 
instance was created. It should be noted that the earlier Data Types: Abstract (R1) specification does not explicitly reference Value Sets in the CD data type 
(or elsewhere). This has potentially important implications, because the earlier R1 data types are still being widely used in the CDA R2 Standard (see the CDA 
discussion in 11.4).

The R2 CD valueSet property is a UID (UniqueIdentifierString), which is intended to identify an object “in a globally unique and timeless manner”, and may be 
populated with either an OID (Object Identifier) or UUID (Universally Unique Identifier). This should always be populated with the Value Set Identifier.  

The R2 Data Types specification also requires that the version of the Value Set SHALL also be provided. The valueSetVersion property is a string (ST.SIMPLE), 
and its value “must properly identify a particular version of the Value Set following the rules defined by the Value Set or its publisher.” For HL7 defined 
Value Sets, the version SHALL be the date/time that the Value Set Definition was published in a ballot. This date will match the expectation that the 
valueSetVersion property be populated with the Value Set Expansion: from the Value Set Expansion Code Set used to populate the code component of the CD.

### Version 2

HL7 Version 2 mentioned Value Sets in various descriptions for many years, but did not formally define them or their explicit reference. In V2.5.1, the 
CWE (Coded with Exceptions) datatype states:

> The CWE data type should be used for coded fields that are optional or where it is permissible to send text for items that are not yet a part of the 
approved value set. In the normal situation, the identifier is valued with the code from the value set. If the value of the field is known, but is not part 
of the value set, then the value is sent as text, and the identifier has no value.  

In addition, Value Sets are mentioned in the second component of the SPS (Specimen Source) datatype, where the values are drawn from HL7 table 0371:

> The table’s values are taken from NCCLS AUTO4. The value set can be extended with user specific values.  

In the discussions on V2 Conformance (section 2.12 in V2.5.1), Value Sets are mentioned as being part of the Static Definition of a Conformance Profile. 
In version 2.6, additional text was added in the definition of the CWE datatype to further describe how Value Sets are used in conjunction with the V2 coded datatypes.

The explicit reference to Value Sets and their identifiers was introduced in version 2.7, when three pairs of components were added to the CWE and CNE 
(Coded with no Exceptions) datatypes. Each pair of components holds the Value Set OID (carried as a string) and the Value Set Version ID, which is a 
Date/Time. Note that the Value Set Version ID components are defined as “the date is the date/time that the value set being used was published.” This 
should be populated with the Value Set Expansion: Date of Expansion for the Value Set Expansion Code Set from which the code populated in the code component was drawn.

### Model Interchange Format

HL7’s V3 Model Interchange Format (MIF) originally defined most (though not all) of the content formal Value Set structure described in this document, including 
the formal definition, support for partitions, Code System Supplements, control over post- coordination, etc. As such, MIF is a conformant implementation of this specification.  

MIF has been exercised by HL7 as the primary publication mechanism (and tooling support mechanism) for HL7 V3 vocabulary maintained by HL7 International for the past 
10 years. It is the format consumed by tooling such as the V3 Generator and RoseTree. It has also been used by at least some HL7 affiliates, meaning that much of the 
content documented in this specification has been subject to implementation experience and stems from real- world use cases.  

Because MIF is used specifically for HL7 use-cases, there are some constraints on what it can do. Examples include:
* No support for version identifiers other than dates or date-time values
* No support for multiple Value Set Expansion Code Sets, maintaining Value Set Expansion Code Sets or the level of detail supported in this specification for Value Set Expansion Code Sets.

A couple of minor changes to align with this specification will be performed once this specification passes Normative ballot.

### CDA

Clinical Document Architecture Release 2 (CDA R2) is one of the HL7 V3 family standards; however, CDA R2 uses Release 1 of the Data Types –Abstract specification, 
which does not include explicit references to Value Sets and versions in the CD (Concept Descriptor) or other coded data types. In particular for implementation guides 
where references to Value Sets are required, such as QRDA (HL7 Implementation Guide for CDA® Release 2: Quality Reporting Document Architecture – Category I27), 
it may be necessary to use a CDA extension in order to represent this data – for QRDA, this extension is the sdtc:valueSet attribute (note that there is no extension 
currently being used in QRDA to represent the value set version).  

The CDA R2 base Standard includes the specification of a large number of Value Sets that are defined in tables contained within the CDA R2 Standard document itself 
(HL7 Clinical Document Architecture, Release 2.028). The majority of these Value Sets are enumerations (extensional definitions), but some are defined by rather simple 
intensional rules – an example is “Table 31: Value set for RelatedEntity.classCode (CNE)”, which is defined as “all subtype of RoleClassMutualRelationship”.

### Fast Health Interoperable Resources

Fast Health Interoperable Resources (FHIR) is the newest HL7 specification for data exchange. It includes a specific ValueSet resource29 that corresponds with much of the 
content found here. The ValueSet resource is a first-order structure like any other resource and can be conveyed in instances along with clinical data and can be queried 
and maintained using FHIR RESTful services.  

The design of the core ValueSet resource is limited to those features and capabilities expected to be used by most systems, so a considerable amount of the capability 
found in this specification is not supported directly by the resource. However, FHIR makes use of a profiling structure in which extensions can add capabilities 
(and constraints) not found in the base resource. A Profile that strictly aligns with the capabilities defined in this document will be developed during the STU 
phase of this specification to provide guidance to FHIR implementers who wish to create more sophisticated Value Set Definitions.  

FHIR’s ValueSet goes beyond the capabilities documented here, in that ValueSet can also be used define Code Systems “on the fly”. This is done as an implementer 
convenience as frequently Code Systems and Value Sets are created on a 1..1 basis for things like answers to questions in questionnaires, for structural codes 
and other purposes. This behavior falls outside of the scope of this document as formally, Value Set Definitions do not include the definition of Code Systems, Code System Supplements, etc.

### Common Terminology Services 2

The Common Terminology Services – Release 2 (CTS 2) specification30 is intended to mediate among disparate terminology sources by defining a common information model and 
computational model. The information model specified in the CTS 2 Platform Independent Model (PIM) outlines the structural definition, attributes and associations of the 
elements common across structured terminologies and terminology elements such as Value Sets. CTS 2 does not mandate specific terminology components, but provides the 
infrastructure to support a diverse array of structured terminology representations.  

In the future, when an individual with sufficient knowledge of CTS 2 can provide the necessary support, the metadata elements specified in this document will be mapped 
to the CTS 2 PIM. There is no evidence that it will be difficult to define how HL7 Value Sets would be represented in CTS 2 in accordance with the Value Set Definition Project.
