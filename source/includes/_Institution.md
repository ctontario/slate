
# Institution


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
      "code": {"type": "string", "maxLength": 25, "description": "Code name"},
      "type": {"type": "string", "maxLength": 15, "description": "The institution type"},
      "status": {"type": "string", "enum": ["pending", "active", "deleted", "suspended"]},
      "statusEffectiveChangeDt": {
        "type": "string",
        "description": "The effective date of a change of status"
      },
      "loadStreamUsers": {
        "type": "boolean",
        "description": "Whether to load users from stream or not"
      },
      "legalEntityId": {
        "type": "string",
        "description": "The ID of the legal entity institution, used if the institution is grouped under one legal entity"
      },
      "committeeId": {
        "type": "string",
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
        "required": ["streetAddress", "postalCode", "locality", "region", "countryName"]
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
              "enum": [null, "home", "msg", "work", "pref", "fax", "cell", "pager"],
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
system | admin | N/A|N/A
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
      "completeDt": {"type": "date"},
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
system | admin | N/A|N/A
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
            "required": ["streetAddress", "locality", "region", "postalCode"]
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
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
institution | member | N/A|The data is filtered to only include records that match the privilege target.
institution | admin | N/A|The data is filtered to only include records that match the privilege target.

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
        "type": {"type": "string"},
        "status": {"type": "string"},
        "website": {"type": "string"},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"},
        "loadStreamUsers": {"type": "boolean"},
        "committeeId": {"type": "object", "description": "The ID of the associated committee"},
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
                "required": ["streetAddress", "locality", "region", "postalCode"]
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
                      "enum": [null, "home", "msg", "work", "pref", "fax", "cell", "pager"]
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
          "required": ["streetAddress", "locality", "region", "postalCode"]
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


Gets the profile data related to one institution

### HTTP Request

`GET /institution/:institutionId`



### Authorization
 
N/A

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
institution | admin | institution|N/A
institution | member | institution|N/A

## InstitutionSearch - <em>Search Institutions</em>


```shell
curl "https://ctoregistry.com/api/v1/dictionary/institution/:searchString"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/Search",
    "type": "object",
    "properties": {"searchString": {"type": "string"}},
    "required": ["searchString"]
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
            "required": ["streetAddress", "locality", "region", "postalCode"]
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

`GET /dictionary/institution/:searchString`



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
      "code": {"type": "string", "maxLength": 25, "description": "Code name"},
      "type": {"type": "string", "maxLength": 15, "description": "The institution type"},
      "status": {"type": "string", "enum": ["pending", "active", "deleted", "suspended"]},
      "statusEffectiveChangeDt": {
        "type": "string",
        "description": "The effective date of a change of status"
      },
      "loadStreamUsers": {
        "type": "boolean",
        "description": "Whether to load users from stream or not"
      },
      "legalEntityId": {
        "type": "string",
        "description": "The ID of the legal entity institution, used if the institution is grouped under one legal entity"
      },
      "committeeId": {
        "type": "string",
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
        "required": ["streetAddress", "postalCode", "locality", "region", "countryName"]
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
              "enum": [null, "home", "msg", "work", "pref", "fax", "cell", "pager"],
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
institution | admin | institution|N/A