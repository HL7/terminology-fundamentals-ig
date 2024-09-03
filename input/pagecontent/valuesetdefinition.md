Value Sets represent the terminology constraint for a data element in a model for a particular use case and, thus, strongly influence the semantics that may be carried in the model. 
As such, they are usually authored and published using well-controlled processes to ensure quality and consistency. In order for such quality oversight and robust governance 
operations to be implemented efficiently, a well-designed standard for the content and structure for Value Sets is highly desirable. This standard supplies such a definition 
and many of the elements described in the next sections are specifically included to support robust governance processes.

### Value Set Architecture

#### General Overview

When most people think of a Value Set, they think of a list of codes or phrases. These lists may be called member list, code list, etc. While a critical part of the usefulness of a 
Value Set, the final set of Code System members used by implementers, which is called the Value Set Expansion in this specification, is only one part of the collective information 
that _is a Value Set_.  

A Value Set is a specification composed of general metadata that is true for all versions of the Value Set8 and version-specific information that describes the content of the 
Value Set9. Some of the information conveyed in the specification is not intended to be machine computable, but carries information users may interpret. Other elements in the 
specification are intended to be directly computable so that automated systems may act upon this information and exhibit reliable behavior.  

Also included are critical metadata used to identify the people and entities that are responsible for developing and maintaining the Value Set Definition, Value Set Definition 
versioning information and elements that can support tracking of changes to the Value Set and authoring workflow, and other key provenance information.  

Each of the elements of the model is described in the sections below.

#### Relationship Between the Value Set Definition and Value Set Expansion Code Set

The phrase "Value Set" usually is taken to mean both of the following:

*   **Value Set Definition**, a description of the set of Concept Representations (usually codes) that are intended for use, **plus** the
*   **Value Set Expansion Code Set**, the set of resulting codes actually obtained for a particular use, drawn from one or more specific Code System versions.

Yet as is shown in this specification and in Core Principles, these are not exactly the same thing. In general, when the phrase “Value Set” is used (including within this specification), 
the intent is to reference both the Value Set Definition and the Value Set Expansion Code Set as one, in that the distinction is immaterial for the point being made. From this point 
forward in this document one of the more specific phrases is used when one or the other item is under discussion in particular and the difference is important to note.  

A Value Set Definition is a set of metadata that describes the scope of the intended member Concept Representations, provenance of the included information and, most importantly, a set 
of instructions that describe (preferably in a computable manner) which Code System Concept Representation, which is almost always a code, should be in the Value Set Expansion Code Set. 
As such, the Value Set Definition is then applied to one or more Code System instances to determine the Value Set Expansion Code Set Member Concept Representations. In essence the Value 
Set Definition (specifically the Content Logical Definition described below) is a set of functions against the Code System to retrieve the concepts as described in the definition. This 
is true for every Value Set Definition. It is not restricted to only definitions that use a logical or “intensional” definition; it is also true for simple explicit lists of individually 
selected concepts (“extensional.”) As long as the Value Set Definition is not locked to a single Code System version, even simple code lists can result in changing Value Set Expansion Code 
Sets if the codes in the original definition are retired in later Code System versions. In summary, only a Value Set Expansion Code Set (see Figure 1 below and also the <a href="vsexpansion.html">Value Set Expansion</a> page) will contain 
the accurate Expansion Code Set Member Concept Representations that are the result of the proper Value Set Definition version applied against the proper Code System version.

#### Alignment with Intensional and Extensional

There are two approaches to defining Value Sets (think of these as “types” of a value set definition), Intensional and Extensional, repeated in part here for clarity:

*   _Extensional Definition_: Explicitly enumerating each of the Value Set concepts.
*   _Extensional Definition_: Explicitly enumerating each of the Value Set concepts.

Both approaches are used frequently in defining Value Sets but intensional definitions may use text that is not directly computable and therefore requires human interpretation to 
determine a reliable set of concepts that make up the actual Value Set Expansion Code Set.

