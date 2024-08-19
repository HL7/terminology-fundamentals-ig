
As described in the previous section, there are different syntaxes that may be used to define the content of a value set. The HL7 version 3 Model Interchange Format, Release 122 
is a complete and existing example of such a syntax used within HL7. This section enumerates this full set of Content Expression syntax functions that can be used to define a Content 
Expression based on the functions in the MIF standard. This format is used for all HL7 V3 Value Set Definitions and is how these Value Set Definitions are described in the thrice-annually 
released MIF document. This set of Value Set Definition Content Expression functions may not be the only HL7 syntax for defining a Content Logical Definition Expression, but it can be 
considered the default syntax that may be used for Content Expressions. 

Using this formalism, a Content Logical Definition that uses this HL7 Expression Syntax is composed of exactly one of the eight descendants listed in the Content Defining Element 
Types section below that specialize the abstract class Content Defining Element or one of its children. The HL7 CLD Expression UML model below depicts how the HL7 Expression Syntax 
can include ValueSetReference and CodeSystemElement that can be based on RelationshipBasedContent, CodeFilterContent that is either based on the code itself, or a code directly linked 
to the code, or a combination of these in CombinedContent.

Two of these, ValueSetReference and CombinedContent, are not expressly bound to a Code System because the internals of their definitions include such a binding. The remaining content 
defining classes are bound to a pair of classes that specify a Code System and are linked from CodeSystemElement.

A detailed set of interlinked textual examples using this HL7 Expression Syntax is provided as informative examples in the Appendix: Examples.

<figure>
    <img src="{{site.baseurl}}expressionsyntax.png"
         alt="HL7 Expression Syntax">
    <figcaption>Figure 5 – UML Class Model of the HL7 Value Set Definition Expression Syntax functions described in this section that may be used in a Content Expression.</figcaption>
</figure>

### Content Defining Element Types

The makeup of the Content Expression may be any one of the following six types of ContentDefiningElement:
1. CodeSystemElement:
    1. CodeBasedContent
    2. PropertyBasedContent
    3. RelationshipBasedContent
    4. CodeFilterContent
2. ValueSetReference
3. CombinedContent

There are four sub-types of CodeSystemElement, each of which use an aspect of the Code System noted to identify the concepts to be included in the Value Set Expansion Code Set.  

The first two, CodeBasedContent and PropertyBasedContent, may describe multiple codes (for CodeBasedContent,) or multiple properties (for PropertyBasedContent) within the single 
CodeBasedContent or PropertyBasedContent element. These multiple items are unioned together to define the Value Set Expansion Code Set.  

RelationshipBasedContent and CodeFilterContent can only include a single relationship (for RelationshipBasedContent) or code filter (for CodeFilterContent.)  

Combining more than one of the sub-types of CodeSystemElement or combining a ValueSetReference with another type (including another ValueSetReference) requires the use of 
CombiningContent to define how the various parts are to be combined (Union, Intersection, Exclusion) as described in CombinedContent section below.  

The structure and data elements of each of these types of Content Defining Element are described in detail below.  

#### CodeSystemElement

This element (or class) is a “parent class” to five of the types described – all except ValueSetReference and CombinedContent. Further, if this is present without any of 
its five subtypes (therefore only the mandatory reference to the DrawnFromCodeSystem, see below), then the Value Set Expansion Code Set will contain all codes from the specified Code System.

##### DrawnFromCodeSystem

Drawn from Code System is a mandatory collection of elements fully described in Source Code System Specification.

##### CodeBasedContentSet

Code Based Content Set is an aggregator that contains one or more Code Based Content elements. All Value Set Expansion Code Set members defined via individual codes or by direct subsumption are included via this element.

