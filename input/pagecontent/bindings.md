<a name="binding"/>

Most HL7 data elements do not intend to allow that all concepts from a Code System are to be used. A constraint on which values are permitted for a particular business case must be asserted. 
In HL7 this is known as Terminology Binding and it asserts a specific relationship between a data element and certain Value Sets in the context of a particular business case, which is usually 
defined in an Implementation Guide. In Implementation Guides and some other standards artifacts, attributes and elements may be bound to Value Sets. HL7 has defined many types of bindings, 
such as model binding and Context Binding in Version 3, and other types in FHIR and Version 2. Please refer to the specific messaging standard for further information about product 
family-specific bindings. 