The <a href="cld.html">Content Logical Definition</a> page of this document describes how to represent a computable description of the Concept Representations that are intended to be in the Value Set 
Expansion Code Set. It is through the use of functions included in the Content Logical Definition that any and all concepts included in a Value Set Expansion Code Set will be identified. 
The difference between Intensional and Extensional is a description of the style used to determine the Value Set Expansion Code Set.  

In an Extensional style Value Set if the Value Set Expansion is allowed to change with new Code System versions (i.e., is not LOCKED to a single Code System version), then new concepts 
will not automatically be added to the Value Set Expansion Code Set because each concept is explicitly identified, but concepts may fall out of the Value Set Expansion Code Set if they 
are retired. In an Intensional style Value Set the Content Logical Definition contains a logical expression that is to be evaluated against each allowed Code System version and that 
evaluation can result in both the addition and removal of concepts from the Value Set Expansion Code Set.

<figure>
    <img src="{{site.baseurl}}vstypes.png"
         alt="Value Set Definition Types and Expansions">
    <figcaption><b>Figure 1</b> Value Set Definition types and resulting Expansions illustrates how a value set expansion may change over time whether its value set definition is written intensionally or extensionally.</figcaption>
</figure>

#### Class Model Diagram

<figure>
    <img src="{{site.baseurl}}vsdmodel.png"
         alt="Value Set Metadata">
    <figcaption><b>Figure 2</b> Value Set Metadata</figcaption>
</figure>

### Elements

The Value Set Definition consists of a collection of Elements, which contain the specification and documentation of the Value Set. The Value Set Expansion Code Set can be generated from 
these elements and the documentation elements support governance and distribution. Any element with an unstated cardinality is presumed to have a cardinality of 0..\*. All elements with 
a non-zero lower cardinality are required.

Each of the following sections is structured to align with the UML Model categories noted in the diagram above. Each of the primary sections below are sub-divided to indicate if the 
element described is definitional or non-definitional, where definitional elements, when changed, must result in either an entirely new Value Set (for the Value Set Elements) or a new 
Value Set version (for Value Set Version Elements). Elements that are derived from other elements are also identified. Each section below describes the details of the components 
illustrated in Figure 2 - Value Set Metadata.

#### Implied Constraints of “Definitional” and “Non-definitional” Elements

The class diagram includes “definitional” and “non-definitional” categorization of model elements. By this we mean that when elements in a class that are “definitional” are changed 
in a substantive way, the model expects that a new instance of the class should be created.  

For all elements, except those that are an ST datatype, any change is potentially substantive. For the Scope content, which is a text string, a substantive change is subjective and 
described more completely in the <a href="#scope">Scope</a> section. The definitional elements impose baseline process expectations in the Standard, i.e., all compliant implementations of the Standard must 
create new Value Set Definitions or new Value Set Definition versions when a definitional element has a substantive change. A new Value Set Definition or Value Set Definition version 
that is based on a change in a non-definitional element is not considered best practice but may occur in certain business scenarios.

#### Value Set Definition

Elements described in this section provide identification and descriptive information about the entire Value Set Definition and can be consistently applied to all versions of the 
Value Set Definition. This collection of elements is made up of an identifier and two categories of model elements: definitional and non-definitional. These categories are described in Implied Constraints above.  