<table class="grid">
    <caption><b>CodeBasedContent - Element</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Code</td>
            <td>
                <p>specific Concept Representation</p>
            </td>
            <td>
                <p>Specifies a particular code to be used in the Value Set Expansion Code Set. It may be included on its own or it may define a header code for a set of codes based on specialization 
				relationships with other Concept Representations in the Code System that are to be included in the Value Set Expansion Code Set. Code may be an expression using a Code System that 
				supports the definition of concepts using expression grammar. In these situations it should be noted that the expression must define a single concept and not be an expression that 
				is in essence a query that can represent multiple concepts (i.e., the expression cannot include a subsumption parameter).</p>
            </td>
            <td>
                <p>This function requires a code anchor. Other types of relationships are handled in sections below for PropertyBasedContent and RelationshipBasedContent, so this is limited to the 
				generalization relationship (i.e., parent/child relationships).</p>
            </td>
            <td>ST</td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

###### IncludeRelatedCodes

The following set of elements specifies the functional behavior for the inclusion of codes in the Value Set Expansion Code Set based on relationships with the specified Code (sometimes referred to 
as a head code) defined in the Code System. This group repeats for each different relationship to be used.

<table class="grid">
    <caption><b>IncludeRelatedCodes - Elements</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>RelationshipName</td>
            <td>
                <p>word or set of words to describe the relationship used for traversal to find related codes.</p>
            </td>
            <td>
                <p>This is the name of relationship between concepts in the Code System that can be used to identify concepts for inclusion in the Value Set Expansion Code Set.</p>
            </td>
            <td>
                <p>When a Code System has a hierarchy that is not named, then</p>
                <p>
                </p>
                <p>RelationshipName is to be called “HIERARCHY”.</p>
                <p></p>
            </td>
            <td>ST</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>RelationshipTraversal</td>
            <td>identifies which codes related by the specified relationship should be included.&nbsp;</td>
            <td>
                <p>In a tree of codes of arbitrary depth for a particular relationship, this element identifies whether all codes walking the transitive closure of the 
				specified relationship (“TransitiveClosure”), only those codes with a direct first-level relationship to the selected code (“DirectRelationsOnly”) or 
				only those codes walking the transitive closure of the specified relationship where the code has no outbound relationship of the specified type (“TransitiveClosureLeaves”) should be included.</p>
            </td>
            <td>
                <p>The 3 defined values are an exhaustive list for this item.</p>
            </td>
            <td>
                <p>Constrained string (values “TransitiveClosure”, “DirectRelationsOnly” or</p>
                <p>“TransitiveClosureLeaves” permitted only)</p>
            </td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>IncludeHeadCode</td>
            <td>
                <p>indicates that the code is included in the content.</p>
            </td>
            <td>If false, only the concepts identified via the relationship traversal based on this code are included. The CodeBasedContent.code <i>is not included</i>.</td>
            <td>
                <p>The default value is TRUE. Note that if this is set to FALSE and if there are no additional codes to be included, then no codes will be included.</p>
            </td>
            <td>BL</td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

###### PropertyBasedContentSet

This type of Content Defining Element contains elements that identify content to be included based on Code System properties held (or not held) by concepts. e.g., “all lab observation 
codes that are designated as ‘orderable’”. There is only a single repetition permitted for this Content Defining Element specification type, but it may include multiple IncludeWithProperty 
elements that are combined via a logical AND to generate the Concept Representations included in the Value Set Expansion Code Set.

