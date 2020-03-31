# JSON Definitions

## Company

### Definition of company in JSON Schema

    "Company": {
      "type": "object",
      "properties": {
        "CompanyName": {
          "type": "string"
        },
        "Street": {
          "type": "string"
        },
        "ZipCode": {
          "type": "string"
        },
        "City": {
          "type": "string"
        },
        "Country": {
          "type": "string",
          "minLength": 2,
          "maxLength": 2
        },
        "VAT_Id": {
          "type": "string",
          "minLength": 9,
          "maxLength": 11
        },
        "Email": {
          "type": "string",
          "format": "email"
        }
      },
      "required": [
        "CompanyName",
        "Street",
        "ZipCode",
        "City",
        "Country",
        "VAT_Id",
        "Email"
      ],
      "additionalProperties": false
    }

We require all defined elements: the element `Email` for obvious reasons, the element `VAT_Id` serves as global unique identifier of legal entities

### Application of company definition in JSON Schema

    "A01": {
      "description": "The manufacturer's works which delivers the certificate along the product",
      "$ref": "#/definitions/Company"
    }

### Usage of company in JSON 

    "A01": {
      "CompanyName": "Steel Factory",
      "Street": "Stahlstrasse 1",
      "ZipCode": "4010",
      "City": "Linz",
      "Country": "AT",
      "VAT_Id": "U12345678",
      "Email": "sbs.steelfactory@gmail.com"
    }

## Chemical Analysis

### Remarks
EN 10168 defines that in fields C71 to C92 the share of chemical elements has to be provided, but it does not map fields to chemical elements. In practice there is kind of quasi standard which element is put into which field. But a quasi standard doesn't work well for machines, so we suggest to provide the symbol for a chemical element for each field.

### Definition of chemical elements in JSON Schema

    "ChemicalElement": {
      "type": "object",
      "description": "The chemical elements of the product.",
      "properties": {
        "Symbol": {
          "description": "The symbol of the element",
          "type": "string"
        },
        "Actual": {
          "description": "The measured part of the element as absolute number.",
          "type": "number",
          "minimum": 0,
          "maximum": 1
        },
        "Minimum": {
          "description": "The minimum if defined by the product specification, otherwise the element must not provided.",
          "type": "number",
          "minimum": 0
        },
        "Maximum": {
          "description": "The maxium as defined by the product specification.",
          "type": "number",
          "maximum": 1
        }
      }
      "required": ["Symbol", "Actual"],
      "additionalProperties": false
    }

### Application of chemical element definition in JSON Schema

EN 10168 assigns fields C71 to C92 to which we assign the definition for chemical elements above.

    "C71": {
      "description": "Share of element",
      "$ref": "#/definitions/ChemicalElement"
    }

### Usage of chemical element in JSON

    "C71": {
      "Symbol": "C",
      "Actual": 0.088,
      "Minimum": 0,
      "Maximum": 0.5
    }

In case CEV is provided the solution is simply to use CEV as symbol as we do not restrict the length of the string for symbols to 2.

    "C72": {
      "Symbol": "CEV",
      "Actual": 0.088
    }

Furthermore, only the elements `Symbol` and `Actual`are required as in many cases the minimum and maximum values for the product are not put on the certificate.

The advantages of this solution is that no party are
* no need to define an absolute standard on which element goes into which field - because, who defines it?
* no need to change the mapping of which element goes into which field - keep frictions low
* developers building integrations can simply lookup the values for each element they want to import into systems

## Measurements

### Remarks

### Definition

    "Measurement": {
      "type": "object",
      "description": "Measured values in a structured fashion for easy processing and rendering of data",
      "properties": {
        "Property": {
          "description": "The property measured",
          "type": "string"
        },
        "Value": {
          "description": "A measured or calculated value (e.g. mean of individual measurements).",
          "type": "number"
        },
        "Minimum": {
          "description": "The lower limit according product specification. If not provided it is 0.",
          "type": "number"
        },
        "Maximum": {
          "description": "The upper limit according product specification. If not provided it is ∞.",
          "type": "number"
        },
        "Unit": {
          "description": "The unit of value.",
          "type": "string"
        }
      },
      "required": ["Value"],
      "additionalProperties": false
    }

## Key Value Elements

EN 10168 implements flexibility by defining plenty of supplementary information fields to add any kind of information     

### Definition of supplementary information in JSON Schema

    "KeyValueObject": {
      "type": "object",
      "properties": {
        "Key": {
          "type": "string"
        },
        "Value": {
          "type": "string"
        },
        "Unit": {
          "type": "string"
        },
        "Interpretation": {
          "type": "string"
        }
      },
      "required": ["Key", "Value"],
      "additionalProperties": false
    }

### Application of key value objects in JSON Schema

    "OtherMechanicalTests": {
      "type": "object",
      "propertyNames": {
        "pattern": "D[5-9][0-9]"
      },
      "patternProperties": {
        "": {
          "$ref": "#/definitions/KeyValueObject"
        }
      }
    }

### Usage of key value objects in other mechanical test

In this section typically a list of various tests is provided without any kind of result.

A use case is to provide information on hydrostatic tests including the test pressure.

    "NonDestructiveTest": {
      "D02": {
        "key": "Hydrostatic test - test pressure",
        "value": "7",
        "unit": "MPa/5s",
        "interpretation": "satisfactory"
      }
    }

Another use case is to provide the result of transverse flat bend tests, which is basically boolean - it either complies or not according the product definition/standards.

    "OtherMechanicalTests": {
      "D51": {
        "key": "Transverse flat bend test",
        "value": "complies"
      }
    }

### Closing remark

Many steel mills use the field D51 to provide information on the Transverse flat bend test, but as stated earlier it is just a quasi standard, so do not rely on that. 

## Supplementary Information

EN 10168 defines plenty of fields for any kind of information which could be possibly free text. Still we think that this information should be structured for easy reading and interpretation. There for we define supplementary information fiels as key value objects.

### Application of key value objects to supplementary information fields

    "SupplementaryInformation": {
      "type": "object",
      "propertyNames": {
        "pattern": "A[1-9][0-9]"
      },
      "patternProperties": {
        "": {
          "$ref": "#/definitions/KeyValueObject"
        }
      }
    }

### Usage of supplementary information fields 

    "SupplementaryInformation": {
      "A11": {
        "Key": "Delivery note number",
        "Value": "1583836"
      }
    }
 
  