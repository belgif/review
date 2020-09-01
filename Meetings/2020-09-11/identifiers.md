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
*	To designate the type of an identifier value and its associated semantics
   * The listed identifiers have a specific structure, granting authority, lifecycle, etc. The generic identifier (http://purl.org/dc/terms/identifier) doesn’t convey this information. These identifiers are also used in various analogue ways e.g. paper input forms, and the national number on the eID card.
*	To differentiate between different identifiers for the same entity: e.g. nrn (BE), bsn (NL) for the same person

Note that at CBSS, we don’t have a practical use case for any of the URIs at the moment because we don’t have an application using Linked Data. Though I think specific URIs would be needed if we would.
