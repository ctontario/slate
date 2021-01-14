
# Institution


## InstitutionCheckUniqueAlternateName - <em>Check if Institution Alternate Name Unique</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/unique-alternate-name/:alternateName/:institutionId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionUniqueAlternateNameParams",
    "type": "object",
    "properties": {"alternateName": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["alternateName"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean"}},
  "required": ["exists"]
}
```


Checks to see if an institution alternate name is already in use or not

### HTTP Request

`GET /institution/unique-alternate-name/:alternateName/:institutionId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | N/A|N/A

## InstitutionCheckUniqueCode - <em>Check if Institution Code Unique</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/unique-code/:code/:institutionId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionUniqueCodeParams",
    "type": "object",
    "properties": {"code": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["code"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean"}},
  "required": ["exists"]
}
```


Checks to see if an institution code is already in use or not

### HTTP Request

`GET /institution/unique-code/:code/:institutionId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | N/A|N/A

## InstitutionCheckUniqueName - <em>Check if Institution Name Unique</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/unique-name/:name/:institutionId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionUniqueNameParams",
    "type": "object",
    "properties": {"name": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["name"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean"}},
  "required": ["exists"]
}
```


Checks to see if an institution name is already in use or not

### HTTP Request

`GET /institution/unique-name/:name/:institutionId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | N/A|N/A

## InstitutionCreation - <em>Create a new institution</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/institution/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/Institution",
    "type": "object",
    "properties": {
      "name": {"type": "string", "maxLength": 200, "description": "Institution name"},
      "alternateNames": {"type": "array", "items": {"type": "string", "maxLength": 200}},
      "code": {"type": "string", "maxLength": 25, "description": "Code name"},
      "type": {"type": "string", "maxLength": 15, "description": "The institution type"},
      "status": {"type": "string", "enum": ["pending", "active", "deleted", "suspended"]},
      "loadStreamUsers": {
        "type": "boolean",
        "description": "Whether to load users from stream or not"
      },
      "isQuickStartReady": {
        "type": "boolean",
        "description": "Whether the institution is ready to participate in the QuickSTART program or not."
      },
      "legalEntityId": {
        "type": ["string", "null"],
        "description": "The ID of the legal entity institution, used if the institution is grouped under one legal entity"
      },
      "committeeId": {
        "type": ["string", "null"],
        "description": "The ID of the committee associated with this institution."
      },
      "website": {"type": "string"},
      "address": {
        "id": "/Address",
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
        "required": ["streetAddress", "postalCode", "locality", "region"]
      },
      "phones": {
        "type": "array",
        "items": {
          "id": "/Phone",
          "type": "object",
          "properties": {
            "number": {"type": "string", "description": "Phone number"},
            "extension": {"type": "string", "description": "The extension"},
            "type": {
              "type": "string",
              "enum": ["home", "msg", "work", "pref", "fax", "cell", "pager"],
              "description": "Phone number type"
            }
          },
          "required": ["number"]
        },
        "minItems": 0,
        "maxItems": 5
      },
      "test": {"type": "boolean"}
    },
    "required": ["name", "code", "address", "phones", "type"]
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


Create a new institution in the system.

### HTTP Request

`POST /institution/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A

## InstitutionDictionary - <em>Institution Dictionary</em>


```shell
curl "https://ctoregistry.com/api/v1/dictionary/institution"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/InstitutionDictionaryResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "code": {"type": "string"},
          "name": {"type": "string"},
          "type": {"type": "string"},
          "typeLabel": {"type": "string"},
          "locality": {"type": "string"},
          "region": {"type": "string"},
          "country": {"type": "string"}
        },
        "required": ["id", "code", "name", "type", "typeLabel", "locality", "region", "country"]
      }
    }
  }
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Gets the list of institutions that are present in the system.

### HTTP Request

`GET /dictionary/institution`



### Authorization
 
N/A

## InstitutionDocumentDelete - <em>Delete an Institution Document</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/institution/:institutionId/documents/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionDocumentDelete",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}, "documentId": {"type": "string"}},
    "required": ["institutionId", "documentId"]
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


Deletes a specified document from an institution document

### HTTP Request