<table class="grid">
	<tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Value Set Identifier</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Value Set Identifier</td>
            <td>globally unique string identifying this value set</td>
            <td>The string must be globally unique, is expected to be a permanent canonical identifier for all versions and associated instances, and is used to reference the value set
			in a specification, model, design or an instance.</td>
            <td>Current implementations at HL7 use <a href="https://www.hl7.org/fhir/datatypes.html#uri">URIs</a> or <a href="https://www.hl7.org/fhir/datatypes.html#oid">OIDs</a> (a subtype of URI). 
			Identifiers can have attributes, such as "preferred" or "authoritative".</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#uri">uri</a></td>
            <td>1..*</td>
        </tr>
    </tbody>
  </table>
  <table class="grid">
	<tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Value Set Definition— Definitional Elements<br><br>If the elements within this section changes substantively, then a new Value Set Definition <b>must</b> be created and a new Value Set Identifier assigned.</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td><a name="scope"/>Scope</td>
            <td>textual description of the span of meanings for concepts to be included within the Value Set Expansion Code Set including the intended use and limitations of the Value Set.</td>
            <td>This is intended to convey between humans (and not necessarily in a computable fashion) the scope of Concept Representation meanings and capture important elements of the context 
			of use for the Value Set. The scope should describe “the semantic space” the Value Set Expansion is intended to cover. This can also describe the approach taken to build the Value Set
			Expansion Code Set. Any substantive change is one that changes the meaning of the scope and therefore implies a different Value Set Definition rather than a new Value Set Definition Version.
			This item is a key component for the meaning of the Value Set.</td>
            <td>The Scope should cover the following kinds of information:
			<ul>
				<li>Focus: The general focus of the Value Set as it relates to the intended semantic space. This can be the information about clinical relevancy or the statement about the general focus of the Value Set, such as a description of types of messages, payment options, geographic locations, etc.</li>
				<li>Model Context: A statement that describes how this Value Set is to be used in an artifact.</li>
				<li>Inclusion Criteria: Criteria describing what concepts or codes should be included and why.</li>
				<li>Exclusion Criteria: Criteria describing what concepts or codes should be excluded and why.</li>
			</ul>
			As noted above, the scope text is intended to be non-computable, therefore 
			determining a substantive change is solely the responsibility of the Value Set steward/author/reviewer community. The expectation is that the original intent of the Value Set 
			should be held unalterable.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>Immutable</td>
            <td>property indicating that no change to the Content Logical Definition may occur. Immutable means no change can occur.</td>
            <td>If this is set to ‘true’, then no new versions of the Content Logical Definition can be created. Other metadata might still change and it is possible that the Value Set Expansion Code Set can change if the underlying Code Systems change and the Content Logical Definition (CLD) is not locked to a specific Code System version.</td>
            <td>
                <p>The default value is FALSE. Note that the implication is that if this is set to ‘true’, thereafter, the current Value Set Definition version must be the last Value Set Definition allowed. The Immutable Flag tends to be set to ‘TRUE’ in one of two cases:</p>
                <ul>
					<li>Where the Value Set Definition, by the nature of its usage, cannot change (e.g., "all specializations of ACT in ActClassCode")</li>
					<li>Where there's no safe way to express the "Scope" such that someone else could safely make changes to the Value Set Definition.</li>
				</ul>
                <p>Source workflow control must guarantee that the same URI always yields the same definition.</p>
            </td>
            <td><a href="https://hl7.org/fhir/datatypes.html#boolean">boolean</a></td>
            <td>1..1</td>
        </tr>
    </tbody>
  </table>
  
  <table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Value Set Definition— Non-definitional Elements<br><br>The content of the elements in this section may change without requiring a new Value Set Definition be created.</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Value Set Definition Naming</td>
            <td>
                <p>human-readable monikers of this Value Set Definition.</p>
            </td>
            <td>This repeating group of elements contains information about the human- readable strings associated with this Value Set Definition that are used as names.</td>
            <td></td>
            <td>COLL (listed following)</td>
            <td>1..*</td>
        </tr>
        <tr>
            <td>&nbsp;&nbsp;&nbsp;Name (sub-element)</td>
            <td>word or set of words by which the Value Set is known, addressed or referenced</td>
            <td>This name is intended to be human readable, short and as specific as possible and it should relate to the content and intent. It is considered to be the name of the Value Set Definition.</td>
            <td>This need not be unique. Some use cases may require uniqueness within a namespace and, therefore, best practice is to make the name unique.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>&nbsp;&nbsp;&nbsp;Name Language (sub-element)</td>
            <td>code to indicate the system of communication used by a particular country or community in which the name is represented.</td>
            <td>This indicates the language system (e.g., US English) in which the name is expressed.</td>
            <td>The intention is to use the IETF language tags preference referenced by the current RFC for BCP 47 (add reference).</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a> (drawn from IETF language tags noted)</td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>&nbsp;&nbsp;&nbsp;Preferred Name Indicator (sub-element)</td>
            <td>identifies the single preferred name for the “Name Language”.</td>
            <td>Flag that this <i>Name </i>in this <i>Name Language </i>is the preferred human-readable signifier in this language. The only permissible value of this property is “preferred”.</td>
            <td>There may be multiple human readable names in a given language, and this flag indicates which of them is preferred for the given language. The expectation is that only one is 
			preferred for any given language.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1 (within each Value Set Naming group of elements)</td>
        </tr>
        <tr>
            <td>Definition URL</td>
            <td>
                <p>a web pointer to where the Value Set Definition may be located.</p>
            </td>
            <td>Pointer to the authoritative accessible, persisted source of truth of the entire Value Set Definition, including textual information and available versions.</td>
            <td>If provided, the URL should be and remain (through redirection if applicable) resolvable.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#url">url</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Intellectual Property Information</td>
            <td>publishing restrictions for the Value Set Definition metadata</td>
            <td>These are generally legal restrictions on the use and publishing of the Value Set Expansion and metadata.</td>
            <td>This is intended to convey the restrictions, such as copyright, of the directly referenced Value Set Definition and Expansion, including Code System(s). It should also 
			contain contact information. It is a text block of unlimited length and unspecified internal format although markdown is recommended so that specific information types, such as contact, are identified.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Experimental</td>
            <td>this Value Set is created for educational or testing purposes and is not intended for production use.</td>
            <td>When set to ‘experimental’, this Value Set should not be used in a production system or environment and may be used for exemplary purposes. It must be noted that use
			of a Value Set Definition designated as Experimental is under the control of the user and is not meant to be controlled by this element. If not populated, the Value Set 
			may be used in a production system or environment. This decision is wholly the judgment of the Value Set steward.</td>
            <td>When absent, the Value Set may be used for any purpose. Value Sets noted to be Experimental may also be used for demonstration purposes.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Source Reference</td>
            <td>reference to prior work used as a basis in authoring of this Value Set</td>
            <td>This text is intended to act as a citation to work done elsewhere that is not part of the current stewarding process where the referenced source is in some way
			a basis of the current Value Set Definition.</td>
            <td>This may refer to other Value Set Definitions, research articles, or other resources. This is not intended to document uses of the Value Set Definition, 
			for this, see Section 5.2.2.3.7 below. For example, the identifier for a Value Set Definition that was cloned to begin the work on this 
			Value Set Definition, or a pointer to a published article that describes appropriate concepts. There may be multiple source references.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>Keyword</td>
            <td>a word or phrase that captures a key aspect of a Value Set Definition</td>
            <td>
                <p>Word or words that may be used in an information retrieval system to index the contents of the Value Set Definition. The string datatype allows implementers to use strings or coded concepts.</p>
            </td>
            <td>
                <p>This may be used to surface indexing terms for a search.</p>
            </td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>Use</td>
            <td>the manner in which the Value Set Definition will be employed or applied.</td>
            <td>an optional repeating element used to capture information about consumers of the Value Set Definition and the implementations, projects or standards where the author has utilized the Value Set.</td>
            <td>
                <p>The information captured in “Use” can and should include names of programs and/or names of organizational entities that use the value set definitions, including standards that 
				require the value set definition. This is likely to be a “point in</p>
                <p>time” view and should not be considered an authoritative listing of all uses of the Value Set. In the USA, the Value Set Expansions created for electronic quality measures 
				(eCQMs) that are a part of the Meaningful Use requirements could implement this as follows:</p>
                <ul>
					<li>User: Measure Steward name; Usage: Measure Identifier & version/Name</li>
					<li>User: Centers for Medicare & Medicaid Services (CMS); Usage: eCQM release identifier.</li>
			</ul>
            </td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..*</td>
        </tr>
    </tbody>
