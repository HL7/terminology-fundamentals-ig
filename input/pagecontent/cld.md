The formal specification in the Value Set Definition of the Code System content that is to appear in the Value Set Expansion Code Set is 
called a Content Logical Definition (CLD.) Previous specifications allowed only one formalism (the original grammar called the HL7 Value Set Definition Expression Syntax which can be referenced in 
<a href="https://www.hl7.org/implement/standards/product_brief.cfm?product_id=437">Characteristics of a Value Set Definition, Release 1</a>) for representing the CLD, however this version 
allows the CLD to be specified in any usable way. While this increases the possibility of more than one standards-compliant way to represent a CLD, 
it provides flexibility to support existing formalisms for obtaining Concept Codes from Code Systems. This means that a specific Value Set Definition may use a CLD formalism 
that all users may not completely understand, but the intent 
is to expect designers of such formalisms, such as <a href="https://www.snomed.org/">SNOMED International</a>, to publish descriptions of the formalism used so others may understand 
and compute the Value Set Expansion Code Sets defined. The HL7 Value Set Definition Expression Syntax serves as an example approach 
through which the key functions are described. This specification separates the “Non-computable Expression” as one that describes the expected Value Set Expansion Code Set from a 
CLD that can be computationally processed. This is 
meant to be easily identifiable as “non-computable” and, as such, a Value Set Definition that uses this in a CLD cannot mix together into one Value 
Set Definition Version both non-computable and formal syntax elements.  

### Content Logical Definition General Model

The Content Logical Definition describes how the Value Set Expansion Code Set shall be generated. The UML diagram in Figure 4 (below), illustrates that a 
CLD is a content expression that can use only a single syntax.

<figure>
    <img src="{{site.baseurl}}cld.png"
         alt="Content Logical Definition">
    <figcaption><b>Figure 4</b> A Content Logical Definition is made up of a Content Expression (that can recursively contain other Content Expressions using the same grammar). 
	The Content Expression can be a syntax or it can be a textual description of the process to be followed to obtain the correct Concepts and, as such, is considered “non-computable”.</figcaption>
</figure>  
<br>

A “syntax-based” formalism is expected to be computable, wherein a “Non-computable” expression is assumed to be a textual description 
and not directly computable. Th types of expressions noted in the figure are described in the section on <a href="#contentexpression">Content Expression</a>.

### Content Logical Definition – Elements

