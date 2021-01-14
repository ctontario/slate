
# Funding


## StudyFundingDocumentDelete - <em>Delete Study Funding Document</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/funding/:studyFundingId/documents/:type/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingDocumentDelete",
    "type": "object",
    "properties": {
      "studyFundingId": {"type": "string"},
      "type": {"type": "string", "enum": ["fundingHstExemption", "invoice"]},
      "documentId": {"type": "string"}
    },
    "required": ["studyFundingId", "type", "documentId"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Deletes one document from a Study Funding record using its type and id

### HTTP Request

`DELETE /funding/:studyFundingId/documents/:type/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingDocumentDownload - <em>Download Study Funding Document</em>


```shell
curl "https://ctoregistry.com/api/v1/download/funding/:studyFundingId/documents/:type/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingDocumentDownloadParams",
    "type": "object",
    "properties": {
      "studyFundingId": {"type": "string"},
      "type": {"type": "string", "enum": ["fundingHstExemption", "invoice"]},
      "documentId": {"type": "string"}
    },
    "required": ["studyFundingId", "type", "documentId"]
  }
}
```


> Response Schema

```json
undefined
```


Downloads one document from the specified study funding.

### HTTP Request

`GET /download/funding/:studyFundingId/documents/:type/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingDocumentUpload - <em>Upload Study Funding Document</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/upload/funding/:studyFundingId/:type"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/StudyFundingDocumentUpload",
    "type": "object",
    "properties": {
      "name": {"type": "string", "description": "The document name"},
      "documentId": {
        "type": "string",
        "description": "optional document Id, will update this document record if passed in"
      }
    },
    "required": []
  },
  "params": {
    "id": "/StudyFundingDocumentUploadParams",
    "type": "object",
    "properties": {
      "studyFundingId": {"type": "string"},
      "type": {"type": "string", "enum": ["fundingHstExemption", "invoice"]}
    },
    "required": ["studyFundingId", "type"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingDocumentUploadResponse",
  "type": "object",
  "properties": {
    "document": {
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "name": {"type": "string"},
        "uploadDt": {"type": "date"},
        "completeDt": {"type": "date"},
        "originalFilename": {"type": "string"}
      },
      "required": ["id", "uploadDt", "originalFilename"]
    }
  }
}
```


Uploads a document to the specified study funding record.  The document information is contained in the POST

### HTTP Request

`POST /upload/funding/:studyFundingId/:type`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingGenerateInvoiceDocuments - <em>Study Funding Generate Invoice Documents</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/funding/:studyFundingId/generate-invoice-documents"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingParams",
    "type": "object",
    "properties": {"studyFundingId": {"type": "string"}},
    "required": ["studyFundingId"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Processes the study funding and creates invoices for an invoices flagged as requiring new invoices.  This action is also done by the recalculate invoices route

### HTTP Request

`PUT /funding/:studyFundingId/generate-invoice-documents`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingHstExemption - <em>Update Study Funding Payee</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/funding/:studyFundingId/hst-exemption"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/StudyFundingHstExemptionBody",
    "type": "object",
    "properties": {"isHstExempt": {"type": "boolean"}},
    "required": ["isHstExempt"]
  },
  "params": {
    "id": "/StudyFundingHstExemptionParams",
    "type": "object",
    "properties": {"studyFundingId": {"type": "string"}},
    "required": ["studyFundingId"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Updates the Payee information regarding hst exemption for one study funding record

### HTTP Request

`PUT /funding/:studyFundingId/hst-exemption`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingInstitutionSearch - <em>Search Institutions with Funding Information</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/institution-search/:searchString?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/SearchParams",
    "type": "object",
    "properties": {"searchString": {"type": "string"}},
    "required": []
  },
  "query": {
    "id": "/SearchQuery",
    "type": "object",
    "properties": {"reject": {"type": "string"}},
    "required": []
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingInstitutionSearchResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/StudyFundingInstitutionShortProfile",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "code": {"type": "string"},
          "name": {"type": "string"},
          "type": {"type": "string"},
          "committeeId": {"type": "object", "description": "the associated committee ID"},
          "legalEntityId": {"type": "object", "description": "the associated legal entity ID"},
          "status": {"type": "string"},
          "address": {
            "id": "/Address",
            "type": "object",
            "properties": {
              "streetAddress": {"type": "string"},
              "locality": {"type": "string"},
              "region": {"type": "string"},
              "postalCode": {"type": "string"},
              "extendedAddress": {"type": "array", "items": {"type": "string"}},
              "countryName": {"type": "string"}
            },
            "required": []
          },
          "institutionPayee": {
            "id": "/InstitutionPayee",
            "properties": {
              "id": {"type": "object"},
              "name": {"type": ["string", "null"]},
              "address": {
                "id": "/Address",
                "type": "object",
                "properties": {
                  "streetAddress": {"type": "string"},
                  "locality": {"type": "string"},
                  "region": {"type": "string"},
                  "postalCode": {"type": "string"},
                  "extendedAddress": {"type": "array", "items": {"type": "string"}},
                  "countryName": {"type": "string"}
                },
                "required": []
              },
              "contact": {
                "properties": {
                  "userId": {"type": ["object", "null"]},
                  "name": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phones": {"type": "array", "items": {"type": "string"}}
                },
                "required": []
              },
              "invoiceDisplayValues": {
                "type": "array",
                "items": {
                  "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
                  "required": ["label", "value"]
                }
              },
              "invoiceCCEmails": {"type": "array", "items": {"type": "string"}},
              "daysToPay": {"type": "number"}
            },
            "required": []
          }
        },
        "required": ["id", "code", "name", "type", "status", "address"]
      }
    }
  }
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Searches for institutions whose name matches the search string. Returns the payee information as well as the institution short profile

### HTTP Request

`GET /funding/institution-search/:searchString?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingInvoiceList - <em>Get Study Funding Invoices</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/invoices"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/StudyFundingInvoiceListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "payeeIds": {"type": ["string", "array"], "description": "an array of payee institution IDs"},
      "committeeIds": {"type": ["string", "array"], "description": "an array of committee IDs"},
      "payeeLinked": {
        "type": "string",
        "enum": ["notLinked", "linked", "all"],
        "description": "an array of payee institution IDs"
      }
    }
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingInvoiceListResponse",
  "type": "object",
  "properties": {
    "meta": {
      "id": "/ListMeta",
      "properties": {
        "count": {"type": "number"},
        "limit": {"type": "number"},
        "offset": {"type": "number"}
      },
      "required": ["count", "limit", "offset"]
    },
    "data": {
      "type": "array",
      "items": {
        "id": "StudyFundingInvoiceListProfile",
        "properties": {
          "id": {"type": "object"},
          "studyFundingId": {"type": "object"},
          "studyId": {"type": "object"},
          "fundingNumber": {"type": "string"},
          "projectIdNumber": {"type": "number"},
          "feeScheduleId": {"type": "object"},
          "isVoid": {"type": "boolean"},
          "reb": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
            "required": ["name"]
          },
          "institutions": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
              "required": ["name"]
            }
          },
          "payee": {
            "id": "StudyFundingPaymentPayee",
            "properties": {
              "id": {"type": "object"},
              "name": {"type": ["string", "null"]},
              "address": {
                "id": "/Address",
                "type": "object",
                "properties": {
                  "streetAddress": {"type": "string"},
                  "locality": {"type": "string"},
                  "region": {"type": "string"},
                  "postalCode": {"type": "string"},
                  "extendedAddress": {"type": "array", "items": {"type": "string"}},
                  "countryName": {"type": "string"}
                },
                "required": []
              },
              "contact": {
                "properties": {
                  "userId": {"type": ["object", "null"]},
                  "name": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phones": {"type": "array", "items": {"type": "string"}}
                },
                "required": []
              },
              "invoiceDisplayValues": {
                "type": "array",
                "items": {
                  "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
                  "required": ["label", "value"]
                }
              },
              "invoiceCCEmails": {"type": "array", "items": {"type": "string"}},
              "daysToPay": {"type": "number"}
            },
            "required": []
          },
          "invoiceNumber": {"type": "string"},
          "invoiceShortNumber": {"type": "number"},
          "legacyInvoiceNumber": {"type": "string"},
          "condition": {"type": "string"},
          "conditionLabel": {"type": "string"},
          "description": {"type": "string"},
          "value": {"type": ["number", "string", "null"]},
          "isHstExempt": {"type": "boolean"},
          "subTotal": {"type": "number"},
          "hst": {"type": "number"},
          "total": {"type": "number"},
          "totalPaid": {"type": "number"},
          "lastSentDt": {"type": "date"},
          "isSendRequired": {"type": "boolean"},
          "rebPaymentAmount": {"type": "number"},
          "rebPaymentId": {"type": "object"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "studyFundingId",
          "studyId",
          "fundingNumber",
          "projectIdNumber",
          "feeScheduleId",
          "isVoid",
          "reb",
          "institutions",
          "payee",
          "invoiceNumber",
          "invoiceShortNumber",
          "condition",
          "conditionLabel",
          "description",
          "value",
          "isHstExempt",
          "subTotal",
          "hst",
          "total",
          "isSendRequired",
          "totalPaid",
          "createDt",
          "updateDt"
        ]
      }
    }
  },
  "required": ["meta", "data"]
}
```


Gets a listing of study funding invoices in the system that the current user can access.

### HTTP Request

`GET /funding/invoices`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingInvoiceSearch - <em>Search Invoices</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/invoice-search/:searchString?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/SearchParams",
    "type": "object",
    "properties": {"searchString": {"type": "string"}},
    "required": []
  },
  "query": {
    "id": "/SearchQuery",
    "type": "object",
    "properties": {"reject": {"type": "string"}},
    "required": []
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingInvoiceSearchResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "StudyFundingInvoiceSearchProfile",
        "properties": {
          "id": {"type": "object"},
          "studyFundingId": {"type": "object"},
          "studyId": {"type": "object"},
          "projectIdNumber": {"type": "number"},
          "isVoid": {"type": "boolean"},
          "payee": {
            "properties": {"id": {"type": "object"}, "name": {"type": ["string", "null"]}},
            "required": ["name"]
          },
          "condition": {"type": "string"},
          "conditionLabel": {"type": "string"},
          "description": {"type": "string"},
          "invoiceNumber": {"type": "string"},
          "invoiceShortNumber": {"type": "number"},
          "legacyInvoiceNumber": {"type": "string"},
          "total": {"type": "number"},
          "totalPaid": {"type": "number"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "studyFundingId",
          "studyId",
          "projectIdNumber",
          "payee",
          "isVoid",
          "condition",
          "conditionLabel",
          "description",
          "invoiceNumber",
          "invoiceShortNumber",
          "total",
          "totalPaid",
          "createDt",
          "updateDt"
        ]
      }
    }
  }
}
```


