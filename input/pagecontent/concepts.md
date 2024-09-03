<a name="concepts"/>

A Concept is defined as an unitary mental representation of a real or abstract thing – an atomic unit of thought. It should be unique in a given Code System. 
A concept may have synonyms in terms of representation and it may be a singleton, or may be constructed of other concepts (i.e. post-coordinated concepts).  

Concepts, as abstract, language- and context-independent representations of meaning, are important for the design and interpretation of HL7 data models. 
They constitute the smallest semantic entities on which HL7 datamodels are built. The authors and the readers of a model use concepts and their relationships 
to build and understand the models; these are what matter to the human user of HL7 data models. The rest of the terminology machinery exists to permit software 
manipulation of these units of thought.  

A Concept Representation is defined as a terminology object that enables the manipulation of a Concept in HL7. A Concept Representation exists in some form that is computable, 
and can be used in HL7 models and specifications. Concept Representations can take on a number of different roles in the structure and processing of terminology in HL7; these roles and functions are described below.  

A Code is defined as a Concept Representation published by the author of a Code System as part of the Code System. It is the preferred unique identifier for 
that concept in that Code System for the purpose of communication (preferred wire-format identifier), and is used in the 'code' property of an HL7 coded data type. 
Codes are sometimes meaningless identifiers, and sometimes they are mnemonics that imply the represented concept to a human reader. In Code Systems that contain more 
than one Concept Identifier, the one that should be used in HL7 as the Code should be explicitly declared.  

The meaning of a Code within a particular Code System entity is valid only within that Code System. For example, each table having enumerated codes in the HL7 Codes
are sometimes used in different Code Systems to have different meanings. One example is the code "M" in the <a href="http://terminology.hl7.org/CodeSystem/v2-0001">Administrative Sex</a> Code System which signifies "Male," 
whereas the code "M" in the in the <a href="http://terminology.hl7.org/CodeSystem/v2-0001">Marital Status</a> Code System signifies "Married". Another example is the code "1609-7" which signifies the Native American tribe 
"Sioux" in the Race &amp; Ethnicity – CDC Code System, and the code "1609-7" which signifies "Prolactin^1.5H post dose insulin IV" in the LOINC Code System. Codes do 
not have explicit semantics without their Code Systems, and cannot be referenced without identifying the code system in which they are published.  

A Concept Identifier is defined as a Concept Representation that may be published by the Code System author, and unambiguously represents the concept internally 
within the context of that Code System. Such an object used for identification, when combined with the unique identifier of the Code System itself (a machine-processable 
unique string), provides a globally unique and language-independent identification for the particular concept. This globally unique identification can be used in transactions 
and data records that span both space and time. In some cases, multiple synonymous identifiers may be present for the same concept.  

A Coding is a Concept Representation is a structured way to represent a specific concept using 

Codeable Concept (placeholder)  

A Designation is defined as a language symbol Concept Representation that may be published by the Code System author for a concept, and are intended to convey meaning to a human being. 
These are additional representations for the concept. Use cases include other languages or aliases used for particular purposes for a concept. A Designation is typically used to 
populate an alternate display for the concept.  

The following table may help to clarify the differences in meanings and uses of these Concept Representations.  

<table class="grid">
	<tr style="font-weight: bold; background-color: #eeeeee"><td colspan="4">Some Names and Uses for Concept Representations</td></tr>
	<tr style="font-weight: bold;"> <th>Name</th> <th>Definition</th> <th>Primary HL7 Use</th> <th>Examples</th></tr>
	<tr> <td>Code</td> <td>An identifier for a concept intended for use when representing a concept in a computable manner. For example, passing into a decision support tool or for use in data exchange. 
	Some code systems use human-readable mnemonics for these.</td> <td>Pass information between or shared by different systems in a computable manner.</td> <td>HL7 AdministrativeGender: F<br>
	LOINC:6690-2<br>SNOMED CT:233607000<br>UCUM:L, mg/L</td></tr>
	<tr> <td>Concept Id</td> <td>A concept representation that is unique within the code system and that is used internally by the code system when referencing concepts.</td> <td>Many code systems use 
	the same value for Concept Code and Concept Identifier, therefore the Concept Identifier may be used in CD.code; however, it is often used as a component of maps and ontologies outside of HL7 
	interoperability standards. Some Code Systems have more than one Concept Identifier for a concept.</td> <td>HL7 AdministrativeGender: F<br>LOINC:6690-2<br>SNOMED CT:233607000<br>UCUM: m, g, L</td></tr>
	<tr> <td>Coding</td> <td></td> <td></td> <td></td></tr>
	<tr> <td>Codeable Concept</td> <td></td> <td></td> <td></td></tr>
	<tr> <td>Designation</td> <td>Human consumable representation of the concept; may or may not be a string of characters; generally subject to language variants.</td> <td>Human language representation 
	of the concept. A concept has 1..* of these. Often language-dependent, i.e. a set of English designations, a set of French designations, etc.</td> <td>HL7 AdministrativeGender:<br>Female<br>
	<br>LOINC:<br>Leukocytes [#/volume] in Blood by Automated Count<br>WBC #Bld Auto<br><br>SNOMED CT:<br>Pneumococcal pneumonia (disorder)<br><br>UCUM:<br>Litre<br>
	mg/L<br>L<br>milligram/Litre<br>gram/Litre</td></tr>
  </table>