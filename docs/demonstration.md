# Demonstration

This is a step by step guide to go through the full process of creating a certificate document as JSON file, notarize it on the blockchain and verify the integrity of both delivered documents, the raw JSON file and the certificate as PDF document.

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

<iframe width="100%" height="500" src="https://demo.notarization.en10204.io"/></iframe>

Wait until the processing is completed and success is reported as illustrated.

The screen will be updated with a success message:

>example.json is a valid certificate!</br>
>It has been notarized **here**</br>
>And the generated PDF has been notarized **here**

In case the uploaded JSON document is not valid certificate - it does not comply to the structures defined by a JSON Schema - only the hash of the document is calculated and put on the blockchain. 

      "asset": {
        "data": {
          "notarization": "SBS Notarized:c84f10d82e8b19c2f552035106f99df4b9ea3caec63933b737fe9185c7a1b6da"
        }
      }

Clicking on the **here** link for the PDF opens the transaction. In the element `asset` the hash of the PDF can be found in the entry `notarization`. Furthermore, the link to notarization of the JSON is stored in `jsonLink`.

     "asset": {
        "data": {
          "jsonLink": "https://test.ipdb.io/api/v1/transactions/015c651968e7ee1b7e49f0b8309ee800b48783c72f4920d3c2ba5416a805cc08",
          "notarization": "SBS Notarized:872fee239f29f6decf5b1912b8171f0d07e828b6a58a5ac249a34e865bb62611"
        }
      }

This documents that the input for the PDF is the linked JSON document.

### Note
The demo system for notarization is not requiring any authentication nor keys to make things simple. For test and liver systems public private key pairs will be required, see section [Deployment](/deployment).

## Step 4: Receive the certificate

A view seconds after the successful notarization of the both the JSON and PDF certificate document you should receive an email with:

1. The contents of the certificate rendered as HTML in the email itself.
2. The certificate raw JSON document as an attachment.
3. And the certificate rendered as PDF document, again as attachment.

Download both the JSON and PDF document to your computer. 

## Step 5: Verify the JSON and PDF document

Upload the JSON document.

<iframe width="100%" height="500" src="https://demo.verification.en10204.io"/></iframe>

After 




>✅ SteelFactory_SteelTrader_0334-2019-ZZS_1.json is verified</br>
>Creator: 6MXbQupMW6Vxy95b6DrVYB17bBudJTXG2KyT7Q3gk8iS</br>
>Timestamp: 4/2/2020, 6:20:16 AM</br>
>**See transaction**

      "asset": {
        "data": {
          "notarization": "SBS Notarized:c84f10d82e8b19c2f552035106f99df4b9ea3caec63933b737fe9185c7a1b6da"
        }
      }

Repeat with the PDF document.

>✅ SteelFactory_SteelTrader_0334-2019-ZZS_1.pdf is verified</br>
>Creator: 6MXbQupMW6Vxy95b6DrVYB17bBudJTXG2KyT7Q3gk8iS</br>
>Timestamp: 4/2/2020, 6:29:15 AM</br>
>**See transaction**

     "asset": {
        "data": {
          "jsonLink": "https://test.ipdb.io/api/v1/transactions/015c651968e7ee1b7e49f0b8309ee800b48783c72f4920d3c2ba5416a805cc08",
          "notarization": "SBS Notarized:872fee239f29f6decf5b1912b8171f0d07e828b6a58a5ac249a34e865bb62611"
        }
      }

In case the JSON or PDF has been tampered the hash calculated by the Verification Service will not be found resulting in the message:

>❌ SteelFactory_SteelTrader_0334-2019-ZZS_1.PDF is not verified