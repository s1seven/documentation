# Design Approach

## Background

The European Standard [EN 10168](https://www.en-standard.eu/bs-en-10168-2004-steel-products-inspection-documents-list-of-information-and-description/) defines five information groups to document the results of steel product inspection. For each information group 99 or 100 fields are defined with a very basic naming convention - letter for the section and 2 digit number.

| Information Group | Fields| 
|---|---|
| Commercial transactions and parties involved | A01 to A99|
| Description of products | B01 to B99|
| Inspection | C00 to C99|
| Other tests | D01 to D99|
| Validation | Z01 to Z99|

In each group some fields are designated for specific information and in all groups are many fields for designation and many for free usage. It should be noted that the standard does not give any recommendations on formats so basically all fields have to be considered as strings from a software development perspective.

### Examples

To illustrate the designation of sections (or fields in our understanding) some examples are given. 

| No | Section designation | Contents |
|---|---|---|
| A01 | Manufacturer's works | Name and address of the works where the products were manufactured.|
| B07 | Identification of the product | Indications for the traceability of the products, e.g. cast number, ingot number, rolling number, batch number, test number. |
| C11 | Yield or proof strength | Yield or proof strength recorded in MPa.|
| C93 to C99 | Supplementary information | Available for supplementary information on the chemical composition. |

## Research

We have been studying certificates created by many market participants viewing them from the view point of machines - how is data provided for easy and high quality processing.

## Results

In our humble opinion there are a lot of issues in practice. Here we are writing up the most important ones as starting point for machine readable format. 

### Sections 

There are no definitions nor any guidance provided how to structure information in any section so there is no easy processing of data. OCR and modern machine learning/artifical intelligence techniques might be able to process big parts of the information available but still with a lot of failures and errors. 

Many companies provide metadata on the data by noting the section to the piece of information printed on. A simple example is

[Screenshot of a section]

### Companies
First prominent sections are A01, A05 and A06 which contain the manufacture, the laboratory and buyer information. Company name and address information is provided in country specific format but most important lacks a global valid identifier as e.g. the VAT ID in Europe or DUNS, which is popular in other parts of the world.

### Product Description

To describe the product there are basically four essential fields:

| No | Section designation | Contents |
|---|---|---|
| B01 | Product| Description of the product form (e.g. : heavy plate, section, wide flat, tube, hollow section, etc.) and, where appropriate, surface condition, with reference to the dimensional standard, if applicable.|
| B02 | Steel Designation | ISteel name or number and additional symbols and the product specification for the steel. |
| B03 | Any supplementary requirements | This section is for indicating special requirements, agreed at the time of ordering, not appearing in sections B 01 and B 02.|
| B04 | Product delivery condition | Delivery condition of the products as specified in the applicable product specification. |

The real world is basically a mess illustrated by an overview of approaches we have seen:

* Product **EW Steel Pipes S355J2H EN 2019/1/2-2006** written to a combined section for B01 and B02
* Product in B02 split into 
    * Product Norm
    * Material Norm
    * Mass Norm
    * Steel Grade
    * Product Code
* Product **TUBE NORMALIZED (+N), EN 10210-1 ATA** in B01, steel grade **S355J2H/NH** in B02 plus a combined section of B04 and B09-B11 with **SGM 100x100x12,5x12000 S355J2H 10210 HF**
* No section specified  with **S355J2H N / E355+N / St 52.0 N** and **DIN 2448: 81 EN 10210-1; 2: 06/ EN 10297-1: 03; DIN 1629: 84** which points to the interesting case a product complies to multiple standards.
* One company put everything into a section described **B01-B04**
* Steel grade **C45+A/1.1730** in B02, the norm **EN 10083-2:2006** is provided in section B14 as supplementary information.
* One company splits B02 into B02.1 for steel grade and B02.2 for the norm.

### Identification of the product
To identify a product section B07 is designated by the norm, which describes it with

*Indications for the traceability of the products, e.g. cast number, ingot number, rolling number, batch number, test number.*

In our simple understanding the section should contain the batch number of the product with which the mill certificate comes, e.g. the production batch number for some tubes. However, tracability must be ensured back to the inital cast number so in practice people developed some workarounds:

* Split of B07 into B07.1, into which goes **Heat Number** and B07.2, into which goes **Specimen number**.
* Many occurances of B07, put into context with processing step and its inspection, e.g. a batch number associated with the chemical analysis and a batch number associated with the product. We have seen up to **five** B07 on one mill certificate. 

This is perfectly fine when looking at it from the production process and on paper. However, dealing with more than one B07 in an format to be consumed by software is getting tricky pretty fast. 

### Chemical Analysis

Sections C71 to C99 are dedicated to the chemical analysis but leaving open which chemical element goes into which section. In practice there is a quasi industry standard on which chemical element goes into which field but still there are slight differencies between the producers.

### Processing of Mill Reports
As final observation we would like to add the fact that we talked to many people which would love an electronically processable certificate - they look basically at each certificate and enter some values manually into their system. And our rough estimate on certificates in Europe only is in magnitude of 100 million annually!

## Conclusions

Based on our observations we came to the following conclusions on EN 10168:

* It is a very open standard enabling users to add any kind of information which is produced in inspecting steel products.
* It defines a somehow precise definition for a very limited set of information.
* The industry established some common practices to provide certain information.
* The target platform for the standard is paper which is fine as paper (and nowadays PDF) are the only means to establish document character.
* There is a need for data in a machine readable format, confirmed by basic tools offered by some companies. 

## Objectives

Based on our observations and conclusions we set ourselves the following objectives for the design of an electronic format:

* The target platform for the format are both machines and humans (in the forma of PDFs).
* The format must be developer friendly enabling easy implementation of both the creation of data in the format and reading it for further processing.
* The format should provide standards and guidelines for many data points.
* The format should flexible to integrate all kinds of information.
* The format should make it easy to render great looking PDF documents following established practices.

The data format in the next chapters tries to perform the balancing act to meet this to some extend contradictory objectives.