<table class="grid">
    <caption><b>PropertyBasedContentSet - Elements</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>IncludeWithProperty</td>
            <td>
                <p>indicates that codes with certain properties in the Code System are part of the Value Set Expansion Code Set.</p>
            </td>
            <td>
                <p>This optional repeating group of elements indicates that codes having properties in the Code System that match the specified value(s) should be considered part of the 
				content and included in the Value Set Expansion Code Set. Multiple IncludeWithProperty instances are combined using a logical AND. This means that only codes that have 
				properties that match <b>all </b>IncludeWithProperty instances are included in the Value Set Expansion Code Set.</p>
            </td>
            <td>
                <p><br></p>
                <p></p>
            </td>
            <td>COLL (listed following)</td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; Name</td>
            <td>
                <p>word or set of words to describe the concept property.</p>
            </td>
            <td>
                <p>This element specifies the moniker of the named concept property in the Code System.</p>
            </td>
            <td>
                <p>This is the name of the property as published by the Code System publisher.</p>
            </td>
            <td>
                <p>ST</p>
            </td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; Value</td>
            <td>
                <p>the value for which the property should be checked.</p>
            </td>
            <td>
                <p>The value that must be present in the name-value pair associated with the concepts to be included in the expansion code set.</p>
            </td>
            <td>
                <p>Either Value or Expression must be present. Note that for Code Systems that include properties without values, no value can be specified. In such a case matching 
				on the Name alone would result in inclusion.</p>
            </td>
            <td>ST</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; Expression</td>
            <td>a regular expression against which the property value should be evaluated.&nbsp;</td>
            <td>An expression that can be evaluated to determine a value that is to be found in the name-value pair associated with the concepts to be included in the expansion code set.</td>
            <td>Either Value or Expression must be present. Note that for Code Systems that include properties without values, no value can be specified. In such a case matching on the Name 
			alone would result in inclusion.</td>
            <td>ST</td>
            <td>0..1</td>
        </tr>
    </tbody>
</table>

#### RelationshipBasedContent

This type of Content Defining Element is an element that identifies content to be included based on relationships held (or not held) by concepts, e.g., “all concepts with a ‘finding site’ 
(RelationshipType) of ‘lung’ (TargetConcepts) AND ‘associated morphology’ (RelationshipType) of ‘inflammation’ (TargetConcepts)”.

<table class="grid">
    <caption><b>RelationshipBasedContentSet - Elements</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>RelationshipType</td>
            <td>
                <p>string uniquely identifying the relationship being used to filter the content. </p>
            </td>
            <td>
                <p>The string may be either a unique name or a unique identifier for the relationship type to be used.</p>
            </td>
            <td>
                <p>This is intended to uniquely identify the kind of relationship to be used in RelationshipBasedContent. The directionality of the relationship should also be clear, i.e., source and target.</p>
                <p></p>
            </td>
            <td>ST</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>TargetConcepts</td>
            <td>
                <p>an expression that defines the set of Concept Representations that are allowed targets of the named relationship.</p>
            </td>
            <td>
                <p>If present, this defines the allowed range of concepts for the named relationship.</p>
            </td>
            <td>
                <p>This may be specified in part as CodeBasedContent, PropertyBasedContent and/or CodeFilterContent. When more than one is used within the expression, the resulting Expansion 
				Code Sets for each collection are unioned together.</p>
            </td>
            <td>
                <p>COLL (relationship fulfilled by CodeSystemElement)</p>
            </td>
            <td>0..1</td>
        </tr>
    </tbody>
</table>

#### CodeFilterContent

This type of Content Defining Element is an element that identifies content to be included based on operations performed on the string value of codes, e.g., all codes starting with ‘A5’ 
or all codes ending with ‘B’. This content type has a single instance.

<table class="grid">
    <caption><b>CodeFilterContent - Elements</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ExpressionType</td>
            <td>name or description of the language in which the expression is rendered. </td>
            <td>
                <p>This element contains a string that specifies the name or short description of the language used to render the expression that is used to filter the codes in CodeFilterContent .</p>
            </td>
            <td>
                <p>The intent of this is to eventually become a constrained list that describes the syntax used to find the needed strings using a constant name for the syntax. 
				Given that a normative list of the string names is not known, for now an ST data type is used. A few known assumed entries are regexp<a href="#_bookmark129">23,
				</a> regexp_perl, regexp_sxp, regexp_PCRE, POSIX_BRE, POSIX_ERE and POSIX_SRE.</p>
            </td>
            <td>ST</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>Expression</td>
            <td>the string expression against which to evaluate the code symbols.&nbsp;</td>
            <td>This contains the string in the syntax of the language declared in the ExpressionType (above) that is used to process the codes (strings which are Concept Representations in the Code System).</td>
            <td></td>
            <td>ST</td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