<table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Content Logical Definition – Elements</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td><a name="lockeddate"/>LockedDate</td>
            <td>the effective date that is used to determine the version of all referenced Code Systems and Value Set Definitions included in the Content Expression that are not already tied to a specific version. </td>
            <td>
                <p>A LockedDate is used to restrict the Value Set Expansion Code Set by fixing the Code System versions to the most recent as of the LockedDate.</p>
                <p>When specified, "locking" is transitive to all referenced Value Set Definitions that are not already locked within the CLD, where in those cases the “inner” specified Code System version 
				takes precedence (e.g., the Code System Version used to determine the Value Set Expansion Code Set content of a CLD "clause" is governed by the Code System version specified "closest" to the 
				clause.) Therefore the Value Set Definition LockedDate may be overridden by a specific CLD Code System Version within the CLD.</p>
                <p>When a LockedDate is specified, the Value Set Definition Version is considered "Locked" for all uses. The Value Set Expansion Code Set provided by a Value Set Definition with LockedDate
				specified <b><i>will always be the one determined by the LockedDate</i></b>. Otherwise, the Value Set Definition is considered to be "unlocked" 
				and may have different Value Set Expansion Code Sets as underlying Code Systems and/or Value Set Definitions evolve.</p>
				<p>Note: The use of LockedDate does not guarantee that expansion of a Value Set Definition in different environments (e.g., two different terminology services) will result in the same Value Set Expansion
				Code Set. For example, environment A contains SNOMED International Edition - v01.2025 while environment B contains SNOMED International Edition – v07.2025. A locked date set to August 1st of 2025 
				may be resolved, based upon environment default behavior, to the “most recently available version" <b>installed in the server performing the expansion</b>, which in this example, would be different in 
				environments A and B.</p>
            </td>
            <td>
                <p><i>A LockedDate is best used when there is a need to lock all referenced Value Set Definitions in the CLD to a specific Code System version</i>.</p>
				<p>If a LockedDate is present, this Value Set Definition version can only generate a Value Set Expansion Code Set that is defined by evaluating the Content Logical Definition against the 
				most recently available version of the Code System as of the LockedDate and the most recent Value Set Definition version as of that date for any Value Set Definitions included by reference. 
				If no LockedDate is provided, then this version of the Value Set Definition could produce different Value Set Expansion Code Set content with every new Code System version used and Value Set 
				Definition version referenced.</p>
                <p>If an author wishes to lock a small subset of Concepts needed for the Value Set Definition to a specific Code System version (versus all referenced Value Set Definitions), 
				the author should not use the LockedDate, and instead use the appropriate function in the CLD grammar chosen and make the “lock” occur 
				<i>within the CLD clause grammar</i>. The LockedDate is used as the effective date to determine the most recent versions of all referenced Code Systems and 
				referenced Value Set Definition versions as of that specified date. If a Code System version is defined on the LockedDate, that new version is the “most current version”.</p> 
				<p>It is important for model binding to consider the CLD content and any included LockedDate.</p>
            </td>
            <td><a href="https://hl7.org/fhir/datatypes.html#dateTime">dateTime</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>ActiveOnly</td>
            <td>
                <p>include only ACTIVE Concept Representations in the Value Set Expansion Code Set</p>
            </td>
            <td>
                <p>This attribute flag indicates if “only active” Concept Representations should be included in the resulting Value Set Expansion Code Set when executing the CLD query. An active 
				Code System Version Concept is identified by the “activity status” which is meant to indicate if the Concept may be used for data collection and recording at the time the Code 
				System Version is the currently active Code System.</p>
            </td>
            <td>
                <p>"FALSE" means that <i>all Concepts</i> that match the CLD in the Code System version used to determine the Value Set Expansion Code Set will be returned. "TRUE" means that only <i>active Concepts</i>  
				that match the CLD in the Code System version used to determine the Value Set Expansion Code Set will be returned.</p>
				<p>Any Code System Concept attribute that represents activity status should be ignored if ActiveOnly = FALSE. If a Code System has no Concept attribute that represents activity status, 
				then all Concepts should be considered to have an activity status = “ACTIVE”. It is assumed that a Concept activity status of “RETIRED” or “INACTIVE” represent a status that is 
				<b>NOT</b> ACTIVE. Note that a Concept activity status of “DEPRECATED” is considered to have an activity status = “ACTIVE”. A “DEPRECATED” Concept remains available for use, if 
				needed, but for one or more reasons it is recommended to avoid using that Concept (particularly for new development).</p>
				<p>LockedDate informs the use of a specific Code System version 
				when creating an expansion, therefore any subsequent change in status for Concept Codes affected by (scoped by) the LockedDate will be ignored when creating the expansion. This means that 
				ActiveOnly will not remove Concept Codes effected by LockedDate.</p>
            </td>
			<td><a href="https://hl7.org/fhir/datatypes.html#boolean">boolean</a></td>
            <td>1..1</td>
        </tr>
        <tr>
            <td><a name="cldsyntaxreference"/>CLDSyntaxReference</td>
            <td>
                <p>a link or identifiable name for the syntax used in the Content Logical Definition Content Expression.</p>
            </td>
            <td>
                <p>This refers to the syntax used in the Content Expression. If this element is null, then the Content Expression is non-computable.</p>
                <p>When populated, this element should provide a link that uniquely specifies the syntax used for the Content Logical Definition. When populated, at a minimum it should provide a unique 
				name that can be used to find documentation of the syntax. This element serves as both a pointer to the documentation and an identifier of the syntax.</p>
            </td>
            <td>
                <p>A URL is preferred. It is suggested that this element may be changed <b><i>without being considered a change in the CLD. </i></b>This means this element may change without triggering the 
				requirement for a Value Set Definition Version update.</p>
            </td>
            <td><a href="https://hl7.org/fhir/datatypes.html#uri">uri</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Content Expression</td>
            <td>
                <p>how to identify a Value Set Expansion Code Set from identified Code Systems that falls within the meaning described in the <a href="valuesetdefinition.html#scope">Scope</a> element.</p>
            </td>
            <td>
                <p>If this is a non-computable expression, then the text should describe a method (or set of steps) that can be used to identify the Concept Representations to be included in the Value Set 
				Expansion. If this is a computable expression, then the text should contain the complete expression needed, rendered using the syntax noted in <a href="#cldsyntaxreference">CLDSyntaxReference.</a> 
				When evaluated based on an approach appropriate for the defined syntax, this should result in identifying a Value Set Expansion Code Set of Concept Representations (usually Concept Codes) from the 
				Code Systems identified within the expression.</p>
            </td>
            <td>Given that the entire expression used to determine the Value Set Expansion Code Set will be included in this element, the size should not be significantly restricted.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

### Content Expression
<a name="contentexpression"/>
The Content Expression holds the text (potentially combined with the LockedDate) that is used to determine what Concept Representations (Concept Codes) should be included in a Value Set Expansion Code Set. 
There is great value in making this text directly computable, which is supported by the CLDSyntaxReference element that identifies the expression syntax used by the Content Expression text. There are two approaches to 
the information provided in the Content Expression: those that are computable and therefore are based on the use of a specific evaluable syntax or structure (and therefore should have a CLDSyntaxDescription) and 
those that are not using a computable syntax or structure, are non-computable and essentially contain textual guidance for how the Concept Codes to be included in the Value Set Expansion Code Set are to be identified. The types are discussed further in the sections below.  

#### Computable Content Expression

A Computable Content Expression is one that uses a syntax to describe the Concepts to be included in the Value Set Expansion Code Set. Computable Content Expressions may be syntax-based or structure-based. To support ease of creation, maintenance and use, it is preferred that the Content Expression is directly computable. Computable Content Expressions include those that are syntax-based and structure-based. 

