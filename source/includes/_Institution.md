
# Institution


## InstitutionCheckUniqueCode - <em>Check if Institution Code Unique</em>


```shell
curl "https://cto.local:9000/api/v1/institution/unique-code/:code/:institutionId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean", "description": ""}},
  "required": ["exists"]
}
```


Checks to see if an institution code is already in use or not

### HTTP Request

`GET /institution/unique-code/:code/:institutionId?`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | N/A

## InstitutionCheckUniqueName - <em>Check if Institution Name Unique</em>


```shell
curl "https://cto.local:9000/api/v1/institution/unique-name/:name/:institutionId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean", "description": ""}},
  "required": ["exists"]
}
```


Checks to see if an institution name is already in use or not

### HTTP Request

`GET /institution/unique-name/:name/:institutionId?`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | N/A

## InstitutionCreation - <em>Create a new institution</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/institution/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
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
    "legal": {"type": "string"},
    "website": {"type": "string"},
    "address": {
      "id": "/Address",
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
      "minItems": 1,
      "maxItems": 5
    },
    "test": {"type": "boolean"}
  },
  "required": ["name", "code", "address", "phones", "type"]
}
```


> Response Body Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string", "description": ""},
    "action": {"type": "string", "description": ""},
    "id": {"type": "object|null", "description": ""},
    "result": {"type": "object|array|string", "description": ""}
  },
  "required": ["status", "action", "id"]
}
```


Create a new institution in the system.

### HTTP Request

`POST /institution/`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## InstitutionDeleteDocument - <em>Delete an Institution Document</em>


```shell
curl -X DELETE "https://cto.local:9000/api/v1/institution/:institutionId/documents/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string", "description": ""},
    "action": {"type": "string", "description": ""},
    "id": {"type": "object|null", "description": ""},
    "result": {"type": "object|array|string", "description": ""}
  },
  "required": ["status", "action", "id"]
}
```


Deletes a specified document from an institution document

### HTTP Request

`DELETE /institution/:institutionId/documents/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | institution

## InstitutionDictionary - <em>Institution Dictionary</em>


```shell
curl "https://cto.local:9000/api/v1/dictionary/institution"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

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
          "id": {"type": "object", "description": ""},
          "code": {"type": "string", "description": ""},
          "name": {"type": "string", "description": ""},
          "type": {"type": "string", "description": ""},
          "typeLabel": {"type": "string", "description": ""},
          "locality": {"type": "string", "description": ""},
          "region": {"type": "string", "description": ""},
          "country": {"type": "string", "description": ""}
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