#### ValueSetReference

This type of Content Defining Element contains elements that identify content to be included that is defined by another Value Set Definition. When multiple Value Set references are needed 
within the HL7 Expression, each is specified within a Combined Content.

<table class="grid">
    <caption><b>ValueSetReference&nbsp;- Elements</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ValueSetRefID</td>
            <td>
                <p>the unique identifier of the referenced Value Set Definition.</p>
            </td>
            <td>
                <p>This is the “Value Set Identifier” of the Referenced Value Set whose Value Set Expansion Code Set is being included by reference.</p>
            </td>
            <td></td>
            <td>
                <p>UID (OID, UUID, URI, or RUID)</p>
            </td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>Version</td>
            <td>a string that uniquely identifies the Value Set Definition Version.</td>
            <td>This string must uniquely identify the version within the context of the Value Set Definition. It is not intended to uniquely identify the version <i>independent </i>of the Value Set Identifier. In the context of a CLD, the Version Identifier is expected to either be a string match for a specific existing Value Set Version Identifier or support a date-query based on the approach noted in Usage Notes.</td>
            <td>
                <p>While many implementers may populate a Value Set Definition Version as a date, the choice of String as a datatype supports non-date strings that some organizations may want to use to disambiguate the ordinal and sequential nature of Value Set Definition Versions without requiring a full version history. It is also recognized that many implementations will want to use a date as input to a query to retrieve the most current active Value Set Definition at that date. While a date-type version identifier simplifies the approach to meeting that requirement, matching on the version string does not guarantee identifying the correct date-based retrieval. Instead, the best approach would be to compare the requested date provided in this version string to Value Set Definition Version <a href="#_bookmark61">Activity Status Date</a> to determine the most current active Value Set Definition Version as of the requested date.</p>
                <p>When no Value Set Definition Version is specified, the Value Set Definition Version is inferred from the context in which the Value Set Definition is used. When the Value Set is referenced in an HL7 binding, then the version that is used is derived from the date/time specified in the STATIC parameter of the binding.</p>
                <p>If the Value Set Definition is included as a Value Set Definition Reference Content Defining Element of another Value Set Definition, the version that is used is inherited from the containing Value Set Definition.</p>
                <p>If the Value Set Definition is being expanded in the context of a dynamic binding, then the date of the evaluation of the binding (and thus the codes to be used for that conformance evaluation) is used as the Value Set Definition Version date/time.</p>
                <p>If the Value Set Definition is not part of any binding but is being evaluated separately from its use, then the Value Set Definition Version is either the evaluation date/time or inherited from a containing Value Set Definition.</p>
                <p>
                </p>
                <p>In essence this means that a Referenced Value Set Definition with no specified version will “inherit” the closest transitively defined version-defining date. This means that a Referenced Value Set Definition with no version ID that is referenced by two different containing Value Set Definitions, each with a different Value Set Definition Version ID, will inherit the Version ID from the containing Value Set Definition (as the closest transitive source of version). This may result in different versions of the same Referenced Value Set Definition being used in each of the containing value sets.</p>
                <p><br></p>
            </td>
            <td>ST</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Name</td>
            <td>human readable string associated with the Referenced Value Set Definition.&nbsp;</td>
            <td>
                <p>For human display only and may be any of the names that are in the Name element of the Referenced Value Set Definition.</p>
            </td>
            <td></td>
            <td>ST</td>
            <td>0..1</td>
        </tr>
    </tbody>
</table>

#### CombinedContent

This type of Content Defining Element contains elements that identify content to be included based on set operations on additional Content Expressions. The evaluation of the 
operations is performed in order – first unions, then intersections and then exclusions. There may be an arbitrary number of these elements of any of the three kinds in this single content specification type.