##### Syntax-based Content Expression

The syntax used to represent the “expression” used to compute the Value Set Expansion Code Set must be clearly specified and allow full use of the Code System (and additional data sources) 
to determine what Concept Codes are wanted. A complete set of syntax functions that may be used to fully specify a Content Expression is described in <a href="https://www.hl7.org/implement/standards/product_brief.cfm?product_id=437">HL7 Specification: Characteristics of a Value Set Definition, Release 1</a> in the HL7 Value Set Definition Expression Syntax Section and is summarized later in this section. 

Syntax examples include but are not limited to:
* <a href="https://confluence.ihtsdotools.org/display/DOCECL">SNOMED CT Expression Constraint Language (ECL)</a>
* <a href="https://build.fhir.org/ig/FHIR/ig-guidance/vcl.html#valueset-compose-language-vcl">ValueSet Compose Language (VCL)</a>
* <a href="https://www.w3.org/OWL/">Web Ontology Language (OWL)</a>
* <a href="https://en.wikipedia.org/wiki/SQL">Structured Query Language (SQL)</a>
* <a href="https://apelon.com/dts-documentation/#dts-tql-doc">Apelon Terminology Query Language (TQL)</a>

###### HL7 Value Set Definition Expression Syntax Overview
This sections intends to summarize the types of functions covered by the HL7 Value Set Definition Expression Syntax. For the full specification, see the <a href="https://www.hl7.org/implement/standards/product_brief.cfm?product_id=437">HL7 Specification: Characteristics of a Value Set Definition, Release 1</a>. 

The HL7 Value Set Definition Expression Syntax is comprised of two main components; the Content Defining Element Types and the Source Code System Specification. 

The Content Defining Element Types describe what kinds of content can be included in a Value Set Expansion Code Set. They act as building blocks of the expression and use the elements described below:
1.	CodeSystemElement - uses Concept Representations (Concept Codes) directly from a source Code System; the types are described below:
    * CodeBasedContent – includes specific Concept Representations and/or their descendants.
    * PropertyBasedContent – includes Concept Representations based on properties held (or not held) by Concepts.
    * RelationshipBasedContent – includes Concept Representations based on relationships held (or not held) by Concepts (e.g., “finding site = lung”).
    * CodeFilterContent – includes Concept Representations based on operations performed on the string value of Concept Codes (e.g., Concept Codes starting with "A5").
2.	ValueSetReference – includes Concept Representations defined by another Value Set Definition.
3.	CombinedContent – applies set operations (union, intersection, exclusion) to combine multiple Content Expressions.

The Source Code System Specification defines where the Concept Representations come from and ensures unambiguous identification of the content. It uses the elements described below:
*	DrawnFromCodeSystem – specifies the Code System, its version (by date or string), and optionally partitions or supplements.
*	CodeSystemConstraintParameters – declares a set of constraints on the DrawnFromCodeSystem or on the Concept Representations in that Code System (e.g., include short vs. long name).
*	AllowedQualifiers – specifies constraints on which qualifiers may be used with a Concept Representation when post-coordinated expressions are created (e.g., only include "finding site" and its value).

In summary, Content Defining Elements describe what Concept Codes to include/exclude while the Source Code System Specification anchors those expressions to a precise Code System and version, ensuring that the included Concept Codes are drawn consistently and reproducibly. Together, they allow a Value Set Definition combine logic (which Concept Codes, relationships, properties) with provenance (which system/version), producing a computable, reliable Value Set Expansion Code Set.

##### Structure-based Content Expression
Computable Content Expressions may also be structure-based. An example of this is the FHIR valueSet.compose element and its sub-elements. The structure of the <a href="https://hl7.org/fhir/valueset-definitions.html#ValueSet.compose">ValueSet.compose</a> decribes which Concepts are included or excluded from the Value Set Expansion Code Set. ValueSet.compose implements a syntax-based Content Expression and does so as a structured model rather than a text-based syntax.

To illustrate the differences between a syntax-based and structure-based computable expression, the following example of including all descendants of a SNOMED CT concept is provided in both formats below. 

SNOMED CT ECL (system is assumed to be SNOMED CT as the language is specific to SNOMED CT content):
```
< 404684003
```

FHIR ValueSet.compose:
```
"compose": {
  "include": [
    {
      "system": "http://snomed.info/sct",
      "filter": [
        {
          "property": "concept",
          "op": "is-a",
          "value": "404684003"
        }
      ]
    }
  ]
}
```

#### Non-computable Content Expression

Some descriptions of Code System content cannot be captured in a computable syntax. This can occur for a variety of reasons, such as when the needed Concept Codes are not identified using computable parameters 
or when an initial version of the CLD is crafted as a general textual statement using “pseudo-code”. 
In this case the CLD can be defined using text to capture the CLD intent. As noted before, if a CLD uses this approach, it cannot be combined with a computable syntax CLD, i.e., that version of the 
Value Set Definition will not support a directly-computable Value Set Expansion Code Set. Of course, a different version of the Value Set Definition could specify a CLD that uses a computable syntax.