Searches for invoices with the invoice number

### HTTP Request

`GET /funding/invoice-search/:searchString?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingInvoiceUpdateTotal - <em>Study Funding Update Invoice Total</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/funding/invoices/:invoiceId/update-total"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {"properties": {"invoiceId": {"type": "string"}}, "required": ["invoiceId"]},
  "body": {
    "id": "StudyFundingInvoiceUpdateTotalBody",
    "type": "object",
    "properties": {"subTotal": {"type": "number"}, "hst": {"type": "number"}},
    "required": ["subTotal", "hst"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Updates an invoice total, should be used only be admin and not be used after payments sent

### HTTP Request

`POST /funding/invoices/:invoiceId/update-total`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## StudyFundingList - <em>Get Study Fundings</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/StudyFundingListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "payeeIds": {"type": ["string", "array"], "description": "an array of payee institution IDs"},
      "payeeLinked": {
        "type": "string",
        "enum": ["notLinked", "linked", "all"],
        "description": "an array of payee institution IDs"
      },
      "committeeIds": {"type": ["string", "array"], "description": "an array of committee IDs"}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingListResponse",
  "type": "object",
  "properties": {
    "meta": {
      "id": "/ListMeta",
      "properties": {
        "count": {"type": "number"},
        "limit": {"type": "number"},
        "offset": {"type": "number"}
      },
      "required": ["count", "limit", "offset"]
    },
    "data": {
      "type": "array",
      "items": {
        "id": "StudyFundingListProfile",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "studyId": {"type": "object"},
          "fundingNumber": {"type": "string"},
          "projectIdNumber": {"type": "number"},
          "isFeesApplicable": {"type": "boolean"},
          "isHstExempt": {"type": "boolean"},
          "reb": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
            "required": ["name"]
          },
          "payee": {
            "properties": {"id": {"type": "object"}, "name": {"type": ["string", "null"]}},
            "required": ["name"]
          },
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"},
          "totalInvoiced": {"type": "number"},
          "totalPaid": {"type": "number"},
          "invoiceCount": {"type": "number"}
        },
        "required": [
          "id",
          "studyId",
          "fundingNumber",
          "projectIdNumber",
          "isFeesApplicable",
          "isHstExempt",
          "reb",
          "payee",
          "createDt",
          "updateDt",
          "totalInvoiced",
          "totalPaid",
          "invoiceCount"
        ]
      }
    }
  }
}
```