<table class="grid">
    <caption><b>CombinedContent - Elements</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>UnionWithContent</td>
            <td>
                <p>identifies one or more Content Defining Elements such that content from any of them is considered to be part of the Content Defining Element.</p>
            </td>
            <td>
                <p>This is a recursive inclusion of any sub-type of ContentDefiningElement (see <a href="#_bookmark103">Content Defining Element Types</a>). It is intended to be additive to 
				the set of codes that will be generated in the Value Set Expansion Code Set.</p>
            </td>
            <td>
                <p>The first instance of CombinedContent MUST be a UnionWithContent. The ‘union’ implies inclusion with any other existing parts of this Content Defining Element specification.</p>
            </td>
            <td>
                <p>COLL of ContentDefiningElement (see <a href="#_bookmark103">Content Defining Element Types</a>)<br></p>
            </td>
            <td>1..*</td>
        </tr>
        <tr>
            <td>IntersectionWithContent</td>
            <td>
                <p>identifies Content Expressions that all concepts/codes must also match to be included.</p>
            </td>
            <td>
                <p>This operation permits a full Content Expression which produces a set of codes which must also be present with the codes that the other content inclusion operations produce (intersection operation).</p>
            </td>
            <td>
                <p><br></p>
                <p>This may be employed to enable the production of the final set of codes to be populated in the Value Set Expansion Code Set rather than making use of multiple complex sets of Code Based Content inclusions.</p>
            </td>
            <td>COLL of ContentDefiningElement (see <a href="https://www.htmltables.io/#_bookmark103">Content Defining Element Types</a>)</td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>ExcludeContent</td>
            <td>
                <p>identifies content that is explicitly excluded.</p>
            </td>
            <td>
                <p>Rather than specifying overly complex inclusion criteria, it is sometimes easier to implement a comprehensive inclusion Value Set Definition and then also a simply- defined 
				set of codes that should be removed from the comprehensive Value Set Definition before being populated into the Value Set Expansion Code Set. The Content Expression provides that capability.</p>
            </td>
            <td></td>
            <td>ContentDefiningElement (see <a href="#_bookmark103">Content Defining Element Types</a>)</td>
            <td>0..*</td>
        </tr>
    </tbody>
</table>

### Source Code System Specification

The first part of the Content Specification consists of a set of parameters that lay out a series of constraints relative to Code Systems and are applied when the expressions that 
reference codes in Code Systems are evaluated.  

Note that these parameters do not propagate across ValueSetReference instances.