</table>

#### Value Set Definition Version

The Value Set Definition Version section contains the information required to computationally produce a Value Set Expansion from the Value Set Definition, metadata specific to the 
version and an identifier for the Value Set Definition Version. Similar to the overall Value Set Definition, the Value Set Definition version metadata includes an identifier, elements 
characterized as definitional, elements characterized as non- definitional (both are described in Implied Constraints) and a derived element. Each of the elements in this section applies 
to a particular version of a Value Set Definition.

<table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Value Set Definition Version Identifier</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Value Set Definition Version Identifier</td>
            <td>a unique string labeling a Value Set Definition Version.</td>
            <td>A unique identifier within the context of the Value Set Definition that is used to indicate a specific Value Set Definition at a point in time.</td>
            <td>The identifier must be updated when any of the "Definitional metadata elements" of the Value Set Definition have changed. In addition, it may be updated under other circumstances. This may be a string identifier of any type or may explicitly be a timestamp, which is often used to simplify dynamic binding processing. If the string is intended to be encoded as a timestamp consistent with HL7 Datatypes R2, the format should be TS.DATETIME.FULL.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

<table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Value Set Definition Version — Definitional Elements<br><br>If either of the elements within this section changes in any way, then a new Value Set Definition Version must be created with a new Value Set Version Identifier assigned but the 
		Value Set Identifier does not change.</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>
                <p>Content Logical Definition</p>
            </td>
            <td>
                <p>formal representation used to determine the coded concept contents to be included in the Value Set Expansion Code Set</p>
            </td>
            <td>
                <p>The Content Logical Definition (CLD) is a formal representation of Value Set content and is intended to be machine processable. It is used to generate the coded 
				content of the Value Set Expansion, i.e., the Value Set Expansion Code Set.</p>
            </td>
            <td>
                <p>This element uses the ED data type (REFERENCE ED) meaning that the content is structured and that the structure includes an identification of the 
				structure (or the application that must be used to interpret the data). For example, an “HL7 Expression” uses a MIME type of “application/xml”. This flexibility means
				that subsequent specifications can identify the allowance for additional expression syntaxes.</p>
                <p>The HL7 Expression functions are an available syntax for the CLD that is described below, possibly including some recursive elements. Each recursive section is 
				considered a “clause”. The Value Set Definition Version contains a single mandatory Content Logical Definition that describes different types of specifications of 
				content, some of which contain or reference Content Logical Definitions; thus the definition is inherently recursive. The list of functions is described in Section 6.</p>
                <p>If a content logical definition content expression contains Concept Representations that can change yet are still considered a representation of the same concept, 
				then the value set version may change due to a Code System Version change alone.</p>
            </td>
            <td>ED (???)</td>
            <td>1..1</td>
        </tr>
    </tbody>