Gets a listing of study fundings in the system that the current user can access.

### HTTP Request

`GET /funding/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingPayeeUpdate - <em>Update Study Funding Payee</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/funding/:studyFundingId/payee"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingParams",
    "type": "object",
    "properties": {"studyFundingId": {"type": "string"}},
    "required": ["studyFundingId"]
  },
  "body": {
    "id": "/StudyFundingPayeeBody",
    "properties": {
      "institutionId": {"type": "string"},
      "name": {"type": "string"},
      "address": {
        "id": "/PayeeAddress",
        "type": "object",
        "properties": {
          "streetAddress": {"type": "string", "description": "Street address"},
          "extendedAddress": {
            "type": "array",
            "items": {"type": "string"},
            "minItems": 0,
            "maxItems": 5
          },
          "postalCode": {"type": "string", "maxLength": 10},
          "locality": {"type": "string"},
          "region": {"type": "string"},
          "countryName": {"type": "string"}
        },
        "required": []
      },
      "contact": {
        "properties": {
          "name": {"type": "string"},
          "phones": {"type": "array", "items": {"type": "string"}},
          "email": {"type": "string"}
        },
        "required": ["email"]
      },
      "invoiceDisplayValues": {
        "type": "array",
        "description": "if omitted, defaults from the linked institution will be used.",
        "items": {
          "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
          "required": ["label", "value"]
        }
      },
      "invoiceCCEmails": {
        "type": "array",
        "description": "if omitted, defaults from the linked institution will be used.",
        "items": {"type": "string"}
      },
      "daysToPay": {
        "type": "number",
        "description": "if omitted, defaults from the linked institution will be used."
      }
    },
    "required": ["name"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Updates the Payee information for one study funding record

### HTTP Request

`PUT /funding/:studyFundingId/payee`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingPaymentDelete - <em>Delete a Study Funding Payment</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/funding/payments/:paymentId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingPaymentProfileParams",
    "type": "object",
    "properties": {"paymentId": {"type": "string"}},
    "required": ["paymentId"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Deletes a payment.  Payments cannot be deleted if REB payouts have already happened.

### HTTP Request

`DELETE /funding/payments/:paymentId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingPaymentList - <em>Get Study Funding Payments List</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/payments"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/StudyFundingPaymentListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "payeeIds": {"type": ["string", "array"], "description": "an array of payee institution IDs"},
      "payeeLinked": {
        "type": "string",
        "enum": ["notLinked", "linked", "all"],
        "description": "whether to include linked payees or not"
      },
      "paymentType": {
        "type": "string",
        "enum": ["all", "reb", "sponsor", "institution"],
        "description": "The payment type to filter by"
      }
    }
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingPaymentListResponse",
  "type": "object",
  "properties": {
    "meta": {
      "id": "/ListMeta",
      "properties": {
        "count": {"type": "number"},
        "limit": {"type": "number"},
        "offset": {"type": "number"}
      },
      "required": ["count", "limit", "offset"]
    },
    "data": {
      "type": "array",
      "items": {
        "id": "/StudyFundingPaymentShortProfile",
        "properties": {
          "id": {"type": "object"},
          "paymentType": {"type": "string", "enum": ["reb", "sponsor", "institution"]},
          "paymentNumber": {"type": "string"},
          "paymentReference": {"type": "string"},
          "quickBooksId": {"type": "string"},
          "paymentDt": {"type": "date-time"},
          "isVoid": {"type": "boolean"},
          "totalPayment": {"type": "number"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"},
          "payee": {
            "id": "StudyFundingPaymentPayee",
            "properties": {
              "id": {"type": "object"},
              "name": {"type": ["string", "null"]},
              "address": {
                "id": "/Address",
                "type": "object",
                "properties": {
                  "streetAddress": {"type": "string"},
                  "locality": {"type": "string"},
                  "region": {"type": "string"},
                  "postalCode": {"type": "string"},
                  "extendedAddress": {"type": "array", "items": {"type": "string"}},
                  "countryName": {"type": "string"}
                },
                "required": []
              },
              "contact": {
                "properties": {
                  "userId": {"type": ["object", "null"]},
                  "name": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phones": {"type": "array", "items": {"type": "string"}}
                },
                "required": []
              },
              "invoiceDisplayValues": {
                "type": "array",
                "items": {
                  "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
                  "required": ["label", "value"]
                }
              },
              "invoiceCCEmails": {"type": "array", "items": {"type": "string"}},
              "daysToPay": {"type": "number"}
            },
            "required": []
          },
          "invoicePaymentCount": {"type": "number"}
        },
        "required": ["id", "paymentNumber", "totalPayment", "invoicePaymentCount", "isVoid"]
      }
    }
  },
  "required": ["meta", "data"]
}
```


Gets a filterable list of payments recorded in the system

### HTTP Request

`GET /funding/payments`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingPaymentProfile - <em>Gets the full details about one Study Funding Payment</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/payments/:paymentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingPaymentProfileParams",
    "type": "object",
    "properties": {"paymentId": {"type": "string"}},
    "required": ["paymentId"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingPaymentProfileResponse",
  "type": "object",
  "properties": {
    "payment": {
      "id": "StudyFundingPayment",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "paymentType": {"type": "string", "enum": ["reb", "sponsor", "institution"]},
        "paymentNumber": {"type": "string"},
        "paymentReference": {"type": "string"},
        "quickBooksId": {"type": "string"},
        "paymentDt": {"type": "date-time"},
        "isVoid": {"type": "boolean"},
        "totalPayment": {"type": "number"},
        "paymentReason": {"type": "string", "enum": ["legacy", "full", "hard", "manual"]},
        "createUserId": {"type": ["object", "null"]},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"},
        "payee": {
          "id": "StudyFundingPaymentPayee",
          "properties": {
            "id": {"type": "object"},
            "name": {"type": ["string", "null"]},
            "address": {
              "id": "/Address",
              "type": "object",
              "properties": {
                "streetAddress": {"type": "string"},
                "locality": {"type": "string"},
                "region": {"type": "string"},
                "postalCode": {"type": "string"},
                "extendedAddress": {"type": "array", "items": {"type": "string"}},
                "countryName": {"type": "string"}
              },
              "required": []
            },
            "contact": {
              "properties": {
                "userId": {"type": ["object", "null"]},
                "name": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phones": {"type": "array", "items": {"type": "string"}}
              },
              "required": []
            },
            "invoiceDisplayValues": {
              "type": "array",
              "items": {
                "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
                "required": ["label", "value"]
              }
            },
            "invoiceCCEmails": {"type": "array", "items": {"type": "string"}},
            "daysToPay": {"type": "number"}
          },
          "required": []
        },
        "invoicePayments": {
          "type": "array",
          "items": {
            "properties": {
              "studyId": {"type": "object"},
              "studyFundingId": {"type": "object"},
              "invoiceId": {"type": "object"},
              "invoiceNumber": {"type": "string"},
              "invoiceShortNumber": {"type": "number"},
              "condition": {"type": "string"},
              "conditionLabel": {"type": "string"},
              "description": {"type": "string"},
              "projectIdNumber": {"type": "number"},
              "fundingNumber": {"type": "string"},
              "paymentAmount": {"type": "number"},
              "total": {"type": "number"},
              "totalPaid": {"type": "number"}
            },
            "required": [
              "studyId",
              "studyFundingId",
              "invoiceId",
              "invoiceNumber",
              "invoiceShortNumber",
              "condition",
              "conditionLabel",
              "description",
              "projectIdNumber",
              "fundingNumber",
              "paymentAmount"
            ]
          }
        },
        "history": {
          "type": "array",
          "items": {
            "properties": {
              "actionDt": {"type": "date"},
              "action": {
                "type": "string",
                "enum": [
                  "void",
                  "payeeUpdate",
                  "create",
                  "updateTotal",
                  "sendInitial",
                  "sendReminder",
                  "sendUpdate",
                  "document_create",
                  "document_update",
                  "institution_add",
                  "institution_update",
                  "payment_reb_create",
                  "payment_reb_update",
                  "payment_reb_delete",
                  "payment_institution_create",
                  "payment_institution_update",
                  "payment_institution_delete",
                  "payment_sponsor_create",
                  "payment_sponsor_update",
                  "payment_sponsor_delete"
                ]
              },
              "reason": {"type": "string"},
              "userId": {"type": "object"}
            },
            "required": ["actionDt", "action", "reason"]
          }
        }
      },
      "required": [
        "id",
        "paymentType",
        "paymentNumber",
        "totalPayment",
        "isVoid",
        "createDt",
        "paymentReason",
        "updateDt",
        "history",
        "invoicePayments"
      ]
    }
  },
  "required": ["payment"]
}
```


