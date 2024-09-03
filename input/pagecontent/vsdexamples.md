
Example Value Set content based on the HL7 Value Set Expansion Expression syntax, rendered within Microsoft Excel workbooks, are available for download at this url: 
<a href="http://wiki.hl7.org/index.php?title=HL7_VSD_Expression_Syntax">http://wiki.hl7.org/index.php?title=HL7_VSD_Expression_Syntax</a>

Currently the following two primary example groups are provided:

### Chlamydia Value Sets

The Chlamydia Value Sets described in these examples are actual Value Sets used in the US electronic quality measure program. The Chlamydia Grouping example and the 
three grouped Value Sets that make up the grouping: Chlamydia ICD9, Chlamydia ICD10, and Chlamydia SCT, all exist in the US NLM Value Set Authority Center (VSAC). 
The Chlamydia Union example demonstrates how a single Value Set using the HL7 Value Set Expression Syntax could be constructed using enumerated codes from multiple 
Code Systems, with each CodeBasedContent set unioned together. Both the Chlamydia Union definition and the Chlamydia Grouping definition generate the same Value Set Expansion Code Set.

### RoleClass-based Value Sets

The RoleClassAssignedEntity Value Set uses the RoleClass Code System. This example demonstrates two things:
1.	Both RoleClassAssignedEntity and RoleClassContact use an "intensional" definition style to identifying concepts to be included in the Expansion Code Set wherein a single 
code is provided along with a relationship traversal that clarifies that a transitive closure traversal is to be followed to find all codes related to the code provided. This 
is how "and all descendants" is communicated.
2.	RoleClassAssignedEntity unions together the "code and all descendants" noted above plus a reference to another value set - RoleClassContact.
