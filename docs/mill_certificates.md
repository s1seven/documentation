# Steel mill certificates

## Current situation

Producers of steel products create mill certificates by

* printing a document, signing and scanning it or
* creating a PDF document
and sending it to buyers by email.

## Issues with current situation

The most important pain points in our understanding are:

* Scanned documents and PDFs are hard to process electronically so a lot of effort is spent on extracting only essential information manually in various steps of the value chain.
* Authenticity of documents cannot be verified easily so tampering with mill certificates happens all the time.

## New approach

Producers of steel products create mill certificates by

* creating a JSON file with the data used in the past for PDFs
* submitting the JSON file to the S1Seven platform

S1Seven platform

* validates the formal correctness of the JSON file via JSON Schema
* renders a PDF document from the JSON file
* notarizes both the JSON file and the PDF on the blockchain with the producers signature
* sends the JSON file and the PDF by email to the buyer

## Advantages of the new approach

The most important ones are

* the data is made available in two formats, PDF operating as an user interface to data for humans and JSON serving machines well
* creating the PDF document directly from the JSON file garantues that both formats have the same data
* immutable proofs on the contents are provided on Blockchain
* the authenticity of the electronic document and the PDF can be verified on the blockchain
* existing process continues with PDF documents so all customers can be switched in one step
* the machine readable JSON format is provided to customers using existing processes and protocols resulting in very low roll out cost
