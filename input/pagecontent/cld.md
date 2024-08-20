
The formal specification in the Value Set Definition of the Code System content that is to appear in the Value Set Expansion Code Set is 
called a Content Logical Definition (CLD.) In the initial publication for review of this specification, only one formalism for representing 
the CLD was described. Based on considerable feedback, this final publication of the specification allows the CLD to be specified in any usable 
way, including the original grammar now called HL7 Value Set Definition Expression Syntax. While this change increases the possibility of more 
than one standards-compliant way of representing a CLD, it provides flexibility to support existing formalisms for obtaining concepts/codes from 
Code Systems. This means that a specific Value Set Definition may use a CLD formalism that all users may not completely understand, but the intent 
is to expect designers of such formalisms, such as SNOMED International14, to publish descriptions of the formalism used so others may understand 
and compute the Value Set Expansion Code Sets defined. At a minimum, the HL7 Value Set Definition Expression Syntax serves as a “default” approach 
through which the key functions are described. This updated specification also separates out the “Non-computable Expression” type of CLD so that an 
expression that describes, but does not support formal computation of the Value Set Expansion Code Set is available for those that need it. This is 
meant to be easily identifiable as “non-computable” and, as such, a Value Set Definition that uses this in a CLD cannot mix together into one Value 
Set Definition Version both non-computable and formal syntax elements.  

The CLD consists of a single sub-type of Content Defining Element, which by nature may be recursive. Further, most sub-types of Content Defining Element 
refer to a specific Code System and to a set of constraint parameters relative to that Code System. In aggregate these comprise an expression that precisely 
specifies coded content to be generated into a Value Set Expansion Code Set.

### Content Logical Definition General Model

The Content Logical Definition describes how the Value Set Expansion Code Set shall be generated. The UML diagram in Figure 4 (below), illustrates that a 
CLD is a content expression that can use only a single syntax. This document describes a default expression syntax called “HL7 Value Set Definition Expression.”  

<figure>
    <img src="{{site.baseurl}}cld.png"
         alt="Content Logical Definition">
    <figcaption>Figure 4 - A Content Logical Definition is made up of a Content Expression (that can recursively contain other Content Expressions using the same grammar). 
	The Content Expression can be an “HL7 Expression” using the functions described in this specification, it can be some other syntax or it can be a textual 
	description of the process to be followed to obtain the correct concepts and, as such, is considered “non-computable”.</figcaption>
</figure>  

As is noted in the figure above and described in the caption, a CLD is expected to contain a formal specification of the set of Concept Representations to be retrieved 
from one or more Code Systems. A “syntax-based” formalism is expected to be computable, wherein a “Non- computable” expression is assumed to be a textual description 
and not directly computable. The default syntax for the CLD is HL7 Value Set Definition Expression Syntax. This set of expression functions is based on the HL7 Model 
Interchange Format15 that is described in detail in Section 7 as an illustrative enumeration of useful functions for obtaining concepts from a Code System. The three 
types of expressions noted in the figure are described in Section 6.2.4.

### Content Logical Definition – Elements

