# Identifiers

## Origin 
The federal G-Cloud functional workgroup requests input from the ICEG review group with respect to the topic of "Identifiers".

See issue list https://github.com/belgif/fedvoc/issues/10

## Context
ICEG URI standard: https://github.com/belgif/thematic/blob/master/URI/iceg_uri_standard.md

Federal vocabulary standard: 
* https://github.com/belgif/fedvoc (intro), 
* https://github.com/belgif/fedvoc/blob/master/FederalServicePlatform-Vocabularies.xlsx (federal vocabulary standard)

## Simple identifiers
The identifiers in the following table each received as URI:  <http://purl.org/dc/terms/identifier>
Id | Ontology | Name | Definition
-- | -------- | ---- | ----------
687 | Generic | bic | Business Identifier Code, also known as Swift Code. International identifier for financial and non-financial institutions, commonly used for international bank transfers.
685 | Generic | iban | International Bank Account Number, as defined in ISO 13616:2007
680 | Generic | identifier | "Recommended best practice is to identify the resource by means of a string conforming to a formal identification system. An unambiguous reference to the resource within a given context."
686 | Location | municipalityCode | Numeric code to identify a Belgian municipality.
294 | Location | objectId | "Recommended best practice is to identify the resource by means of a string conforming to a formal identification system. An unambiguous reference to the resource within a given context."
702 | Location | streetNrCode | Street code assigned by National Registry
241 | Organization | cbeNumber | Identifier issued by CBE for either an organization or a site (establishment) of an organization
691 | Organization | employerId | Definitive or provisional NSSO number, assigned to each registered employer or local or provincial administration.
231 | Organization | enterpriseNumber | Identifier issued by CBE for a registered organization
232 | Organization | establishmentUnitNumber | Identifier issued by CBE for a site (establishment) of an organization 
692 | Organization | nssoNumber | "Recommended best practice is to identify the resource by means of a string conforming to a formal identification system. An unambiguous reference to the resource within a given context."
693 | Organization | pplNumber | "Recommended best practice is to identify the resource by means of a string conforming to a formal identification system. An unambiguous reference to the resource within a given context."
694 | Organization | provisionalNssoNumber | "Recommended best practice is to identify the resource by means of a string conforming to a formal identification system. An unambiguous reference to the resource within a given context."
344 | Person | nrn | "Recommended best practice is to identify the resource by means of a string conforming to a formal identification system. An unambiguous reference to the resource within a given context."
349 | Person | ssin | Social Security Identification Number issued by the National Register or CBSS

## Complex identifiers
Id | Ontology | Type | URI | Name | Definition
-- | -------- | ---- | --- | ---- | ----------
256 | Generic | Class | <http://www.w3.org/ns/adms#Identifier> | Identifier | "This class is based on the UN/CEFACT Identifier complex type defined in See Section 5.8 of Core Components Data Type Catalogue Version 3.1 (http://www.unece.org/fileadmin/DAM/cefact/codesfortrade/CCTS/CCTS-DTCatalogueVersion3p1.pdf). In RDF this is expressed using the following properties: (1) the content string should be provided using skos:notation, datatyped with the identifier scheme (including the version number if appropriate); (2) use dcterms:creator to link to a class describing the agency that manages the identifier scheme or adms:schemaAgency to provide the name as a literal. Although not part of the ADMS conceptual model, it may be useful to provide further properties to the Identifier class such as dcterms:created to provide the date on which the identifier was issued."
679 | Generic | Property | <http://www.w3.org/ns/adms#identifier> | identifier | "adms:identifier is used to link any resource to an instance of adms:Identifier which is its range. N.B. it is not appropriate to use dcterms:identifer to link to the Identifier class as its range is rdfs:Literal. ADMS uses this to provide any identifier for the Asset."

## Problem
Until now, the way the federal functional wg handled identifying properties such as the nrn (national registry number), was to allocate the same URI  <http://purl.org/dc/terms/identifier> to this property.
The consequence was that a lot of identifying properties received the same generic URI.
These identifying properties could then be used to construct a complex identifier together with a namespace and eventual version.

KSZ/BCSS would like to give a distinct URI to each identifying property instead of allocating a generic URI. (e.g. http://vocab.belgif.be/ns/person#nrn instead of <http://purl.org/dc/terms/identifier> )

Additional info from KSZ/BCSS:

Some justification why separate URIs for the types of identifiers:
*	To designate the type of an identifier value and its associated semantics: 
the listed identifiers have a specific structure, granting authority, lifecycle, etc. The generic identifier (http://purl.org/dc/terms/identifier) doesn’t convey this information. These identifiers are also used in various analogue ways e.g. paper input forms, and the national number on the eID card.
*	To differentiate between different identifiers for the same entity: e.g. nrn (BE), bsn (NL) for the same person

Note that at CBSS, we don’t have a practical use case for any of the URIs at the moment because we don’t have an application using Linked Data. Though I think specific URIs would be needed if we would.

## Reaction Raf Buyle (2020-10-01)
Hereby some feedback and pointers regarding the discussion at the ICEG RC.
 
The identifier challenges — as discussed in https://github.com/belgif/review/blob/master/Meetings/2020-09-11/identifiers.md — require fair agreements.
 
As pointed out, there are two main approaches for identifiers:
*    a) without provenance knowledge
*    b) with provenance knowledge

