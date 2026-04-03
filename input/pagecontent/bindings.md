<a name="binding"/>

Many HL7 data elements are not intended to be exchanged using any concept from a Code System. A constraint on which values are permitted for a business case must be asserted. In HL7 this is known as Terminology Binding which asserts a specific relationship between a coded data element and a Value Set in the context of a business case - usually defined in an Implementation Guide. HL7 has defined many types of Bindings, 
such as model binding and Context Binding in Version 3, and other types in FHIR and Version 2. Please refer to the specific messaging standard for further information about product 
family-specific Bindings. 