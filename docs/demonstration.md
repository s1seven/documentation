# Demonstration

This is a step by step guide to go through the full process of creating a certificate document as JSON file, notarize it on the blockchain and verify the integrity of both delivered documents, the raw JSON file and the 
## Step 1: Download sample JSON file

Download the file [example.json](/_json/example.json ':ignore title :target=_blank').

## Step 2: Edit sample JSON file

Open the file in an editor and enter your email address in the element `A06/Email`:

    "A06": {
        "CompanyName": "Steel Trading",
        "Street": "Handelsgasse 1",
        "ZipCode": "10115",
        "City": "Berlin",
        "Country": "DE",
        "Email": "[Enter your email address here!]"
    }
Save the file.

## Step 3: Notarize the sample JSON file

Drag and drop the file into the "Drag & Drop" section.

<iframe width="100%" height="400" src="https://test.notarization.en10204.io"/></iframe>

Wait until the processing is completed and success is reported as illustrated.

Result [Screenshot]

## Step 4: Receive the certificate

A view seconds after the successful notarization of the both the JSON and PDF certificate document you should receive an email with:

1. The contents of the certificate rendered as HTML in the email itself.
2. The certificate raw JSON document as an attachment.
3. And the certificate rendered as PDF document, again as attachment.

Download both the JSON and PDF document to your computer. 

## Step 5: Verify the JSON and PDF document

Upload the JSON document.

<iframe width="100%" height="400" src="https://test.verification.en10204.io"/></iframe>

Result [Screenshot]

Repeat with the PDF document.
Result [Screenshot]