<table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Content Logical Definition – Elements</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>LockedDate</td>
            <td>the effective date that is used to determine the version of all referenced Code Systems and Value Set Definitions included in the Content Expression that are not already tied to a specific version. </td>
            <td>
                <p>A LockedDate provides the author the ability to restrict the Value Set Expansion Code Set content independent of Value Set use (e.g., as defined as part of HL7 v3 Binding Stability) by 
				fixing the Code System Versions needed to determine the Value Set Expansion Code Set to the most recent Code System Version as of the LockedDate (e.g., the Code System versions and Referenced 
				Value Set Definition versions in the CLD)<i>.</i></p>
                <p>If a LockedDate is present, this Value Set Definition version can only generate a Value Set Expansion Code Set that is defined by evaluating the Content Logical Definition against the 
				most recently available version of the Code System as of the LockedDate and the most recent Value Set Definition version as of that date for any Value Set Definitions included by reference. 
				If no LockedDate is provided, then this version of the Value Set Definition could produce different Value Set Expansion Code Set content with every new Code System version used and Value Set 
				Definition version referenced.</p>
                <p>When specified, "locking" is transitive to all referenced Value Set Definitions that are not already locked within the CLD, where in those cases the “inner” specified Code System version 
				takes precedence (e.g., the Code System Version used to determine the Value Set Expansion Code Set content of a CLD "clause" is governed by the Code System version specified "closest" to the 
				clause.) Therefore the Value Set Definition LockedDate may be overridden by a specific CLD Code System Version within the CLD.</p>
                <p>
                </p>
                <p>When a LockedDate is specified, the Value Set Definition Version is considered "Locked" for all uses. The Value Set Expansion Code Set provided by a Value Set Definition with LockedDate specified <b><i>will always be the one determined by the LockedDate</i></b><a href="#_bookmark89"><b><i>16</i></b>.</a> Otherwise, the Value Set Definition is considered to be "unlocked" and may have different Value Set Expansion Code Sets as underlying Code Systems and/or Value Set Definitions evolve.</p>
            </td>
            <td>
                <p><i>A LockedDate is best used when there is a need to lock all referenced Value Set Definitions that are included in the CLD to a specific Code System version</i>.</p>
                <p>If an author wishes to lock a small subset of concepts needed for the Value Set Definition to a specific Code System version (versus all referenced Value Set Definitions), the author should not use the LockedDate, and instead use the appropriate function in the CLD grammar chosen<a href="#_bookmark91">17</a> and make the “lock” occur <i>within the CLD clause grammar</i>. The LockedDate is used as the effective date to determine the most recent versions of all referenced Code Systems and referenced Value Set Definition versions as of that specified date. If a Code System version is defined on the LockedDate, that new version is the “most current version”.</p> Given that LockedDate affects the Value Set Expansion Code Set to be used in an implementation independent of the Binding Stability within a model binding, and that LockedDate supersedes the “Static Date” that can be used to define model binding stability, it is important for model binding to consider the CLD content and any included LockedDate.&nbsp;
            </td>
            <td>TS</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>ActiveOnly</td>
            <td>
                <p>include only ACTIVE Concept Representations in the Value Set Expansion Code Set</p>
            </td>
            <td>
                <p>This attribute flag indicates if “only active” Concept Representations should be included in the resulting Value Set Expansion Code Set when executing the CLD query. An active 
				Code System Version concept is identified by the “activity status” which is meant to indicate if the concept may be used for data collection and recording at the time the Code 
				System Version is the currently active Code System.</p>
            </td>
            <td>
                <p>The default is "FALSE" which means that <i>all concepts</i> that match the CLD in the Code System version used to determine the Value Set Expansion Code Set will be returned. 
				Any Code System concept attribute that represents activity status should be ignored if ActiveOnly = FALSE. If a Code System has no concept attribute that represents activity status, 
				then all concepts should be considered to have an activity status = “ACTIVE”. It is assumed that a concept activity status of “RETIRED” or “INACTIVE” represent a status that is 
				<b>NOT</b> ACTIVE. Note that a concept activity status of “DEPRECATED” is considered to have an activity status = “ACTIVE”. A “DEPRECATED” concept remains available for use, if 
				needed, but for one or more reasons it is recommended to avoid using that concept (particularly for new development). LockedDate dictates the use of a specific code system version 
				when creating an expansion, therefore any subsequent change in status for codes affected by (scoped by) the LockedDate will be ignored when creating the expansion. This means that 
				ActiveOnly will not remove codes effected by LockedDate, or either <a href="#_bookmark138">VersionLockedDate</a> or <a href="#_bookmark139">VersionLockedString</a> from 
				“<a href="#_bookmark98">An HL7 Value Set Definition Expression Syntax</a>”.</p>
            </td>
            <td>BL</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>CLDSyntaxReference</td>
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
                <p>The Content Expression syntax described in the <a href="#_bookmark98">An HL7 Value Set Definition Expression</a> <a href="#_bookmark98">Syntax</a> Section will use a URL that points to 
				the published version of this document.</p>
            </td>
            <td>UID</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Content Expression</td>
            <td>
                <p>how to identify a Value Set Expansion Code Set from identified Code Systems that falls within the meaning described in the <a href="#_bookmark38">Scope</a> element.</p>
            </td>
            <td>
                <p>If this is a non-computable expression, then the text should describe a method (or set of steps) that can be used to identify the concept representations to be included in the value set 
				expansion. If this is a computable expression, then the text should contain the complete expression needed, rendered using the syntax noted in <a href="#_bookmark92">CLDSyntaxReference.</a> 
				When evaluated based on an approach appropriate for the defined syntax, this should result in identifying a Value Set Expansion Code Set of Concept Representations (usually codes) from the 
				Code Systems identified within the expression.</p>
            </td>
            <td>Given that the entire expression used to determine the Value Set Expansion Code Set will be included in this element, the size should not be significantly restricted.</td>
            <td>ST</td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