`DELETE /institution/:institutionId/documents/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A

## InstitutionDocumentDownload - <em>Download User Document</em>


```shell
curl "https://ctoregistry.com/api/v1/download/institution/:institutionId/document/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionDocumentDownload",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}, "documentId": {"type": "string"}},
    "required": ["institutionId", "documentId"]
  }
}
```


> Response Schema

```json
undefined
```


Downloads one document from the specified institution.

### HTTP Request

`GET /download/institution/:institutionId/document/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A
institution | admin | institution|N/A
institution | member | institution|N/A

## InstitutionDocumentUpload - <em>Upload Institution Document</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/upload/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/InstitutionDocumentUpload",
    "type": "object",
    "properties": {
      "name": {"type": "string", "description": "The document name"},
      "completeDt": {"type": "string", "format": "date-time"},
      "description": {"type": "string", "description": "The document description"}
    },
    "required": ["name"]
  },
  "params": {
    "id": "/InstitutionDocumentUploadParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/InstitutionDocumentUploadResponse",
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
      "required": ["id", "name", "uploadDt", "completeDt", "originalFilename"]
    }
  }
}
```


Uploads a document to the specified institution.  The document information is contained in the POST

### HTTP Request

`POST /upload/institution/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A

## InstitutionDocuments - <em>Get Institution Documents</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/:institutionId/documents"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/InstitutionDocumentsResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/InstitutionDocument",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "name": {"type": "string"},
          "description": {"type": "string"},
          "filename": {"type": "string"},
          "originalFilename": {"type": "string"},
          "uploadDt": {"type": "date"},
          "completeDt": {"type": "date"}
        },
        "required": ["id", "name", "filename", "originalFilename", "uploadDt", "completeDt"]
      }
    }
  }
}
```


Gets all the documents related to one institution

### HTTP Request

`GET /institution/:institutionId/documents`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A
institution | admin | institution|N/A
institution | member | institution|N/A

## InstitutionList - <em>Get Institutions</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/InstitutionListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "types": {"type": ["string", "array"], "items": {"type": "string"}}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/InstitutionListResponse",
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
        "id": "/InstitutionShortProfile",
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
          }
        },
        "required": ["id", "code", "name", "type", "status", "address"]
      }
    }
  }
}
```


Gets a listing of institutions in the system that the current user can access.

### HTTP Request

`GET /institution/`



### Authorization
 
N/A

## InstitutionPayee - <em>Get Institution Payee</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/:institutionId/payee"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/InstitutionPayeeResponse",
  "type": "object",
  "properties": {
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
  "required": ["institutionPayee"]
}
```


Gets the payee data related to one institution. Payee information is only included for users with the system:admin, system:funding, or system:support roles

### HTTP Request

`GET /institution/:institutionId/payee`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | funding | N/A|N/A

## InstitutionPayeeUpdate - <em>Update Institution Payee</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/institution/:institutionId/payee"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  },
  "body": {
    "id": "/InstitutionPayeeUpdateBody",
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


Updates one institutions payee information in the system

### HTTP Request

`PUT /institution/:institutionId/payee`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | funding | N/A|N/A

## InstitutionProfile - <em>Get Institution</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/InstitutionProfileResponse",
  "type": "object",
  "properties": {
    "institution": {
      "id": "/InstitutionProfile",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "code": {"type": "string"},
        "name": {"type": "string"},
        "alternateNames": {"type": "array", "items": {"type": "string"}},
        "type": {"type": "string"},
        "status": {"type": "string"},
        "website": {"type": "string"},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"},
        "loadStreamUsers": {"type": "boolean"},
        "isQuickStartReady": {"type": "boolean"},
        "committeeId": {"type": "object", "description": "The ID of the associated committee"},
        "legalEntityId": {
          "type": "object",
          "description": "The ID of the associated parent institution"
        },
        "sites": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": {"type": "string"},
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
              "phones": {
                "type": "array",
                "items": {
                  "id": "/Phone",
                  "type": "object",
                  "properties": {
                    "number": {"type": "string"},
                    "extension": {"type": ["string", "null"]},
                    "type": {
                      "type": ["string", "null"],
                      "enum": ["home", "msg", "work", "pref", "fax", "cell", "pager", null]
                    }
                  },
                  "required": ["number", "extension", "type"]
                }
              },
              "required": ["name"]
            }
          }
        }
      },
      "required": [
        "id",
        "code",
        "name",
        "type",
        "status",
        "createDt",
        "updateDt",
        "loadStreamUsers",
        "isQuickStartReady",
        "sites"
      ]
    },
    "legalEntity": {
      "id": "/InstitutionShortProfile",
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
        }
      },
      "required": ["id", "code", "name", "type", "status", "address"]
    },
    "committee": {
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "code": {"type": "string"},
        "name": {"type": "string"},
        "shortName": {"type": "string"}
      },
      "required": ["id", "name", "shortName"]
    }
  },
  "required": ["institution"]
}
```


