
This page provides examples of Value Set content defined using an expression-based approach. These examples illustrate different patterns for defining Value Sets, including enumerated definitions, groupings, and intensional definitions based on hierarchical relationships and properties.

The goal of these examples is to demonstrate how expression-based Value Set definitions are used.

### Total Colectomy Value Sets

The Total Colectomy Value Sets described in these examples are actual Value Sets used in the US electronic quality measure program. The 
<a href="https://vsac.nlm.nih.gov/valueset/2.16.840.1.113883.3.464.1003.198.12.1019">Total Colectomy Grouping</a> example and the three 
grouped Value Sets that make up the grouping: <a href="https://vsac.nlm.nih.gov/valueset/2.16.840.1.113883.3.464.1003.198.11.1036">Total Colectomy CPT</a>, 
<a href="https://vsac.nlm.nih.gov/valueset/2.16.840.1.113883.3.464.1003.198.11.1035">Total Colectomy SNOMED CT</a>, and 
<a href="https://vsac.nlm.nih.gov/valueset/2.16.840.1.113883.3.464.1003.198.11.1143">Total Colectomy ICD-10-PCS</a>, all exist in the US NLM Value Set Authority Center (VSAC). 

The Total Colectomy Grouping example demonstrates how a single Value Set using VSAC's grouping syntax could be constructed using enumerated Concept Codes from multiple 
Code Systems.

### RoleClass-based Value Sets

The <a href="http://terminology.hl7.org/ValueSet/v3-RoleClassAssignedEntity">RoleClassAssignedEntity Value Set</a> uses the <a href="http://terminology.hl7.org/CodeSystem/v3-RoleClass">RoleClass Code System</a>. This example demonstrates two things:
1.	Both <a href="http://terminology.hl7.org/ValueSet/v3-RoleClassAssignedEntity">RoleClassAssignedEntity</a> and <a href="http://terminology.hl7.org/ValueSet/v3-RoleClassContact">RoleClassContact</a> use an "intensional" definition style to identifying Concepts to be included in the Expansion Code Set wherein a single 
Concept Code is provided along with a relationship traversal that clarifies that a transitive closure traversal is to be followed to find all Concept Codes related to the Concept Code provided. This 
is how "and all descendants" is communicated.
2.	<a href="http://terminology.hl7.org/ValueSet/v3-RoleClassAssignedEntity">RoleClassAssignedEntity</a> unions together the "Concept Code and all descendants" noted above plus a reference to another Value Set - <a href="http://terminology.hl7.org/ValueSet/v3-RoleClassContact">RoleClassContact</a>.

### Urine Albumin Lab Test Value Sets

The Urine Albumin Lab Test Value Set in this example uses LOINC properties to create an expression to capture all LOINC codes that measure albumin in a urine specimen. The expression below was created using 
<a href="https://apelon.com/solutions/terminology-tooling/dts/">Apelon's Distributed Terminology System (DTS)</a>. 

<figure>
<img src="{{site.baseurl}}subsetexpression.png"
     alt="LOINC Value Set Expression"
     style="border: 1px solid black; display: block; margin: 10px 0; clear: both;">
</figure>

This expression uses an intensional definition, and when expanded includes the following Concept Codes:

<figure>
<img src="{{site.baseurl}}subsetpreview.png"
     alt="LOINC Value Set Expansion"
     style="border: 1px solid black; display: block; margin: 10px 0; clear: both;">
</figure>