Case a) is covered by the dct:identifier URI mapping, while b) is adms:identifier mapping.


In data exchanges, the need for one or both can exist. The implementation choice depends on the use-cases. It is both valid and correct approaches. 
So both need support. [*see below]
 
However there are two other discussion items that also have impact:
*   c) design of identifiers
*   d) dereferenceable identifiers


The design of identifiers corresponds to the table "Simple identifiers" (I would suggest renaming the table to designed/scoped identifiers, they are not that simple).  The table shows that for many entities an special designed identifier is created, tightening the existence of the entity to have an identifier according to that design. E.g. A bank account only exists if it has a IBAN number, but given an IBAN number we have a bank account. 
This design can be expressed e.g. as a custom XSD description. 
 
Now if one designs a payload then the implicit constraint that the identifier of the entity should follow the design of the identifier, is often made explicit via augmenting the label of the identifier with the indication of the desired design.  That is a human aid, not a machine aid. For the machine, the custom XSD description should be connected with that property. In the issue https://github.com/belgif/fedvoc/issues/10, one of the suggestions is to use than an identifier with provenance knowledge. 
 
Example: 


without provenance knowledge:

 ex:bartbankaccount dct:identifier "BE94123412341234" 


with provenance knowledge

ex:bartbankaccount adms:identifier [

skos:notation "BE94123412341234" ;

adms:schemaAgency "IBAN"

].


However, there is a third option: using typed literals.
A typed literal is a value according to design.
 
   ex:bartbankaccount dct:identifier "BE94123412341234"^^iso:IBAN.
 
Typed literals can be used here as with the URI iso:IBAN one can refer to the custom XSD to which the value should comply, and with some additional referencing agreements one could attach a human-readable specification pointing to the issuing or designer of this identifier design. 
 
So if for each of the registered simple identifier a custom XSD is being created and served via a PURI system then one can use the typed literal approach and is there no need to develop a specific property for each case.
 
The only reason for creating a specific property (which should be declared as a subproperty of dct:identifier or adms:identifier) is to be able to express addition constraints that are beyond the identifier definition with its design.
 
Then we still need to include the discussion on dereferenceable identifiers in this. A dereferenceable identifier is an identifier which core information can be retrieved using the http protocol. This is a much stronger binding of core provenance information into service on the identifier.
 
example:
 
   ex:bartbankaccount adms:identifier [

skos:notation "BE94123412341234" ;

adms:schemaAgency "IBAN"

dct:creator "Belfius"

].
 
could be represented in one URI 
    https://data.belfius.be/id/account/BE94123412341234
 
In that case, the maintainer of the identifier (and its core information) is included in the URL structure of the URI.  
 
In that case, the custom XSD is replaced by the persistency and dereferenceability aspects: the above is a bank account, not because it follows the IBAN design, but because it is issued by an authority that declares it is a bank account. The need for IBAN design rules then disappear but are replaced with SLAs on the persistency and deferenceability of the identifier.
 
Therefore as one does not is serving only one user context, all 3 cases might be present in the same payload. 
 
In RDF turtle notation:
 
   <https://data.belfius.be/id/account/BE94123412341234>

dct:identifier "BE94123412341234"^^iso:IBAN ;

adms:identifier [

skos:notation "BE94123412341234" ;

adms:schemaAgency "IBAN"

dct:creator "Belfius"

].
 
 
in JSON-LD notation
 
{

"@context" : "...",  

"@id" : "https://data.belfius.be/id/account/BE94123412341234",

"identifier" : "BE94123412341234",

"adms_identifier" : {

"notation" : "BE94123412341234",
 
 "schemaAgency" : "IBAN",

"creator" : "Belfius"

}

}
 
where the context will map the terms to the corresponding URIs.
 
Observe that because of json one must force another label for dct:identifier and adms:identifier. Maybe here one can search for standard labels.
 
 
[*] the debate between these is one between a technical usage and a business usage. A technical usually tends to simplify the structure to a situation that is only covered by its prime use-cases, while business perspective usually then to be broader. (ease of use/payload size/transport costs, ...).
 
 
Kind regards,
Raf
 