Gets the profile data related to one institution.

### HTTP Request

`GET /institution/:institutionId`



### Authorization
 
N/A

## InstitutionQuickSTARTApprovalCreation - <em>Institution QuickSTART Create Approval</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/institution/:institutionId/quick-start-approvals"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionQuickSTARTApprovalCreationParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  },
  "body": {
    "id": "/QuickSTARTApprovalBody",
    "type": "object",
    "properties": {
      "userId": {"type": ["string", "null"]},
      "dueDay": {"type": "integer", "minimum": 1},
      "dueType": {"type": "string", "enum": ["fixed", "variable"]},
      "dueAfterEvent": {
        "type": ["string", "null"],
        "enum": [null, "contractApproved", "budgetApproved", "fullApproval"]
      },
      "type": {
        "type": "string",
        "enum": ["overall", "protocol", "budget", "contract", "signatures", "resource", "other"]
      },
      "typeOther": {"type": ["string", "null"]},
      "action": {"type": "string"}
    },
    "required": ["dueDay", "dueType", "dueAfterEvent", "type", "action"]
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


Creates an approval record for this institution to use as a template when creating QuickSTART sites.

### HTTP Request

`POST /institution/:institutionId/quick-start-approvals`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A
institution | quickStartAdmin | institution|N/A

## InstitutionQuickSTARTApprovalDelete - <em>Institution QuickSTART Delete Approval</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/institution/:institutionId/quick-start-approvals/:approvalId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionQuickSTARTApprovalDeleteParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}, "approvalId": {"type": "string"}},
    "required": ["institutionId", "approvalId"]
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


Deletes an approval template record for an Institution.

### HTTP Request

`DELETE /institution/:institutionId/quick-start-approvals/:approvalId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A
institution | quickStartAdmin | institution|N/A

## InstitutionQuickSTARTApprovalUpdate - <em>Institution QuickSTART Update Approval</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/institution/:institutionId/quick-start-approvals/:approvalId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionQuickSTARTApprovalUpdateParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}, "approvalId": {"type": "string"}},
    "required": ["institutionId", "approvalId"]
  },
  "body": {
    "id": "/QuickSTARTApprovalBody",
    "type": "object",
    "properties": {
      "userId": {"type": ["string", "null"]},
      "dueDay": {"type": "integer", "minimum": 1},
      "dueType": {"type": "string", "enum": ["fixed", "variable"]},
      "dueAfterEvent": {
        "type": ["string", "null"],
        "enum": [null, "contractApproved", "budgetApproved", "fullApproval"]
      },
      "type": {
        "type": "string",
        "enum": ["overall", "protocol", "budget", "contract", "signatures", "resource", "other"]
      },
      "typeOther": {"type": ["string", "null"]},
      "action": {"type": "string"}
    },
    "required": ["dueDay", "dueType", "dueAfterEvent", "type", "action"]
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


Updates an approval template record for an Institution.

### HTTP Request

`PUT /institution/:institutionId/quick-start-approvals/:approvalId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A
institution | quickStartAdmin | institution|N/A

## InstitutionQuickSTARTApprovalsList - <em>QuickSTART Site Approvals</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/:institutionId/quick-start-approvals"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/InstitutionQuickStartApprovalsResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/InstitutionQuickStartApproval",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "type": {
            "type": "string",
            "enum": ["overall", "protocol", "budget", "contract", "signatures", "resource", "other"]
          },
          "typeOther": {"type": ["string", "null"]},
          "action": {"type": "string"},
          "createUserId": {"type": "object"},
          "assignedUserId": {"type": "object"},
          "dueType": {"type": "string", "enum": ["fixed", "variable"]},
          "dueAfterEvent": {
            "type": "string",
            "enum": ["contractApproved", "budgetApproved", "fullApproval"]
          },
          "dueDay": {"type": "integer", "minimum": 1},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "type",
          "action",
          "createUserId",
          "dueType",
          "dueDay",
          "createDt",
          "updateDt"
        ]
      }
    }
  },
  "required": ["data"]
}
```


Gets the list of  Quick Start approval templates recorded for the institution

### HTTP Request

`GET /institution/:institutionId/quick-start-approvals`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A
institution | quickStartAdmin | institution|N/A

## InstitutionRoles - <em>Get Institution Roles</em>


```shell
curl "https://ctoregistry.com/api/v1/institution/:institutionId/role"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/InstitutionParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/InstitutionRolesResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
        "required": ["code", "label"]
      }
    }
  }
}
```


Get the list of institution roles allowed for a specific institution

### HTTP Request

`GET /institution/:institutionId/role`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A
institution | member | institution|N/A

## InstitutionSearch - <em>Search Institutions</em>


```shell
curl "https://ctoregistry.com/api/v1/dictionary/institution-search/:searchString?"  
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
  "id": "/InstitutionSearchResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/InstitutionShortProfile",
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
          }
        },
        "required": ["id", "code", "name", "type", "status", "address"]
      }
    }
  }
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Searches for institutions whose name matches the search string.