</table>

<table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Value Set Definition Version — Non-definitional Elements<br><br>The elements within this section may change without requiring that a new Value Set Definition Version be created. Some elements in this section should never result in a new version (e.g., 
		Activity Status, Effective Date, Workflow Status Description, Completeness), but a change in others could lead a Value Set steward to decide to identify a new version (e.g., Steward, Author, etc.).</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Activity Status</td>
            <td>
                <p>the release and/or usability state</p>
            </td>
            <td>
                <p>The state that represents the current state of the Value Set Definition in the context of the Value Set creation and release process.</p>
            </td>
            <td>
                <p>The Activity Status should track the status with regards to the Value Sets availability for use in a publishing environment context. Changes to this element should never result in a new Value 
				Set Definition Version.</p>
                <p>This element has the following allowed values:</p>
                <ul>
					<li>Preliminary: State during which time the Value Set Definition version is being drafted and is not available for use. The element Workflow Status Descripition will carry additional information regarding pre-Active state.</li>
					<li>Active: State during which the Value Set Definition version is available for use. The Activity Status Date associated with this status is known as the “Effective Date”.</li>
					<li>Inactive: State indicating that the Value Set Definition version is no longer available for use in creating new content. The Activity Status Date associated with this status is known as the “Expiration Date”.</li>
					<li>Deleted: State intended to be used to remove a Value Set Definition from use and view in a repository and is only possible if the Value Set was never Active (i.e., can only transition from Preliminary).</li>
				</ul>
                <p>Since activity status is only represented here in Value Set Definition Version information and is a required element, then any Value Set Definition that does not have this is <i>not valid. </i>Furthermore, 
				a Value Set Definition may have more than one Value Set Definition Version with any of the status states noted. Given that this can lead to overlapping Active definitions, external governance must be available
				to either restrict the allowed overlap or resolve overlap if usage does not specify a particular Value Set Definition Version.</p>
                <p><figure>
					<img src="{{site.baseurl}}activitystatus.png"
						alt="Activity Status Workflow"
						style="width: 100%;">
					<figcaption><b>Figure 3</b> Valid state transitions for Value Set Activity Status</figcaption>
					</figure></p>
            </td>
            <td>CS ???</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>Activity Status Date</td>
            <td>
                <p>the date when the associated Value Set Definition Version activity status is in effect.</p>
            </td>
            <td>This is the date the associated status for this version began.</td>
            <td>
                <p>When the Activity Status is set to “Active”, the Activity Status Date defines the Effective Date which is the date-time the Value Set Definition Version becomes active.</p>
                <p>When the Activity Status is set to “Inactive”, the Activity Status Date is the date-time when the Value Set Definition version becomes Inactive. This cycle may happen multiple times.
				The specified time is expected to be one second after midnight UTC of the Activity Status Date. The date may be in the future.</p>
                <p>It is <i>strongly encouraged </i>that the Activity Status be set such that <b>no more than one Value Set Definition Version for a single Value Set Identifier can have an Activity 
				Status of ACTIVE at the same time within a single realm</b>. In cases where this is not true, evaluation of the alignment of a Value Set Expansion Code Set to a specific Value Set 
				Definition, as referenced in a CD, will be problematic.</p>
                <p>Changes to this element should never result in a new Value Set Definition Version.</p>
            </td>
            <td>TS (<a href="https://www.hl7.org/fhir/datatypes.html#date">date</a> or <a href="https://www.hl7.org/fhir/datatypes.html#dateTime">dateTime</a>???)</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>Workflow Status Description</td>
            <td>
                <p>the state of development of the Value Set Definition while in a single Activity Status.</p>
            </td>
            <td>
                <p>Workflow Status Description is used to represent details of the Value Set Definition development process. The development of a Value Set Definition often follows a formal workflow process from 
				initiation to completion and this element carries the state variable for this state machine. The assumption is that when first created, a Value Set Definition would have a workflow state of Draft. 
				Additional workflow states may be used.</p>
            </td>
            <td>
                <p>The values that are traditionally used for this element while the Value Set Definition has an Activity Status of Preliminary are assumed to include phrases that capture various stages in review and 
				approval. It is expected that this would be used to manage maintenance activities, but that a terminology service would not be expected to expose this information. Different services might adopt different
				workflow status description values reflecting their local practices.</p>
                <p><u>As an example</u>, the US Value Set Authority Center (VSAC) uses the following workflow status descriptions. The Activity Status is “Preliminary” (see Activity Status) for all these workflow status descriptions:</p>
                <ul>
					<li>“Draft” – The initial Value Set Definition creation status. An author can make changes to the Value Set Definition only while the definition is in this status.</li>
					<li>“Proposed” – Once an author has completed editing, the Value Set Definition is submitted for review by a Value Set steward. The submission changes the Value Set Definition to this status and editing 
					can no longer occur.</li>
					<li>“Approved” – When the Steward completes the review and approves the Value Set Definition. This status is for Value Set Definitions that have successfully completed a review process but are not yet 
					set to be published.</li>
					<li>“Ready to Publish” – This status occurs when the steward sets a Publication Date that defines when the Value Set Definition version is to become ACTIVE (Activity Status = ACTIVE). The VSAC Value Set 
					Definition version is in this status from the time the publication date is set until the publication time. VSAC Value Set Definition versions are published at 00:01 (one minute after midnight) of the 
					publish date morning (Eastern Time) and the earliest a Value Set Definition version can be published is the next day’s morning.</li>
				</ul>
                <p>VSAC allows all Value Set Definition workflow status descriptions to be changed back to the prior status as long as the Value Set Definition has not been “Published” (Activity Status = ACTIVE).</p>
                <p>A Value Set Definition version can only have one workflow status description at any time. There may be additional states defined by different developers. This is an optional element because the</p>
                <p>use of Activity Status “Preliminary” may be sufficient for some implementations. Changes to this element should never result in a new Value Set Definition version.</p>
            </td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Steward</td>
            <td>the entity that is responsible for the content of the Value Set Definition.</td>
            <td>
                <p>This is a textual description of the organizational entity responsible for the content and maintenance.</p>
            </td>
            <td>The information included should include contact information.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>
                <p>1..1</p>
            </td>
        </tr>
        <tr>
            <td>Author</td>
            <td>
                <p>the entity or set of entities that create and may modify the Value Set Definition content.</p>
            </td>
            <td>
                <p>The name of a group or an individual.</p>
            </td>
            <td>
                <p>This can be any combination of groups or individuals. When known and actively maintained, this should be populated. The information included about the Author may include contact information.</p>
            </td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>Comments</td>
            <td>human-specified notes and other documentation</td>
            <td>This optional repeating group of elements contains human-specified notes and other documentation, which consists of a time-stamped list of comments text blocks.</td>
            <td>
                <p>Changes to this element should never result in a new Value Set Definition Version.</p>
            </td>
            <td>COLL (listed following)</td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>&nbsp;&nbsp;&nbsp;CommentString (sub-element)</td>
            <td>unrestricted field of remarks or other text.</td>
            <td>Each comment is an entry of arbitrary length that is only editable by those in the author group.</td>
            <td>This element is expected to primarily used by authors of Value Sets in the development and maintenance process. One important use prior to fully defining the Value Set Content 
			Logical Definition, is to include a set of easily understood example concepts that are consistent with concepts expected to be found in the Value Set Expansion Code Set. This 
			use replaces a defined Example Content element included in a prior version of this specification. Changes to this element should never result in a new Value Set Definition Version.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>&nbsp;&nbsp;&nbsp;CommentTimeStamp (sub-element)</td>
            <td>date/time when the comment was created</td>
            <td>The time stamp for the comment</td>
            <td>Changes to this element should never result in a new Value Set Definition Version.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#dateTime">dateTime</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Trusted Value Set Expansion Source</td>
            <td>list of references to trusted Value Set Expansion Code Sets</td>
            <td>This is to be used to provide links to services for existing persisted Value Set Expansions that are known by the Value Set Author where the Value Set Expansion content can be trusted.</td>
            <td>This URI should directly yield the Value Set Expansion.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#uri">uri</a></td>
            <td>0..*</td>
        </tr>
        <tr>
            <td>Type</td>
            <td>
                <p>characterization of the Value Set Definition</p>
            </td>
            <td>
                <p>user-defined descriptive phrase meant to characterize the content logical definition (CLD.)</p>
            </td>
            <td>
                <p>The following descriptive words have traditionally been used to describe the CLD in HL7 standards. Other phrases may be of use for some users.</p>
                <ul>
					<li>Extensional: the CLD is a simple list of individually specified concepts that uses no relationships or other attributes to determine the Value Set Expansion Code Set.</li>
					<li>Grouping: the CLD is restricted to a UNION of one or more other Value Set Definition references.</li>
					<li>Intensional: the CLD is an algorithm that, when executed by a machine (or interpreted by a human being), yields a set of concepts.</li>
				</ul>
            </td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
    </tbody>
  </table>
  <table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Value Set Definition Version — Derived Elements<br><br>Elements in this section are not entered by the author, but are derived values based on other elements in the Value Set Definition metadata.</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Code System Source</td>
            <td>
                <p>the Code System(s) identifiers explicitly referenced by the Value Set Definition’s Content Logical Definition.</p>
            </td>
            <td>
                <p>An exhaustive list of all Code Systems referenced in the Content Logical Definition.</p>
            </td>
            <td>
                <p>This list of Code System Identifiers should be derived from the Content Logical Definition to ensure that it is accurate. When the Content Logical Definition does not 
				specify any content types based on Code Systems, this is not populated. It is possible that a Code System will be in the CLD <i>but not generate a concept in the Value Set
				Expansion Code Set </i>if codes specified in the CLD are inactive or if an expression does not identify any codes; therefore, this may list Code Systems that are not 
				resident in a specific Value Set Expansion Code Set.</p>
            </td>
            <td>
                <p>UID (OID, UUID, URI or RUID) (replace with <a href="https://www.hl7.org/fhir/datatypes.html#uri">uri</a>???)</p>
            </td>
            <td>
                <p>0..*</p>
            </td>
        </tr>
    </tbody>
  </table>

