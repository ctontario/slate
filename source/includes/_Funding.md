
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
      "type": {"type": "string", "enum": ["fundingHstExemption"]},
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
      "type": {"type": "string", "enum": ["fundingHstExemption"]},
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
      "type": {"type": "string", "enum": ["fundingHstExemption"]}
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
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]}
                },
                "required": []
              }
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
      "isSendRequired": {
        "type": "boolean",
        "description": "set to true to only return invoices that must be sent"
      },
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
          "projectIdNumber": {"type": "number"},
          "feeScheduleId": {"type": "object"},
          "reb": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
            "required": ["name"]
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
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]}
                },
                "required": []
              }
            },
            "required": []
          },
          "invoiceNumber": {"type": "string"},
          "legacyInvoiceNumber": {"type": "string"},
          "condition": {"type": "string"},
          "value": {"type": ["number", "string", "null"]},
          "subTotal": {"type": "number"},
          "hst": {"type": "number"},
          "total": {"type": "number"},
          "totalPaid": {"type": "number"},
          "sentDts": {"type": "array", "items": {"type": "date"}},
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
          "projectIdNumber",
          "feeScheduleId",
          "reb",
          "payee",
          "invoiceNumber",
          "condition",
          "value",
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
          "payee": {
            "properties": {"id": {"type": "object"}, "name": {"type": ["string", "null"]}},
            "required": ["name"]
          },
          "invoiceNumber": {"type": "string"},
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
          "invoiceNumber",
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
          "projectIdNumber": {"type": "number"},
          "isFeesApplicable": {"type": "boolean"},
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
          "projectIdNumber",
          "isFeesApplicable",
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
          "firstName": {"type": "string"},
          "lastName": {"type": "string"},
          "phone": {"type": "string"},
          "email": {"type": "string"}
        },
        "required": ["firstName", "lastName", "phone", "email"]
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
      "isSendRequired": {
        "type": "boolean",
        "description": "set to true to only return invoices that must be sent"
      },
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
          "paymentDt": {"type": "date-time"},
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
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]}
                },
                "required": []
              }
            },
            "required": []
          },
          "invoicePaymentCount": {"type": "number"}
        },
        "required": ["id", "paymentNumber", "totalPayment", "invoicePaymentCount"]
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
        "paymentDt": {"type": "date-time"},
        "totalPayment": {"type": "number"},
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
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]}
              },
              "required": []
            }
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
              "condition": {"type": "string"},
              "projectIdNumber": {"type": "number"},
              "paymentAmount": {"type": "number"},
              "total": {"type": "number"},
              "totalPaid": {"type": "number"}
            },
            "required": [
              "studyId",
              "studyFundingId",
              "invoiceId",
              "invoiceNumber",
              "projectIdNumber",
              "paymentAmount"
            ]
          }
        }
      },
      "required": [
        "id",
        "paymentType",
        "paymentNumber",
        "totalPayment",
        "createDt",
        "updateDt",
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
              "firstName": {"type": "string"},
              "lastName": {"type": "string"},
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


Records or updates a payment.  TO update a payment, pass the paymentId as part of the request

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
          "paymentDt": {"type": "date-time"},
          "totalPayment": {"type": "number"},
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
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]}
                },
                "required": []
              }
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
                "condition": {"type": "string"},
                "projectIdNumber": {"type": "number"},
                "paymentAmount": {"type": "number"},
                "total": {"type": "number"},
                "totalPaid": {"type": "number"}
              },
              "required": [
                "studyId",
                "studyFundingId",
                "invoiceId",
                "invoiceNumber",
                "projectIdNumber",
                "paymentAmount"
              ]
            }
          }
        },
        "required": [
          "id",
          "paymentType",
          "paymentNumber",
          "totalPayment",
          "createDt",
          "updateDt",
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
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]}
              },
              "required": []
            }
          },
          "required": []
        },
        "fees": {
          "id": "StudyFundingFees",
          "properties": {
            "feeScheduleId": {"type": "object"},
            "feeScheduleName": {"type": "string"},
            "isFeesApplicable": {"type": "boolean"},
            "hst": {"type": "number"},
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
            "invoices": {
              "type": "array",
              "items": {
                "id": "StudyFundingInvoice",
                "properties": {
                  "id": {"type": "object"},
                  "invoiceNumber": {"type": "string"},
                  "legacyInvoiceNumber": {"type": "string"},
                  "condition": {"type": "string"},
                  "value": {"type": ["number", "string", "null"]},
                  "subTotal": {"type": "number"},
                  "hst": {"type": "number"},
                  "total": {"type": "number"},
                  "totalPaid": {"type": "number"},
                  "isSendRequired": {"type": "boolean"},
                  "sentDts": {"type": "array", "items": {"type": "date"}},
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
                  "createDt": {"type": "date"},
                  "updateDt": {"type": "date"}
                },
                "required": [
                  "id",
                  "invoiceNumber",
                  "condition",
                  "value",
                  "subTotal",
                  "hst",
                  "total",
                  "totalPaid",
                  "institutions",
                  "isSendRequired",
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
            "invoices"
          ]
        }
      },
      "required": [
        "id",
        "studyId",
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

## StudyFundingSaveInvoiceSentDts - <em>Study Funding Save Invoice Sent Dates</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/funding/invoices/:invoiceId/record-sent-dates"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {"properties": {"invoiceId": {"type": "string"}}, "required": ["invoiceId"]},
  "body": {
    "id": "StudyFundingSaveInvoiceSentDtsBody",
    "type": "object",
    "properties": {
      "sentDts": {"type": "array", "items": {"type": "string", "format": "date-time"}},
      "required": ["sentDts"]
    }
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


Records the set of dates that an invoice was sent on

### HTTP Request

`POST /funding/invoices/:invoiceId/record-sent-dates`



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