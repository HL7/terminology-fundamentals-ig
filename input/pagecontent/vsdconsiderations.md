
Value Sets have been a part of model constructs from the very beginning, but in general have always been implemented in a way to support easy use and review 
of the model content. The following content is not included in the normative specification and as such, is provided as informative content to assist the reader 
and implementers. In most cases a Value Set has either been a list of ideas rendered within the structure of the model or as an attached supplement. The format 
of these artifacts is usually a table, because at a minimum the members of the Value Set are linked tuples with some sort of code/mnemonic linked to a wordier 
description with the expectation that the code/mnemonic was used in model instances with the description displayed for human use. The table would have some sort 
of identifier (often derived by the structure of the publishing document). It is very likely that there are more Value Sets developed, stored and maintained in 
spreadsheet format than in any other technology. As a quick and efficient way of getting the material in a presentable form, this has worked for years. In fact, 
in a very real way the HL7 V2.x world has continued to struggle to move beyond this approach.  

We now understand that such embedded “Value Set” artifacts are problematic because they live in isolation with little overarching governance. At a minimum there 
is value in separating the Value Set content from the artifacts using that content to encourage re-use in other appropriate models. This specification describes 
the metadata that should be used to describe a Value Set that stands alone and as such can be maintained, versioned, vetted and reused. As such, that definition 
can then be applied to a Code System to produce an instance Value Set Expansion Code Set of member concepts. The now independent Value Set Definition can be 
repeatedly applied to every new version of the Code System, producing the latest up-to-date Value Set Expansion Code Set for each new Code System version.

### Implementation Technologies
Traditionally Value Sets have been managed in files, usually spreadsheets. This technology is still useful and can contain all the information noted in the Value 
Set Definition specification. Obviously it can also be used for a Value Set Expansion Code Set (as this technology has essentially been the method of choice in most systems), 
but new technologies that provide database support to the Value Set metadata are extremely useful for repositories, particularly those with authoring and content delivery 
functionality. This specification is agnostic to the technology choices that may be used to implement the requirements.

### Authoring
The importance of the provenance in support of the creation and maintenance of Value Sets is of utmost importance to vetting and open reuse of Value Set Definitions. 
Therefore, a number of workflow-related elements are included in this specification. For some, authoring is a complex, multi-step process that must support internal 
(and potentially external) review, approvals, versions and publication. Only through this kind of rigorous process will the use of understandable and consistent Value 
Sets be possible, a key milestone in true interoperability. As noted in the specification, Value Sets can change stewardship because many useful Value Sets are developed 
under a contractual relationship that can change over time.

### Reuse of Value Sets

Consistency in meaning across implementations is the cornerstone of semantic interoperability. Value Set reuse is critical to this process and through reuse and 
re-vetting, improvements are inevitable. Implementers do not want multiple Value Sets with small variations (or worse, no variation) – reuse means a common approach 
to a single issue and provides for meaningful variation where required. To improve the probability of appropriate reuse, it is critical that Value Set definitional 
(e.g., Scope) and non-definitional (e.g., Use, Source Reference) elements are consistently included and documented to a degree which allows implementers to understand 
aspects such as intent, use, inclusion criteria, exclusion criteria etc. without having access to the Value Set author and/or steward. Likewise, ensuring that the 
author and/or steward information is complete and available will enable clarifying discussions between implementers when there are questions about an existing Value 
Set Definition, thereby preventing redundant Value Set creation.

### Distribution

The Value Set Definition specification has as a primary goal support for alignment of the critical elements needed to describe a Value Set, a defined approach to 
versioning and a complete set of functions needed to describe a simple or complex query into a Code System to retrieve the Value Set Expansion that provides the actual 
Value Set members. While this version of the specification does not describe a syntax for exchange and distribution of either the Value Set Definition or the Value Set 
Expansion, it does provide a platform to determine this in the future.

### Impact of Code System Evolution

A central tenet to the specification is the fact that Value Set Definitions are often created with the expectation that the information is robust and will stand “the test 
of time” – most importantly, it will continue to generate appropriate Value Set Expansion Code Sets as the Code System matures. This means that a single Value Set Definition 
version that is not tied to a particular Code System Version is expected to continue to produce appropriate and usable Value Set Expansion Code Sets for every new Code System version.  

Authors/stewards may review these new Value Set Expansion Code Sets to be assured that assumption remains correct. If they find problematic changes in the Value Set Expansion 
Code Set based on a new Code System version, they can make appropriate changes to the CLD and publish this (as required) as a new Value Set Definition Version. They may even 
restrict the use of the prior Value Set Definition Version such that new content based on that outdated Value Set Definition is not allowed, forcing migration to the newer 
version (when using the appropriate Code System version).