#### Creation Information

Creation Information contains the initial creation user data for the Value Set Definition. Changes to these elements should never result in a new Value Set Definition Version.

<table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Creation Information</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Creation Date</td>
            <td>when the Value Set Definition was originally created.</td>
            <td>This element records the date-time when the first draft of the Value Set Definition was saved.</td>
            <td>The expectation is that if the creation date is unknown, that one will be asserted when the Value Set Definition is entered into the system.</td>
            <td>TS (<a href="https://www.hl7.org/fhir/datatypes.html#date">date</a> or <a href="https://www.hl7.org/fhir/datatypes.html#dateTime">dateTime</a>???)</td>
            <td>
                <p>1..1</p>
            </td>
        </tr>
        <tr>
            <td>Created By</td>
            <td>name of the user entity that created this Value Set Definition.</td>
            <td>This records the entity that performed the original Value Set Definition creation step. This data will persist for the life of the Value Set Definition (and is 
			consistently represented in all versions) because the original creation occurs only once.</td>
            <td>Some systems may allow an organizational entity as a user, most systems require an individual to be a user. In VSAC, this is the logged in individual user that 
			saved the first view of the Value Set Definition. In most instances it would be best if this were the original Value Set Definition steward to capture that information
			without requiring a query into the Value Set Definition modification history.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
    </tbody>
  </table>