## InstitutionDocumentUpload - <em>Upload Institution Document</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/upload/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/InstitutionUploadDocument",
  "type": "object",
  "properties": {
    "name": {"type": "string", "description": "The document name"},
    "completeDt": {"type": "date", "description": ""},
    "description": {"type": "string", "description": "The document description"}
  },
  "required": ["name"]
}
```


> Response Body Schema

```json
{
  "id": "/InstitutionDocumentUploadResponse",
  "type": "object",
  "properties": {
    "document": {
      "type": "object",
      "properties": {
        "id": {"type": "object", "description": ""},
        "name": {"type": "string", "description": ""},
        "uploadDt": {"type": "date", "description": ""},
        "completeDt": {"type": "date", "description": ""},
        "originalFilename": {"type": "string", "description": ""}
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
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | institution

## InstitutionDocuments - <em>Get Institution Documents</em>


```shell
curl "https://cto.local:9000/api/v1/institution/:institutionId/documents"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

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
          "id": {"type": "object", "description": ""},
          "name": {"type": "string", "description": ""},
          "description": {"type": "string", "description": ""},
          "filename": {"type": "string", "description": ""},
          "originalFilename": {"type": "string", "description": ""},
          "uploadDt": {"type": "date", "description": ""},
          "completeDt": {"type": "date", "description": ""}
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
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | institution
institution | member | institution

## InstitutionDownloadDocument - <em>Download User Document</em>


```shell
curl "https://cto.local:9000/api/v1/download/institution/:institutionId/document/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
undefined
```


Downloads a specified document from the specified user.

### HTTP Request

`GET /download/institution/:institutionId/document/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | institution
institution | member | institution

## InstitutionList - <em>Get Institutions</em>


```shell
curl "https://cto.local:9000/api/v1/institution/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/InstitutionListResponse",
  "type": "object",
  "properties": {
    "meta": {
      "id": "/ListMeta",
      "properties": {
        "count": {"type": "number", "description": ""},
        "limit": {"type": "number", "description": ""},
        "offset": {"type": "number", "description": ""}
      },
      "required": ["count", "limit", "offset"]
    },
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object", "description": ""},
          "code": {"type": "string", "description": ""},
          "name": {"type": "string", "description": ""},
          "type": {"type": "string", "description": ""},
          "status": {"type": "string", "description": ""},
          "createDt": {"type": "date", "description": ""},
          "updateDt": {"type": "date", "description": ""}
        },
        "required": ["id", "code", "name", "status", "createDt", "updateDt"]
      }
    }
  }
}
```


Gets a listing of institutions in the system.

### HTTP Request

`GET /institution/`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | member | N/A
institution | admin | N/A

## InstitutionProfile - <em>Get Institution</em>


```shell
curl "https://cto.local:9000/api/v1/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/InstitutionProfileResponse",
  "type": "object",
  "properties": {
    "institution": {
      "id": "/InstitutionProfile",
      "type": "object",
      "properties": {
        "id": {"type": "object", "description": ""},
        "code": {"type": "string", "description": ""},
        "name": {"type": "string", "description": ""},
        "type": {"type": "string", "description": ""},
        "status": {"type": "string", "description": ""},
        "website": {"type": "string", "description": ""},
        "createDt": {"type": "date", "description": ""},
        "updateDt": {"type": "date", "description": ""},
        "loadStreamUsers": {"type": "boolean", "description": ""},
        "sites": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": {"type": "string", "description": ""},
              "address": {
                "id": "/Address",
                "type": "object",
                "properties": {
                  "streetAddress": {"type": "string", "description": ""},
                  "locality": {"type": "string", "description": ""},
                  "region": {"type": "string", "description": ""},
                  "postalCode": {"type": "string", "description": ""},
                  "extendedAddress": {"type": "array", "items": {"type": "string"}},
                  "countryName": {"type": "string", "description": ""}
                },
                "required": ["streetAddress", "locality", "region", "postalCode"]
              },
              "phones": {
                "type": "array",
                "items": {
                  "id": "/Phone",
                  "type": "object",
                  "properties": {
                    "number": {"type": "string", "description": ""},
                    "extension": {"type": "string|null", "description": ""},
                    "type": {
                      "type": "string|null",
                      "description": "",
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
        "id": {"type": "object", "description": ""},
        "code": {"type": "string", "description": ""},
        "name": {"type": "string", "description": ""},
        "type": {"type": "string", "description": ""},
        "address": {
          "id": "/Address",
          "type": "object",
          "properties": {
            "streetAddress": {"type": "string", "description": ""},
            "locality": {"type": "string", "description": ""},
            "region": {"type": "string", "description": ""},
            "postalCode": {"type": "string", "description": ""},
            "extendedAddress": {"type": "array", "items": {"type": "string"}},
            "countryName": {"type": "string", "description": ""}
          },
          "required": ["streetAddress", "locality", "region", "postalCode"]
        }
      },
      "required": ["id", "code", "name", "type", "address"]
    }
  },
  "required": ["institution"]
}
```


Gets all the data related to one institution

### HTTP Request

`GET /institution/:institutionId`



### Authorization
 
N/A

## InstitutionRoles - <em>Get Institution Roles</em>


```shell
curl "https://cto.local:9000/api/v1/institution/:institutionId/role"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/InstitutionRolesResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "code": {"type": "string", "description": ""},
          "label": {"type": "string", "description": ""}
        },
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
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | institution
institution | member | institution

## InstitutionUpdate - <em>Update Institution</em>


```shell
curl -X PUT "https://cto.local:9000/api/v1/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
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
    "legal": {"type": "string"},
    "website": {"type": "string"},
    "address": {
      "id": "/Address",
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
      "minItems": 1,
      "maxItems": 5
    },
    "test": {"type": "boolean"}
  },
  "required": ["name", "type", "status", "address", "phones"]
}
```


> Response Body Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string", "description": ""},
    "action": {"type": "string", "description": ""},
    "id": {"type": "object|null", "description": ""},
    "result": {"type": "object|array|string", "description": ""}
  },
  "required": ["status", "action", "id"]
}
```


Updates one institutions information in the system

### HTTP Request

`PUT /institution/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | institution