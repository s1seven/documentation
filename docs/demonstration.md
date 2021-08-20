# Demonstration

This is a step by step guide to go through the full process of creating a certificate document as JSON file, notarize it on the blockchain and verify the integrity of both delivered documents, the raw JSON file and the certificate as PDF document.

## Step 1: Download sample JSON file

Download the file [example.json](/_json/example.json ':ignore title :target=_blank').

## Step 2: Edit the receiver email address in JSON file

Open the file in an editor and enter your email address in the element `A06/Email`:

    "A06": {
        "CompanyName": "Steel Trading",
        "Street": "Handelsgasse 1",
        "ZipCode": "10115",
        "City": "Berlin",
        "Country": "DE",
        "Email": "[Enter your email address here!]"
    }

## Step 3: Update the value for the CO2 footprint of the product

    "B98": {
        "Key": "CO2 Footprint in kg CO2e/kg",
        "Value": "1.71",
        "Type": "number"
    }

Save the file.

## Step 4: Notarize the sample JSON file

Drag and drop the file into the "Drag & Drop" section.

<iframe width="100%" height="500" src="https://demo.notarization.en10204.io"/></iframe>

Wait until the processing is completed and success is reported as illustrated.

The screen will be updated with a success message:

>example.json is a valid certificate!</br>
>It has been notarized **here**</br>

Clicking on the **here** link to the transaction on the Blockchain. In the element `asset` the hashes of the JSON and the generated PDF can be found included a characterization of the document type.

    "asset": {
      "data": {
        "pdfHash": "e27244bbed86e055a478a44151e9d9576dfc8969eeff5bc6c34819e9e6686847",
        "certificateType": "en10168-schemas",
        "jsonHash": "e3db9cfa7fd8bdc13ba66e13ee92c97c7be0460faabae3087d3d57e38b24d07c"
      }
    }

## Step 5: Receive the certificate

A view seconds after the successful notarization of the both the JSON and PDF certificate document you should receive an email with:

1. The contents of the certificate rendered as HTML in the email itself.
2. The certificate raw JSON document as an attachment.
3. And the certificate rendered as PDF document, again as attachment.

Download both the JSON and PDF document to your computer. 

## Step 6: Verify the JSON and PDF document

Upload the JSON document.

<iframe width="100%" height="500" src="https://demo.verification.en10204.io"/></iframe>

After the upload the hash of the document is calculated and a query with the hash is sent to the Blockchain. If the hash can be found the message is:

>✅ SteelFactory_SteelTrader_0334-2019-ZZS_1.json is verified</br>
>Creator: 6MXbQupMW6Vxy95b6DrVYB17bBudJTXG2KyT7Q3gk8iS</br>
>Timestamp: 4/2/2020, 6:20:16 AM</br>
>**See transaction**

    "asset": {
      "data": {
        "pdfHash": "e27244bbed86e055a478a44151e9d9576dfc8969eeff5bc6c34819e9e6686847",
        "certificateType": "en10168-schemas",
        "jsonHash": "e3db9cfa7fd8bdc13ba66e13ee92c97c7be0460faabae3087d3d57e38b24d07c"
      }
    }

Repeat with the PDF document.

>✅ SteelFactory_SteelTrader_0334-2019-ZZS_1.pdf is verified</br>
>Creator: 6MXbQupMW6Vxy95b6DrVYB17bBudJTXG2KyT7Q3gk8iS</br>
>Timestamp: 4/2/2020, 6:29:15 AM</br>
>**See transaction**

    "asset": {
      "data": {
        "pdfHash": "e27244bbed86e055a478a44151e9d9576dfc8969eeff5bc6c34819e9e6686847",
        "certificateType": "en10168-schemas",
        "jsonHash": "e3db9cfa7fd8bdc13ba66e13ee92c97c7be0460faabae3087d3d57e38b24d07c"
      }
    }

In case the JSON or PDF has been tampered the hash calculated by the Verification Service will not be found resulting in the message:

>❌ SteelFactory_SteelTrader_0334-2019-ZZS_1.PDF is not verified