<table class="grid">
    <caption><b>Source Code System&nbsp;- Elements</b></caption>
    <thead>
        <tr>
            <th>Element</th>
            <th>Definition</th>
            <th>Description</th>
            <th>Usage Notes</th>
            <th>Data Type</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>DrawnFromCodeSystem</td>
            <td>
                <p>group of elements identifying the Code System that applies for this portion of the Content Logical Definition.</p>
            </td>
            <td>
                <p>Many of the functions in the Content Expression refer to a specific Code System. This group is not needed if the Content Expression for this portion does not refer to any Code System. Note that this is a denormalization, as this information can be ascertained by processing the Content Expression; the information is replicated here for application convenience. There may be at most one of these sections for each Content Expression section and this represents the primary Code System providing any content based upon Code Systems for this value set.</p>
            </td>
            <td>
                <p><br></p>
            </td>
            <td>
                <p>COLL (listed following)</p>
            </td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; CodeSystem</td>
            <td>
                <p>formal registered machine-processable identifier of the Code System.&nbsp;<br></p>
            </td>
            <td>
                <p>This is the ID of the Code System rather than its published vernacular name.&nbsp;<br></p>
            </td>
            <td>
                <p>This is the same identifier form that is carried in the codeSystem component or property of the HL7 v2.x and ISO 21090 coded datatypes. It should be registered in the HL7 OID Registry.</p>
            </td>
            <td>
                <p>UID (OID, UUID, URI, or RUID)</p>
            </td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; VersionLockedDate</td>
            <td>
                <p>a dateTime that constrains the associated code system to the single published Code System version that is current as of that dateTime.</p>
            </td>
            <td>
                <p>When specified, this date constrains the content to the most recent Code System version available at the specified point in time.<br></p>
            </td>
            <td>
                <p>It is expected that either the VersionLockedDate or VersionLockedString will be populated in DrawnFromCodeSystem, <b>but not both </b>so there is no conflict. When specified, this element is intended to allow the computable unambiguous identification of a single Code System version. The VersionLockedDate approach <b>should only be used </b>when a VersionLockedString cannot accurately identify the desired version. The level of precision is expected to assure identification of a single unambiguous version. The Content Logical Definition element <a href="#_bookmark87">LockedDate</a> performs a similar, although global, function across the entire CLD <i>in situations where this element is <b>not </b>populated. </i>LockedDate <b>cannot </b>override this element.</p>
            </td>
            <td>TS.DATE</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; VersionLockedString</td>
            <td>
                <p>a string that constrains the associated Code System to the single published Code System version identified.</p>
            </td>
            <td>
                <p>This string is under the control of and is published by the Code System authority. When specified, it is expected to unambiguously identify the Code System at a particular published point.</p>
            </td>
            <td>
                <p>It is expected that either the VersionLockedDate or VersionLockedString will be populated in DrawnFromCodeSystem, <b>but not both </b>so there is no conflict. When specified, this element is intended to allow the computable unambiguous identification of a single Code System version. The level of precision is expected to assure identification of a single unambiguous version. The Content Logical Definition element <a href="#_bookmark87">LockedDate</a> performs a similar, although global, function across the entire CLD <i>in situations where this element is <b>not </b>populated. </i>LockedDate <b>cannot </b>override this element.</p>
            </td>
            <td>ST</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; DescriptiveName</td>
            <td>
                <p>human readable signifier for the Code System.</p>
            </td>
            <td>
                <p>This is a commonly understood name for the Code System and is used for human display purposes.</p>
            </td>
            <td></td>
            <td>ST&nbsp;</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; UsesCodeSystemPartition</td>
            <td>
                <p>identifies the partitions of the specified Code System that are included as part of the content.</p>
            </td>
            <td>
                <p>For those Code Systems that have separable partitions, this identifies a list of partitions that are included with the content.</p>
            </td>
            <td>
                <p>This is left unpopulated for Code Systems that do not have partitions identified by the Code System author/publisher. This should be a list of partition identifiers that must be used to correctly create a complete Value Set Expansion Code Set. If no partition(s) are listed, then the Value Set Expansion is based on all current partitions. For Value Set Definitions where conformance is a requirement, the Code System uses partitions and all current partitions may not be available to certifying agencies, the specific partitions used MUST be defined. Note that if the CLD is an Intensional definition on a Code System that has multiple partitions and this attribute is not valued, then there may be multiple valid Value Set Expansion Code Sets from the same Value Set Definition. Thus, the recommendation is to generally populate this when defining Value Sets on Code Systems that use partitions. See <a href="#_bookmark152">Code System Partitions and Supplements.</a></p>
            </td>
            <td>ST</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; UsesCodeSystemSupplement</td>
            <td>
                <p>identifies a collection of additional concept attributes for the Code System used as part of the Value Set Definition.</p>
            </td>
            <td>
                <p>Many Code Systems have supplements (see Section <a href="#_bookmark152">7.2.4</a>) published by the Code System author or by others. The functions defined in the Content Expression are permitted to refer to items that may be defined only within a supplement, as well as items defined within the base Code System, as long as the supplement(s) are listed in this element.</p>
            </td>
            <td>
                <p>An example of a supplement to the LOINC code system is pCLOCD, which defines additional properties for the concepts in LOINC (it extends the concept model) as well as additional concepts. See <a href="#_bookmark152">Code System Partitions and Supplements.</a></p>
            </td>
            <td>ST</td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>CodeSystemConstraintParameters</td>
            <td>
                <p>contains a set of constraints on the DrawnFromCodeSystem or on the Concept Representations in that Code System.</p>
            </td>
            <td>
                <p>If one of the parameters is present, it affects how the Concept Representations are used in the Value Set Expansion Code Set.</p>
            </td>
            <td></td>
            <td>
                <p>COLL (listed following)</p>
            </td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; AllowedRepresentation</td>
            <td>
                <p>identifies constraints on the Concept Representations to be populated in the Value Set Expansion Code Set when the Code System has multiple Concept Representations available.</p>
            </td>
            <td>
                <p>If present, the constraint restricts the Concept Representations to be included in the Value Set Expansion Code Set to the specified types (e.g., 2-character vs. 3-character vs. numeric, short names vs. long names, case-sensitive vs. case-insensitive, etc.). It is unused when the Code System specified has only a single Concept Representation available. If multiple Concept Representations exist and no constraints are specified, then all representations are to be included in the Value Set Expansion Code Set.</p>
            </td>
            <td></td>
            <td>ST</td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; AreBaseQualifiersUnlimited</td>
            <td>
                <p>indicates whether there are no constraints on qualifiers used in the types of Content Expressions.</p>
            </td>
            <td>This indicates that the expression created will include qualifiers that may include additional qualifiers that are not specified in the AllowedQualifiers element below.&nbsp;</td>
            <td>
                <p>If true, there are no constraints on qualifiers used in the types of Content Expressions. If false, only those qualifiers found in allowed qualifiers (<a href="#_bookmark146">7.2.3</a>) with an upper cardinality greater than 0 are permitted.</p>
            </td>
            <td>BL</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>AllowedQualifiers</td>
            <td>
                <p>specifies, through the identified constraints, a subset of allowed concepts based on matching the specified constraints.</p>
            </td>
            <td>
                <p>This is a group of elements which specify various constraints to the allowed associations (or concept qualifiers) in the base concepts that are selected by the Content Logical Definition.</p>
            </td>
            <td></td>
            <td>
                <p>COLL (listed following)</p>
            </td>
            <td>
                <p>0..*</p>
            </td>
        </tr>
        <tr>
            <td>&nbsp; &nbsp; RelationshipName</td>
            <td>
                <p>word or words to identify the type of relationship from the base concept to the qualifying concept.</p>
            </td>
            <td>
                <p>This element contains the name of types of relationships that are used for post-coordinated expressions based on relationships in the Code System.</p>
            </td>
            <td></td>
            <td>ST</td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