Gets the full details about one Study Funding Payment

### HTTP Request

`GET /funding/payments/:paymentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingPaymentSave - <em>Record or update a Study Funding Payment</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/funding/payments/:paymentId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/StudyFundingPaymentBody",
    "type": "object",
    "properties": {
      "paymentDt": {"type": "date-time"},
      "totalPayment": {"type": "number"},
      "paymentReference": {"type": "string"},
      "quickBooksId": {"type": "string"},
      "payee": {
        "properties": {
          "institutionId": {"type": "string"},
          "name": {"type": "string"},
          "address": {
            "id": "/PayeeAddress",
            "type": "object",
            "properties": {
              "streetAddress": {"type": "string", "description": "Street address"},
              "extendedAddress": {
                "type": "array",
                "items": {"type": "string"},
                "minItems": 0,
                "maxItems": 5
              },
              "postalCode": {"type": "string", "maxLength": 10},
              "locality": {"type": "string"},
              "region": {"type": "string"},
              "countryName": {"type": "string"}
            },
            "required": []
          },
          "contact": {
            "properties": {
              "name": {"type": "string"},
              "phone": {"type": "string"},
              "email": {"type": "string"}
            },
            "required": []
          }
        }
      },
      "invoicePayments": {
        "type": "array",
        "items": {
          "properties": {"invoiceId": {"type": "string"}, "paymentAmount": {"type": "number"}},
          "required": ["invoiceId", "paymentAmount"]
        }
      }
    },
    "required": ["paymentDt", "totalPayment", "payee", "invoicePayments"]
  },
  "params": {
    "id": "/StudyFundingPaymentParams",
    "type": "object",
    "properties": {"paymentId": {"type": "string"}},
    "required": []
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Records or updates a payment.  To update a payment, pass the paymentId as part of the request.  
        If any invoices are marked as void, an error is returned
        If any invoice will be overpaid from the invoice payments, an error is returned

### HTTP Request

`POST /funding/payments/:paymentId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingPayments - <em>Get Study Funding Payments</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/:studyFundingId/payments"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingParams",
    "type": "object",
    "properties": {"studyFundingId": {"type": "string"}},
    "required": ["studyFundingId"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingPaymentsResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "StudyFundingPayment",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "paymentType": {"type": "string", "enum": ["reb", "sponsor", "institution"]},
          "paymentNumber": {"type": "string"},
          "paymentReference": {"type": "string"},
          "quickBooksId": {"type": "string"},
          "paymentDt": {"type": "date-time"},
          "isVoid": {"type": "boolean"},
          "totalPayment": {"type": "number"},
          "paymentReason": {"type": "string", "enum": ["legacy", "full", "hard", "manual"]},
          "createUserId": {"type": ["object", "null"]},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"},
          "payee": {
            "id": "StudyFundingPaymentPayee",
            "properties": {
              "id": {"type": "object"},
              "name": {"type": ["string", "null"]},
              "address": {
                "id": "/Address",
                "type": "object",
                "properties": {
                  "streetAddress": {"type": "string"},
                  "locality": {"type": "string"},
                  "region": {"type": "string"},
                  "postalCode": {"type": "string"},
                  "extendedAddress": {"type": "array", "items": {"type": "string"}},
                  "countryName": {"type": "string"}
                },
                "required": []
              },
              "contact": {
                "properties": {
                  "userId": {"type": ["object", "null"]},
                  "name": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phones": {"type": "array", "items": {"type": "string"}}
                },
                "required": []
              },
              "invoiceDisplayValues": {
                "type": "array",
                "items": {
                  "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
                  "required": ["label", "value"]
                }
              },
              "invoiceCCEmails": {"type": "array", "items": {"type": "string"}},
              "daysToPay": {"type": "number"}
            },
            "required": []
          },
          "invoicePayments": {
            "type": "array",
            "items": {
              "properties": {
                "studyId": {"type": "object"},
                "studyFundingId": {"type": "object"},
                "invoiceId": {"type": "object"},
                "invoiceNumber": {"type": "string"},
                "invoiceShortNumber": {"type": "number"},
                "condition": {"type": "string"},
                "conditionLabel": {"type": "string"},
                "description": {"type": "string"},
                "projectIdNumber": {"type": "number"},
                "fundingNumber": {"type": "string"},
                "paymentAmount": {"type": "number"},
                "total": {"type": "number"},
                "totalPaid": {"type": "number"}
              },
              "required": [
                "studyId",
                "studyFundingId",
                "invoiceId",
                "invoiceNumber",
                "invoiceShortNumber",
                "condition",
                "conditionLabel",
                "description",
                "projectIdNumber",
                "fundingNumber",
                "paymentAmount"
              ]
            }
          },
          "history": {
            "type": "array",
            "items": {
              "properties": {
                "actionDt": {"type": "date"},
                "action": {
                  "type": "string",
                  "enum": [
                    "void",
                    "payeeUpdate",
                    "create",
                    "updateTotal",
                    "sendInitial",
                    "sendReminder",
                    "sendUpdate",
                    "document_create",
                    "document_update",
                    "institution_add",
                    "institution_update",
                    "payment_reb_create",
                    "payment_reb_update",
                    "payment_reb_delete",
                    "payment_institution_create",
                    "payment_institution_update",
                    "payment_institution_delete",
                    "payment_sponsor_create",
                    "payment_sponsor_update",
                    "payment_sponsor_delete"
                  ]
                },
                "reason": {"type": "string"},
                "userId": {"type": "object"}
              },
              "required": ["actionDt", "action", "reason"]
            }
          }
        },
        "required": [
          "id",
          "paymentType",
          "paymentNumber",
          "totalPayment",
          "isVoid",
          "createDt",
          "paymentReason",
          "updateDt",
          "history",
          "invoicePayments"
        ]
      }
    }
  },
  "required": ["data"]
}
```


Gets all the payments related to one study funding document

### HTTP Request

`GET /funding/:studyFundingId/payments`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingProfile - <em>Get Study Funding Profile</em>


```shell
curl "https://ctoregistry.com/api/v1/funding/:studyFundingId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyFundingParams",
    "type": "object",
    "properties": {"studyFundingId": {"type": "string"}},
    "required": ["studyFundingId"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFundingProfileResponse",
  "type": "object",
  "properties": {
    "studyFunding": {
      "id": "StudyFunding",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "studyId": {"type": "object"},
        "fundingNumber": {"type": "string"},
        "projectIdNumber": {"type": "number"},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"},
        "reb": {
          "type": "object",
          "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
          "required": ["name"]
        },
        "payee": {
          "id": "StudyFundingPayee",
          "properties": {
            "id": {"type": "object"},
            "name": {"type": ["string", "null"]},
            "address": {
              "id": "/Address",
              "type": "object",
              "properties": {
                "streetAddress": {"type": "string"},
                "locality": {"type": "string"},
                "region": {"type": "string"},
                "postalCode": {"type": "string"},
                "extendedAddress": {"type": "array", "items": {"type": "string"}},
                "countryName": {"type": "string"}
              },
              "required": []
            },
            "contact": {
              "properties": {
                "userId": {"type": ["object", "null"]},
                "name": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phones": {"type": "array", "items": {"type": "string"}}
              },
              "required": []
            },
            "invoiceDisplayValues": {
              "type": "array",
              "items": {
                "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
                "required": ["label", "value"]
              }
            },
            "invoiceCCEmails": {"type": "array", "items": {"type": "string"}},
            "daysToPay": {"type": "number"}
          },
          "required": []
        },
        "fees": {
          "id": "StudyFundingFees",
          "properties": {
            "feeScheduleId": {"type": "object"},
            "isFeesApplicable": {"type": "boolean"},
            "feeScheduleName": {"type": "string"},
            "isHstExempt": {"type": "boolean"},
            "hstExemptionDocument": {
              "id": "/StudyFundingDocument",
              "properties": {
                "id": {"type": "object"},
                "name": {"type": "string"},
                "originalFilename": {"type": "string"},
                "link": {"type": "string"},
                "mimeType": {"type": "string"},
                "size": {"type": "number"},
                "uploadDt": {"type": "date"}
              },
              "required": ["id", "originalFilename", "uploadDt", "link", "mimeType", "size"]
            },
            "invoiceProcessingMethod": {"type": "string"},
            "invoices": {
              "type": "array",
              "items": {
                "id": "StudyFundingInvoice",
                "properties": {
                  "id": {"type": "object"},
                  "feesId": {"type": "object"},
                  "feesName": {"type": "string"},
                  "feesDt": {"type": "date"},
                  "isVoid": {"type": "boolean"},
                  "isSendRequired": {"type": "boolean"},
                  "isNewInvoiceDocumentRequired": {"type": "boolean"},
                  "rebDaysToPayout": {"type": "number"},
                  "rebPaymentAmount": {"type": "number"},
                  "rebPaymentId": {"type": "object"},
                  "invoiceNumber": {"type": "string"},
                  "invoiceShortNumber": {"type": "number"},
                  "legacyInvoiceNumber": {"type": "string"},
                  "condition": {"type": "string"},
                  "conditionLabel": {"type": "string"},
                  "description": {"type": "string"},
                  "value": {"type": ["number", "string", "null"]},
                  "isHstExempt": {"type": "boolean"},
                  "subTotal": {"type": "number"},
                  "hst": {"type": "number"},
                  "total": {"type": "number"},
                  "totalPaid": {"type": "number"},
                  "lastSentDt": {"type": "date"},
                  "invoiceDocuments": {
                    "type": "array",
                    "items": {
                      "id": "StudyFundingInvoiceDocument",
                      "properties": {
                        "id": {"type": "object"},
                        "name": {"type": "string"},
                        "originalFilename": {"type": "string"},
                        "link": {"type": "string"},
                        "mimeType": {"type": "string"},
                        "size": {"type": "number"},
                        "uploadDt": {"type": "date"},
                        "sentDts": {"type": "array", "items": {"type": "date"}},
                        "documentVersion": {"type": "number"},
                        "isSendRequired": {"type": "boolean"}
                      },
                      "required": [
                        "id",
                        "originalFilename",
                        "uploadDt",
                        "link",
                        "mimeType",
                        "size",
                        "sentDts",
                        "documentVersion",
                        "isSendRequired"
                      ]
                    }
                  },
                  "institutions": {
                    "type": "array",
                    "items": {
                      "properties": {
                        "centreApplicationId": {"type": "object"},
                        "institutionId": {"type": "object"},
                        "name": {"type": "string"},
                        "paymentId": {"type": "object"},
                        "paymentAmount": {"type": "number"}
                      },
                      "required": ["centreApplicationId", "name"]
                    }
                  },
                  "payments": {
                    "type": "array",
                    "items": {
                      "properties": {
                        "paymentId": {"type": "object"},
                        "paymentAmount": {"type": "number"}
                      },
                      "required": ["paymentId", "paymentId"]
                    }
                  },
                  "history": {
                    "type": "array",
                    "items": {
                      "properties": {
                        "actionDt": {"type": "date"},
                        "action": {
                          "type": "string",
                          "enum": [
                            "void",
                            "payeeUpdate",
                            "create",
                            "updateTotal",
                            "sendInitial",
                            "sendReminder",
                            "sendUpdate",
                            "document_create",
                            "document_update",
                            "institution_add",
                            "institution_update",
                            "payment_reb_create",
                            "payment_reb_update",
                            "payment_reb_delete",
                            "payment_institution_create",
                            "payment_institution_update",
                            "payment_institution_delete",
                            "payment_sponsor_create",
                            "payment_sponsor_update",
                            "payment_sponsor_delete"
                          ]
                        },
                        "reason": {"type": "string"},
                        "userId": {"type": "object"}
                      },
                      "required": ["actionDt", "action", "reason"]
                    }
                  },
                  "createDt": {"type": "date"},
                  "updateDt": {"type": "date"}
                },
                "required": [
                  "id",
                  "feesId",
                  "feesName",
                  "feesDt",
                  "isVoid",
                  "isSendRequired",
                  "isNewInvoiceDocumentRequired",
                  "invoiceNumber",
                  "invoiceShortNumber",
                  "condition",
                  "conditionLabel",
                  "description",
                  "value",
                  "isHstExempt",
                  "subTotal",
                  "hst",
                  "total",
                  "totalPaid",
                  "institutions",
                  "history",
                  "createDt",
                  "updateDt"
                ]
              }
            }
          },
          "required": [
            "feeScheduleId",
            "feeScheduleName",
            "isFeesApplicable",
            "isHstExempt",
            "invoiceProcessingMethod",
            "invoices"
          ]
        }
      },
      "required": [
        "id",
        "studyId",
        "fundingNumber",
        "projectIdNumber",
        "reb",
        "createDt",
        "updateDt",
        "payee",
        "fees"
      ]
    }
  },
  "required": ["studyFunding"]
}
```


Gets the full information about one study funding document.

### HTTP Request

`GET /funding/:studyFundingId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingRecalculateInvoices - <em>Study Funding Recalculate Invoices</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/funding/:studyFundingId/recalculate-invoices"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyParams",
    "type": "object",
    "properties": {"studyId": {"type": "string"}},
    "required": ["studyId"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Processes the study funding to update an missing invoices. Does the same actions that the hourly process does for one study

### HTTP Request

`PUT /funding/:studyFundingId/recalculate-invoices`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingSavePaymentSentDt - <em>Study Funding Save Payment Sent Date</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/funding/payments/:paymentId/record-sent-date"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {"properties": {"paymentId": {"type": "string"}}, "required": ["paymentId"]},
  "body": {
    "id": "StudyFundingSavePaymentSentDtBody",
    "type": "object",
    "properties": {"sentDt": {"type": "string", "format": "date-time"}},
    "required": ["sentDt"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Records the date that an payment was sent/received on

### HTTP Request

`POST /funding/payments/:paymentId/record-sent-date`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingSendInvoice - <em>Study Funding Send Invoice Email</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/funding/invoices/:invoiceId/send"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {"properties": {"invoiceId": {"type": "string"}}, "required": ["invoiceId"]},
  "body": {
    "id": "StudyFundingSendInvoiceRequestBody",
    "type": "object",
    "properties": {
      "sendEmail": {"type": "boolean"},
      "sentDt": {"type": "string", "format": "date-time"},
      "invoiceDocumentId": {"type": "string"},
      "subject": {"type": "string"},
      "ccMyself": {"type": "boolean"},
      "extraText": {"type": "string"}
    },
    "required": ["invoiceDocumentId", "sendEmail", "subject"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Emails the document version to the payee for the study funding

### HTTP Request

`POST /funding/invoices/:invoiceId/send`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A

## StudyFundingVoidInvoice - <em>Study Funding Void Invoice</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/funding/invoices/:invoiceId/void"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {"properties": {"invoiceId": {"type": "string"}}, "required": ["invoiceId"]},
  "body": {
    "id": "StudyFundingVoidInvoiceBody",
    "type": "object",
    "properties": {"voidReason": {"type": "string"}},
    "required": ["voidReason"]
  }
}
```


> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Sets an invoice to void status

### HTTP Request

`PUT /funding/invoices/:invoiceId/void`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A