#### Revision History

Revision History is used to record individual changes to any element of the Value Set metadata. It is intended to capture changes over time and serves as an audit trail of all 
such changes. Any change of any kind can result in a revision history item.

<table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Revision History</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Revision Date</td>
            <td>
                <p>date and time when an element was changed in some way.</p>
            </td>
            <td>The date-time when a Value Set Definition element was stored</td>
            <td>
                <p>This should be captured precisely enough to prevent confusion. In most cases, a date may work, but particularly volatile cases may require greater precision such as down to the second.</p>
            </td>
            <td>TS (<a href="https://www.hl7.org/fhir/datatypes.html#date">date</a> or <a href="https://www.hl7.org/fhir/datatypes.html#dateTime">dateTime</a>???)</td>
            <td>1..1</td>
        </tr>
        <tr>
            <td>Tracking Identifier</td>
            <td>
                <p>identifier for the changes for each revision</p>
            </td>
            <td>
                <p>Unique identifier for the change captured in the revision history.</p>
            </td>
            <td>
                <p>This may be used to disambiguate multiple changes and revisions that all carry the same timestamp, such as those done for publishing reasons. It may be best if this is a GUID.</p>
            </td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Revised By</td>
            <td>name of user entity responsible for the revision</td>
            <td>Carries the name or identification of the user entity that is considered to have made the revision.</td>
            <td>Some systems will assign this as the entity that was logged in when the revision occurred.</td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
        <tr>
            <td>Change Notes</td>
            <td>annotation of revision</td>
            <td>Specific narrative description and/or explanation of the changes made to the Value Set Definition, e.g., what was done and perhaps why.</td>
            <td></td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>0..1</td>
        </tr>
    </tbody>
  </table>
  
  <table class="grid">
    <tr style="font-weight: bold; background-color: #eeeeee"><td colspan="6">Revision History — Derived Element</td></tr>
	<tr style="font-weight: bold;"> <th>Element</th> <th>Definition</th> <th>Description</th> <th>Usage Notes</th> <th>Data Type</th> <th>Cardinality</th></tr>
    <tbody>
        <tr>
            <td>Revision Version Identifier</td>
            <td>the Value Set Definition Version Identifier to which the history item applies. </td>
            <td>A derived element that captures the current Value Set Definition Version Identifier at the time the revision history item was created.</td>
            <td></td>
            <td><a href="https://www.hl7.org/fhir/datatypes.html#string">string</a></td>
            <td>1..1</td>
        </tr>
    </tbody>
  </table>