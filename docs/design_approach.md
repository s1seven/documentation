# Design Approach

## Background

The European Standard [EN 10168](https://www.en-standard.eu/bs-en-10168-2004-steel-products-inspection-documents-list-of-information-and-description/) defines five information  groups to document the results of steel product inspection. For each information group 99 or 100 fields are defined with a very basic naming convention - letter for the section and 2 digit number.

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
| C 93 to C 99 | Supplementary information | Available for supplementary information on the chemical composition. |

## Observations

We have been studying many certificates created by many market participants and could a lot of things. Some of them we are writing up here stating upfront that this should not be considered an industry wide review collecting all aspects - this is simply an unfeasibale goal. And from our point of view not nessecary either.

### Companies
Fields A01 and A06 are designated to the manufacturer respective buyer

B07

We have one certificate which displays 5 times a B07 field 
1. in the group Product, which contains the batch number of product shipped to the buyer.
2. in the chemical analysis, which contains the charge number of the raw steel.
...

This is perfectly fine when looking at it from the production process. Nevertheless, it is a challenge to be addressed in designing a format and or implementation guide. 

### Chemical Analysis
There is a quasi industry standard which chemical element goes into which field but still there are slight differencies between the producers.

C71-C99

As final observation we would like to add the fact that we talked to many people which would love an electronically processable certificate - they look basically at each certificate and enter some values manually into their system. And our rough estimate on certificates in Europe only is in magnitute of 100 million annually!

## Conclusions

Based on our observations we came to the following conclusions:

* It is a very open standard enabling users to add any kind of information is produced in inspecting steel products.
* It defines a somehow precise definition for a very limited set of information.
* The industry established some common practices to provide certain information.
* The target platform for the standard is paper which is fine as paper (and nowadays PDF) are the only means to establish document character.
* There is a need for data in a machine readable format, confirmed by basic tools offered by some companies. 

## Objectives

Based on our observations and conclusions we set ourselves the following objectives for the design of an electronic format:

* The target platform for the format are both machines and humans (in the forma of PDFs).
* The format must be developer friendly enabling easy implementation of both the creation of data in the format and reading it for further processing.
* The format should provide standards and guidelines for many data points.
* The format should flexible to integrate all kind of information.
* The format should make it easy to render great looking PDF documents following established practices.

The data format in the next chapters tries to perform the balancing act to meet this to some extend contradictory objectives.