### HTTP Request

`GET /dictionary/institution-search/:searchString?`



### Authorization
 
N/A

## InstitutionTypes - <em>Get Institution Types</em>


```shell
curl "https://ctoregistry.com/api/v1/dictionary/institution-type"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/InstitutionTypeDictionaryResponse",
  "type": "object",
  "properties": {
    "data": {
      "id": "InstitutionTypeDictionary",
      "patternProperties": {
        "^[a-zA-Z_$][\\w$]*$": {
          "properties": {
            "code": {"type": "string"},
            "label": {"type": "string"},
            "description": {"type": "string"}
          },
          "required": ["code", "label", "description"]
        }
      }
    }
  }
}
```


Get the list of institution types allowed in the system

### HTTP Request

`GET /dictionary/institution-type`



### Authorization
 
N/A

## InstitutionUpdate - <em>Update Institution</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/InstitutionUpdate",
    "type": "object",
    "properties": {
      "name": {"type": "string", "maxLength": 200, "description": "Institution name"},
      "alternateNames": {"type": "array", "items": {"type": "string", "maxLength": 200}},
      "code": {"type": "string", "maxLength": 25, "description": "Code name"},
      "type": {"type": "string", "maxLength": 15, "description": "The institution type"},
      "status": {"type": "string", "enum": ["pending", "active", "deleted", "suspended"]},
      "loadStreamUsers": {
        "type": "boolean",
        "description": "Whether to load users from stream or not"
      },
      "isQuickStartReady": {
        "type": "boolean",
        "description": "Whether the institution is ready to participate in the QuickSTART program or not."
      },
      "legalEntityId": {
        "type": ["string", "null"],
        "description": "The ID of the legal entity institution, used if the institution is grouped under one legal entity"
      },
      "committeeId": {
        "type": ["string", "null"],
        "description": "The ID of the committee associated with this institution."
      },
      "website": {"type": "string"},
      "address": {
        "id": "/Address",
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
        "required": ["streetAddress", "postalCode", "locality", "region"]
      },
      "phones": {
        "type": "array",
        "items": {
          "id": "/Phone",
          "type": "object",
          "properties": {
            "number": {"type": "string", "description": "Phone number"},
            "extension": {"type": "string", "description": "The extension"},
            "type": {
              "type": "string",
              "enum": ["home", "msg", "work", "pref", "fax", "cell", "pager"],
              "description": "Phone number type"
            }
          },
          "required": ["number"]
        },
        "minItems": 0,
        "maxItems": 5
      },
      "test": {"type": "boolean"}
    },
    "required": ["name", "type", "status", "address", "phones"]
  },
  "params": {
    "id": "/InstitutionParams",
    "type": "object",
    "properties": {"institutionId": {"type": "string"}},
    "required": ["institutionId"]
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


Updates one institutions information in the system

### HTTP Request

`PUT /institution/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | institution|N/A