### Code System Partitions and Supplements

Code System Partitions are a unique and identifiable distinct segment of an overall Code System namespace. While most Code Systems are in essence one partition and, therefore, do not have 
identifiable partitions, some Code Systems can be made up of a collection of distinct segments. SNOMED CT is a prototypical example of such a Code System. The SNOMED CT International Edition 
is the base partition and can be used alone, but there are many distinct additional partitions that can be added to the international core to create what is known as “a SNOMED CT Edition”. 
Both the international core and an edition will have the same Code System Identifier (OID: 2.16.840.1.113883.6.96), but each unique edition can be distinguished by the partition identifiers 
used to create the edition. For SNOMED CT it seems likely that the “moduleID” can be used as the partition identifier. It should be noted that partitions can introduce new concepts and any 
other construct typical for a Code System to the resulting “complete” Code System.  
Code System Supplements contain information that may (and when useful for Value Set Definitions, do) contain additional attributes and properties that are associated with concepts. 
Code System Supplements cannot add additional concepts to a code system; they may only add attributes to existing concepts within the aligned Code System. In this way a Code System Supplement 
is differentiated from a Code System Partition, as a partition is effectively a segment of the aligned code system namespace and may add additional concepts to the Code System.  

Examples of a Code System Supplement include pCLOCD24 (mentioned previously), but can also be as simple as frequency counts that describe usage statistics for concepts in a particular context. 
Because this supplemental information can be directly tied to individual concepts, Code System Supplements can be used as part of a Value Set Definition Content Expression to determine Value Set 
Expansion Code Set membership. Code System Supplements must have some sort of identifying information so that they may be uniquely identified and accessed and must identify the Code System to which they are associated.