#### Content Expression

The Content Expression holds the text (potentially combined with the LockedDate) that is used to determine what Concept Representations (codes) should be included in a Value Set Expansion Code Set. 
There is great value in making this text directly computable, which is supported by the CLDSyntaxReference element that identifies the expression syntax used by the Content Expression text. Based on 
comments received on the initial version of this document, this updated specification is purposefully open regarding how a Content Expression can be represented. Even so, there are two approaches to 
the information provided in the Content Expression: those that are computable and therefore are based on the use of a specific evaluable syntax (and therefore should have a CLDSyntaxDescription) and 
those that are not using a computable syntax, are non-computable and essentially contain textual guidance for how the codes to be included in the Value Set Expansion Code Set are to be identified. In 
the sections below the types are discussed further.  

In addition to the Default HL7 Expression Syntax just noted, other syntaxes may be used for a Content Expression. Support for “Other Syntax Expression” types means that any reasonable syntax can be 
used to computationally describe how to identify a specific set of Concept Representations (usually codes) from Code System(s). This is a change from the initial version of this specification where 
only the “HL7 Value Set Definition Expression Syntax” was supported.  

An incomplete list of Other Syntax examples that may be used includes:
* SNOMED CT Expression Constraint Language18
* OWL19
* SQL20
* Apelon Terminology Query Language (TQL)21

##### Syntax-based Content Expressions

As has been described elsewhere in the document, the intention of this specification is to support the computable determination of specified Concept Representations (codes) from Code Systems as 
delivered in Value Set Expansion Code Sets for use in data capture and exchange. To support ease of creation, maintenance and use, it is preferred that the Content Expression is directly computable. 
To do so, the syntax used to represent the “expression” used to compute the Value Set Expansion Code Set must be clearly specified and allow full use of the Code System (and additional data sources) 
to determine what codes are wanted. A complete set of syntax functions that may be used to fully specify a Content Expression is described in the An HL7 Value Set Definition Expression Syntax Section. 
This section should be considered a default HL7 Content Expression Syntax.

##### Non-computable Content Expression

Some descriptions of Code System content cannot be captured in a computable syntax. This can occur for a variety of reasons, such as when the needed codes are not identified using computable parameters 
(e.g., “the codes representing conditions currently under discussion in the US Public Health blog”) or when an initial version of the CLD is crafted as a general textual statement using “pseudo-code”. 
In this case the CLD can use text to capture the CLD mechanics. As noted before, if a CLD uses this approach, it cannot be combined with a formal computable syntax CLD, i.e., that version of the 
Value Set Definition will not support a normative directly-computable Value Set Expansion Code Set. Of course, a different version of the Value Set Definition could specify a CLD that uses a computable syntax.