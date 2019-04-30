
# QuickSTART


## QuickSTARTApproval - <em>QuickSTART Site Add / Update Approvals</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/approvals/:approvalId/enter-approval"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteApprovalParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "approvalId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "approvalId"]
  },
  "body": {
    "id": "/QuickSTARTApprovalBody",
    "type": "object",
    "properties": {
      "password": {"type": "string"},
      "doneDt": {"type": "string"},
      "notes": {"type": "string"}
    },
    "required": ["doneDt", "password"]
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


Updates or creates an approval record for a quickSTART site.

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/approvals/:approvalId/enter-approval`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | approver | quickStartSite|The user must be assigned to the specific approval.

## QuickSTARTApprovalCreation - <em>QuickSTART Site Create Approval</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/approvals"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTApprovalBody",
    "type": "object",
    "properties": {
      "userId": {"type": "string"},
      "dueDay": {"type": "integer", "minimum": 1, "maximum": 90},
      "type": {
        "type": "string",
        "enum": ["overall", "protocol", "budget", "contract", "signatures", "resource", "other"]
      },
      "typeOther": {"type": ["string", "null"]},
      "action": {"type": "string"}
    },
    "required": ["userId", "dueDay", "type", "action"]
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


Creates an approval record for a quickSTART site.

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/approvals`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
quickStartSite | approver | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTApprovalUpdate - <em>QuickSTART Site Add / Update Approvals</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/approvals/:approvalId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteApprovalUpdateParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "approvalId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "approvalId"]
  },
  "body": {
    "id": "/QuickSTARTApprovalBody",
    "type": "object",
    "properties": {
      "userId": {"type": "string"},
      "dueDay": {"type": "integer", "minimum": 1, "maximum": 90},
      "type": {
        "type": "string",
        "enum": ["overall", "protocol", "budget", "contract", "signatures", "resource", "other"]
      },
      "typeOther": {"type": ["string", "null"]},
      "action": {"type": "string"}
    },
    "required": ["userId", "dueDay", "type", "action"]
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


Updates or creates an approval record for a quickSTART site.

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/approvals/:approvalId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
quickStartSite | approver | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTApprovalsList - <em>QuickSTART Site Approvals</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/approvals"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickStartApprovalsResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/QuickStartApproval",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "type": {
            "type": "string",
            "enum": ["overall", "protocol", "budget", "contract", "signatures", "resource", "other"]
          },
          "typeOther": {"type": ["string", "null"]},
          "action": {"type": "string"},
          "assignedDt": {"type": "date"},
          "createUserId": {"type": "object"},
          "assignedUserId": {"type": "object"},
          "signUserId": {"type": "object"},
          "dueDay": {"type": "integer", "minimum": 1, "maximum": 90},
          "dueDt": {"type": "date"},
          "doneDt": {"type": "date"},
          "approvalNotes": {"type": "string"},
          "daysLeft": {"type": ["number", "null"]},
          "daysToComplete": {"type": ["number", "null"]},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "type",
          "action",
          "createUserId",
          "assignedUserId",
          "assignedDt",
          "dueDay",
          "dueDt",
          "createDt",
          "updateDt"
        ]
      }
    }
  },
  "required": ["data"]
}
```


Updates or creates an approval record for a quickSTART site.

### HTTP Request

`GET /quick-start/:quickStartId/sites/:institutionId/approvals`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | * | quickStart|N/A
quickStartSite | * | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTCreation - <em>QuickSTART Creation</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/QuickSTARTCreationRequestBody",
    "type": "object",
    "properties": {
      "shortTitle": {"type": "string"},
      "sponsorInstitutionId": {"type": "string"},
      "sponsorUserIds": {
        "type": "array",
        "minItems": 1,
        "uniqueItems": true,
        "items": {"type": "string"}
      },
      "sponsorContractUserId": {"type": ["string", "null"]},
      "sponsorBudgetUserId": {"type": ["string", "null"]},
      "studyType": {"type": "string"},
      "studyTypeOther": {"type": ["string", "null"]},
      "therapeuticArea": {"type": "string"},
      "quickStartIdentifier": {"type": ["string", "null"]},
      "projectIdNumber": {"type": ["string", "null"]},
      "status": {"type": "string", "enum": ["pending", "screen", "active", "completed"]}
    },
    "required": [
      "shortTitle",
      "sponsorInstitutionId",
      "sponsorUserIds",
      "sponsorContractUserId",
      "sponsorBudgetUserId",
      "therapeuticArea",
      "studyType",
      "quickStartIdentifier"
    ]
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


Creates a new QuickSTART application in the system.

### HTTP Request

`POST /quick-start/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | quickStartSponsor | N/A|The data can only include the target institution as the sponsor institution.

## QuickSTARTDocumentDelete - <em>Delete an QuickSTART Document</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/documents/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTDocumentDelete",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "documentId": {"type": "string"}},
    "required": ["quickStartId", "documentId"]
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


Deletes a specified document from an QuickSTART application

### HTTP Request

`DELETE /quick-start/:quickStartId/documents/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTDocumentDownload - <em>Download QuickSTART Document</em>


```shell
curl "https://ctoregistry.com/api/v1/download/quick-start/:quickStartId/documents/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTDocumentDownload",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "documentId": {"type": "string"}},
    "required": ["quickStartId", "documentId"]
  }
}
```


> Response Schema

```json
undefined
```


Downloads one document from the specified QuickSTART application.

### HTTP Request

`GET /download/quick-start/:quickStartId/documents/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | * | quickStart|N/A
quickStartSite | * | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTDocumentUpload - <em>Upload QuickSTART Document</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/upload/quick-start/:quickStartId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/QuickSTARTDocumentUpload",
    "type": "object",
    "properties": {
      "type": {
        "type": "string",
        "description": "The document type",
        "enum": ["protocol", "budget", "contract", "add_protocol", "add_budget", "add_contract"]
      },
      "subType": {"type": "string", "description": "The document sub type"},
      "subTypeOther": {"type": "string", "description": "The document sub type (other specify)"},
      "documentId": {
        "type": "string",
        "description": "optional document Id, will update this document record if passed in"
      }
    },
    "required": ["type"]
  },
  "params": {
    "id": "/QuickSTARTDocumentUploadParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}},
    "required": ["quickStartId"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickSTARTDocumentUploadResponse",
  "type": "object",
  "properties": {
    "document": {
      "id": "/QuickStartDocument",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "type": {"type": "string"},
        "subType": {"type": "string"},
        "subTypeOther": {"type": "string"},
        "uploadDt": {"type": "date"},
        "link": {"type": "string"},
        "mimeType": {"type": "string"},
        "size": {"type": "number"},
        "originalFilename": {"type": "string"},
        "uploadUserId": {"type": "object"}
      },
      "required": ["id", "type", "uploadDt", "link", "mimeType", "originalFilename", "uploadUserId"]
    }
  },
  "required": ["document"]
}
```


Uploads a document to the specified QuickSTART application.  The document information is contained in the POST

### HTTP Request

`POST /upload/quick-start/:quickStartId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTExtraDocumentDelete - <em>QuickSTART Site Pre Screen Document Delete</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/extra-documents/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTExtraDocumentDeleteParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "documentId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "documentId"]
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


Deletes an extra document from a quickSTART site.  The document associated must already be uploaded

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/extra-documents/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTExtraDocumentSave - <em>QuickSTART Site Save Extra Document</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/extra-documents"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTExtraDocumentBody",
    "type": "object",
    "properties": {
      "documentId": {"type": "string"},
      "category": {"type": "string", "enum": ["screen", "review", "active"]},
      "type": {"type": "string", "enum": ["budget", "contract", "protocol"]},
      "visibility": {"type": "array", "items": {"type": "string", "enum": ["site", "sponsor"]}},
      "name": {"type": "string"}
    },
    "required": ["category", "type", "name"]
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


Updates or creates an extra document for a QuickSTART site.  The document associated must already be uploaded

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/extra-documents`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTExtraDocumentUpload - <em>Upload QuickSTART Extra Document</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/upload/quick-start/:quickStartId/sites/:institutionId/extra-documents"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTExtraDocumentUpload",
    "properties": {
      "category": {
        "type": "string",
        "description": "The document type",
        "enum": ["screen", "review", "active"]
      },
      "type": {
        "type": "string",
        "description": "The document type",
        "enum": ["budget", "contract", "protocol"]
      }
    },
    "required": ["type"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickSTARTDocumentUploadResponse",
  "type": "object",
  "properties": {
    "document": {
      "id": "/QuickStartDocument",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "type": {"type": "string"},
        "subType": {"type": "string"},
        "subTypeOther": {"type": "string"},
        "uploadDt": {"type": "date"},
        "link": {"type": "string"},
        "mimeType": {"type": "string"},
        "size": {"type": "number"},
        "originalFilename": {"type": "string"},
        "uploadUserId": {"type": "object"}
      },
      "required": ["id", "type", "uploadDt", "link", "mimeType", "originalFilename", "uploadUserId"]
    }
  },
  "required": ["document"]
}
```


Uploads an extra document to the specified QuickSTART Site application.  The document information is contained in the POST

### HTTP Request

`POST /upload/quick-start/:quickStartId/sites/:institutionId/extra-documents`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTList - <em>QuickSTART List</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/QuickSTARTListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/QuickStartListResponse",
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
        "id": "/QuickStartShortProfile",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "quickStartIdentifier": {"type": "string"},
          "status": {"type": "string", "enum": ["pending", "screen", "active", "completed"]},
          "shortTitle": {"type": "string"},
          "sponsorInstitutionId": {"type": "object"},
          "studyType": {"type": "string"},
          "studyTypeOther": {"type": "string"},
          "projectIdNumber": {"type": "number"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"},
          "sites": {"type": "array"}
        },
        "required": [
          "id",
          "quickStartIdentifier",
          "status",
          "shortTitle",
          "studyType",
          "createDt",
          "updateDt"
        ]
      }
    }
  }
}
```


Gets the list of all QuickSTART study applications that the user can access.

### HTTP Request

`GET /quick-start/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | quickStartSponsor | N/A|The data is filtered to only include QuickSTART and QuickSTART sites that the target institution is listed as the sponsor.
quickStart | * | N/A|The data is filtered to only include QuickSTART and QuickSTART site applications that the user is participating on.
quickStartSite | * | N/A|The data is filtered to only include QuickSTART and QuickSTART site applications that the user is participating on.

## QuickSTARTProfile - <em>QuickSTART Profile</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/:quickStartId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}},
    "required": ["quickStartId"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickStartProfileResponse",
  "type": "object",
  "properties": {
    "quickStart": {
      "type": "object",
      "id": "/QuickStartProfile",
      "properties": {
        "id": {"type": "object"},
        "quickStartIdentifier": {"type": "string"},
        "shortTitle": {"type": "string"},
        "studyType": {"type": "string"},
        "studyTypeOther": {"type": "string"},
        "therapeuticArea": {"type": "string"},
        "projectIdNumber": {"type": "number"},
        "studyId": {"type": "object"},
        "status": {"type": "string", "enum": ["pending", "screen", "active", "completed"]},
        "protocol": {
          "id": "/QuickStartProtocol",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "version": {"type": "string"},
            "versionDt": {"type": "date"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "version", "versionDt"]
        },
        "budget": {
          "id": "/QuickStartBudget",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "version": {"type": "string"},
            "versionDt": {"type": "date"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "version", "versionDt"]
        },
        "contract": {
          "id": "/QuickStartContract",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "version": {"type": "string"},
            "versionDt": {"type": "date"},
            "strategy": {"type": "string"},
            "strategyOther": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "version", "versionDt", "strategy"]
        },
        "documents": {
          "type": "array",
          "items": {
            "id": "/QuickStartDocument",
            "type": "object",
            "properties": {
              "id": {"type": "object"},
              "type": {"type": "string"},
              "subType": {"type": "string"},
              "subTypeOther": {"type": "string"},
              "uploadDt": {"type": "date"},
              "link": {"type": "string"},
              "mimeType": {"type": "string"},
              "size": {"type": "number"},
              "originalFilename": {"type": "string"},
              "uploadUserId": {"type": "object"}
            },
            "required": [
              "id",
              "type",
              "uploadDt",
              "link",
              "mimeType",
              "originalFilename",
              "uploadUserId"
            ]
          }
        }
      },
      "required": ["id", "quickStartIdentifier", "shortTitle", "studyType", "therapeuticArea"]
    },
    "sponsor": {
      "type": "object",
      "id": "/QuickStartSponsor",
      "properties": {
        "institutionId": {"type": "object"},
        "code": {"type": "string"},
        "name": {"type": "string"}
      },
      "required": ["institutionId", "code", "name"]
    },
    "sponsorUsers": {
      "type": "array",
      "items": {
        "id": "/UserShortProfile",
        "properties": {
          "id": {"type": "object"},
          "username": {"type": "string"},
          "contact": {
            "type": "object",
            "properties": {
              "firstName": {"type": "string"},
              "middleName": {"type": "string"},
              "lastName": {"type": "string"},
              "title": {
                "type": "string",
                "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
              }
            },
            "required": ["firstName", "lastName", "title"]
          },
          "institutionIds": {"type": "array", "items": {"type": "object"}}
        },
        "required": ["id", "username", "contact", "institutionIds"]
      },
      "minItems": 1
    },
    "sponsorContractUser": {
      "id": "/UserShortProfile",
      "properties": {
        "id": {"type": "object"},
        "username": {"type": "string"},
        "contact": {
          "type": "object",
          "properties": {
            "firstName": {"type": "string"},
            "middleName": {"type": "string"},
            "lastName": {"type": "string"},
            "title": {
              "type": "string",
              "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
            }
          },
          "required": ["firstName", "lastName", "title"]
        },
        "institutionIds": {"type": "array", "items": {"type": "object"}}
      },
      "required": ["id", "username", "contact", "institutionIds"]
    },
    "sponsorBudgetUser": {
      "id": "/UserShortProfile",
      "properties": {
        "id": {"type": "object"},
        "username": {"type": "string"},
        "contact": {
          "type": "object",
          "properties": {
            "firstName": {"type": "string"},
            "middleName": {"type": "string"},
            "lastName": {"type": "string"},
            "title": {
              "type": "string",
              "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
            }
          },
          "required": ["firstName", "lastName", "title"]
        },
        "institutionIds": {"type": "array", "items": {"type": "object"}}
      },
      "required": ["id", "username", "contact", "institutionIds"]
    }
  },
  "required": ["quickStart", "sponsor", "sponsorUsers"]
}
```


Gets one data record for an QuickSTART application using it's ID.

### HTTP Request

`GET /quick-start/:quickStartId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | * | quickStart|N/A
quickStartSite | * | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSendToSite - <em>QuickSTART Send to Site</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/send-to-site"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
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


Sends a QuickSTART pre-screened application to the Site

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/send-to-site`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteAddUser - <em>QuickSTART Site Add User</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/users"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTSiteAddUserBody",
    "type": "object",
    "properties": {
      "userId": {"type": "string"},
      "roles": {
        "type": "array",
        "items": {
          "type": "string",
          "enum": ["contract", "budget", "investigator", "rc", "readonly"]
        }
      }
    },
    "required": ["userId", "roles"]
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


Adds a user to a QuickSTART site with the specified roles.  Will update existing users if present

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/users`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A
quickStart | sponsor | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A
quickStartSite | contract | quickStartSite|The user can only specify a role that they currently have.                        The user can only give themselves the read only role
quickStartSite | budget | quickStartSite|The user can only specify a role that they currently have.                        The user can only give themselves the read only role
quickStartSite | approver | quickStartSite|The user can only give themselves the read only role

## QuickSTARTSiteCompletePreScreen - <em>QuickSTART Complete Pre-Screen</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/pre-screen/complete"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
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


Marks a QuickSTART Site Pre-Screen as complete by CTO

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/pre-screen/complete`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

## QuickSTARTSiteCreation - <em>QuickSTART Site Creation</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteCreationParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}},
    "required": ["quickStartId"]
  },
  "body": {
    "id": "/QuickSTARTSiteCreationRequestBody",
    "type": "object",
    "properties": {
      "institutionId": {"type": "string"},
      "researchCoordinatorId": {"type": "string"},
      "principalInvestigatorId": {"type": "string"}
    },
    "required": ["institutionId", "researchCoordinatorId"]
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


Adds a new site to an existing QuickSTART application

### HTTP Request

`POST /quick-start/:quickStartId/sites`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteDocumentDelete - <em>Delete an QuickSTART Document</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/documents/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTDocumentDelete",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "documentId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "documentId"]
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


Deletes a specified document from an QuickSTART application

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/documents/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteDocumentDownload - <em>Download QuickSTART Document</em>


```shell
curl "https://ctoregistry.com/api/v1/download/quick-start/:quickStartId/sites/:institutionId/documents/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteDocumentDownload",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "documentId": {"type": "string"},
      "institutionId": {"type": "string"}
    },
    "required": ["quickStartId", "documentId", "institutionId"]
  }
}
```


> Response Schema

```json
undefined
```


Downloads one document from the specified QuickSTART application.

### HTTP Request

`GET /download/quick-start/:quickStartId/sites/:institutionId/documents/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | * | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A
quickStartSite | * | quickStartSite|N/A

## QuickSTARTSiteDocumentUpload - <em>Upload QuickSTART Document</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/upload/quick-start/:quickStartId/sites/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTSiteDocumentUpload",
    "type": "object",
    "properties": {
      "type": {
        "type": "string",
        "description": "The document type",
        "enum": ["protocol", "budget", "contract", "add_protocol", "add_budget", "add_contract"]
      },
      "subType": {"type": "string", "description": "The document sub type"},
      "subTypeOther": {"type": "string", "description": "The document sub type (other specify)"},
      "documentId": {
        "type": "string",
        "description": "optional document Id, will update this document record if passed in"
      }
    },
    "required": ["type"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickSTARTDocumentUploadResponse",
  "type": "object",
  "properties": {
    "document": {
      "id": "/QuickStartDocument",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "type": {"type": "string"},
        "subType": {"type": "string"},
        "subTypeOther": {"type": "string"},
        "uploadDt": {"type": "date"},
        "link": {"type": "string"},
        "mimeType": {"type": "string"},
        "size": {"type": "number"},
        "originalFilename": {"type": "string"},
        "uploadUserId": {"type": "object"}
      },
      "required": ["id", "type", "uploadDt", "link", "mimeType", "originalFilename", "uploadUserId"]
    }
  },
  "required": ["document"]
}
```


Uploads a document to the specified QuickSTART application.  The document information is contained in the POST

### HTTP Request

`POST /upload/quick-start/:quickStartId/sites/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSitePreScreenComment - <em>QuickSTART Site Pre-Screen Comment</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/pre-screen/comments"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTPreScreenCommentBody",
    "type": "object",
    "properties": {
      "comment": {"type": "string"},
      "area": {
        "type": "string",
        "enum": [
          "title",
          "study_type",
          "therapeutic_area",
          "sponsor",
          "roster",
          "protocol",
          "protocol_notes",
          "protocol_document",
          "protocol_add_document",
          "contract",
          "contract_strategy",
          "contract_notes",
          "contract_document",
          "contract_add_document",
          "budget",
          "budget_notes",
          "budget_document",
          "budget_add_document",
          "overall",
          "other"
        ]
      },
      "commentId": {"type": "string"},
      "status": {"type": "string", "enum": ["unresolved", "resolved"]}
    },
    "required": ["comment", "area"]
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


Adds or updates a comment on a QuickSTART Site Pre-Screen

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/pre-screen/comments`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

## QuickSTARTSitePreScreenCommentDelete - <em>QuickSTART Site Pre-Screen Comment</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/pre-screen/comments/:commentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTPreScreenCommentDeleteParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "commentId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "commentId"]
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


Adds a comment to a QuickSTART Site to Pre-Screen

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/pre-screen/comments/:commentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

## QuickSTARTSitePreScreenComments - <em>Get QuickSTART Site Pre-Screen Comments</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/pre-screen/comments"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickStartPreScreenCommentsResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/QuickStartPreScreenComment",
        "properties": {
          "id": {"type": "object"},
          "commentUserId": {
            "type": "object",
            "description": "The Id of the user that created this comment"
          },
          "resolveUserId": {
            "type": "object",
            "description": "The Id of the user that resolved or responded to this comment"
          },
          "isSystemComment": {"type": "boolean"},
          "status": {"type": "string", "enum": ["unresolved", "resolved"]},
          "comment": {"type": "string"},
          "area": {
            "type": "string",
            "enum": [
              "title",
              "study_type",
              "therapeutic_area",
              "sponsor",
              "roster",
              "protocol",
              "protocol_notes",
              "protocol_document",
              "protocol_add_document",
              "contract",
              "contract_strategy",
              "contract_notes",
              "contract_document",
              "contract_add_document",
              "budget",
              "budget_notes",
              "budget_document",
              "budget_add_document",
              "overall",
              "other"
            ]
          },
          "createDt": {"type": "date"}
        },
        "required": ["id", "commentUserId", "status", "comment", "area", "createDt"]
      }
    }
  },
  "required": ["data"]
}
```


Gets all comments for a QuickSTART Site Pre-Screen

### HTTP Request

`GET /quick-start/:quickStartId/sites/:institutionId/pre-screen/comments`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteProfile - <em>QuickSTART Site</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickStartSiteResponse",
  "type": "object",
  "properties": {
    "quickStartSite": {
      "type": "object",
      "id": "/QuickStartSiteProfile",
      "properties": {
        "id": {"type": "object"},
        "studyId": {"type": "object"},
        "institutionId": {"type": "object"},
        "researchCoordinatorId": {"type": "object"},
        "principalInvestigatorId": {"type": "object"},
        "readOnlyUserIds": {"type": "array", "items": {"type": "object"}},
        "status": {
          "type": "string",
          "enum": ["pending", "screen", "review", "active", "completed"]
        },
        "useProtocolDefaults": {"type": "boolean"},
        "useContractDefaults": {"type": "boolean"},
        "useBudgetDefaults": {"type": "boolean"},
        "times": {
          "id": "/QuickStartSiteTimes",
          "type": "object",
          "properties": {"active": {"type": "number"}, "toComplete": {"type": "number"}},
          "required": ["active", "toComplete"]
        },
        "approvals": {
          "type": "object",
          "properties": {
            "timerStartDt": {"type": "date"},
            "timerCompleteDt": {"type": "date"},
            "actualCompleteDt": {"type": "date"},
            "contract": {
              "id": "/QuickStartSiteReview",
              "type": "object",
              "properties": {
                "reviewerUserId": {"type": "object"},
                "documentSentDt": {"type": "date"},
                "assignedDt": {"type": "date"},
                "status": {
                  "type": "string",
                  "enum": ["pending", "comment", "response", "approved"]
                },
                "history": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "id": "/QuickStartSiteApprovalHistory",
                    "properties": {
                      "state": {"type": "string"},
                      "status": {
                        "type": "string",
                        "enum": ["pending", "comment", "response", "approved"]
                      },
                      "userId": {"type": "object"},
                      "action": {
                        "type": "string",
                        "enum": ["comment", "approve", "response", "assign"]
                      },
                      "comment": {"type": "string"},
                      "actionDt": {"type": "date"}
                    },
                    "required": ["status", "action", "actionDt"]
                  }
                },
                "rounds": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "site": {
                        "properties": {
                          "action": {"type": ["string", "null"]},
                          "status": {"type": ["string", "null"]},
                          "dueDt": {"type": "date"},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]}
                        },
                        "required": ["dueDt", "startDt"]
                      },
                      "sponsor": {
                        "properties": {
                          "action": {"type": ["string", "null"]},
                          "status": {"type": ["string", "null"]},
                          "dueDt": {"type": "date"},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]}
                        },
                        "required": ["dueDt", "startDt"]
                      }
                    },
                    "required": ["site"]
                  }
                }
              },
              "required": ["status", "rounds"]
            },
            "budget": {
              "id": "/QuickStartSiteReview",
              "type": "object",
              "properties": {
                "reviewerUserId": {"type": "object"},
                "documentSentDt": {"type": "date"},
                "assignedDt": {"type": "date"},
                "status": {
                  "type": "string",
                  "enum": ["pending", "comment", "response", "approved"]
                },
                "history": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "id": "/QuickStartSiteApprovalHistory",
                    "properties": {
                      "state": {"type": "string"},
                      "status": {
                        "type": "string",
                        "enum": ["pending", "comment", "response", "approved"]
                      },
                      "userId": {"type": "object"},
                      "action": {
                        "type": "string",
                        "enum": ["comment", "approve", "response", "assign"]
                      },
                      "comment": {"type": "string"},
                      "actionDt": {"type": "date"}
                    },
                    "required": ["status", "action", "actionDt"]
                  }
                },
                "rounds": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "site": {
                        "properties": {
                          "action": {"type": ["string", "null"]},
                          "status": {"type": ["string", "null"]},
                          "dueDt": {"type": "date"},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]}
                        },
                        "required": ["dueDt", "startDt"]
                      },
                      "sponsor": {
                        "properties": {
                          "action": {"type": ["string", "null"]},
                          "status": {"type": ["string", "null"]},
                          "dueDt": {"type": "date"},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]}
                        },
                        "required": ["dueDt", "startDt"]
                      }
                    },
                    "required": ["site"]
                  }
                }
              },
              "required": ["status", "rounds"]
            }
          }
        },
        "protocol": {
          "id": "/QuickStartProtocol",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "version": {"type": "string"},
            "versionDt": {"type": "date"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "version", "versionDt"]
        },
        "budget": {
          "id": "/QuickStartBudget",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "version": {"type": "string"},
            "versionDt": {"type": "date"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "version", "versionDt"]
        },
        "contract": {
          "id": "/QuickStartContract",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "version": {"type": "string"},
            "versionDt": {"type": "date"},
            "strategy": {"type": "string"},
            "strategyOther": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "version", "versionDt", "strategy"]
        },
        "documents": {
          "type": "array",
          "items": {
            "id": "/QuickStartDocument",
            "type": "object",
            "properties": {
              "id": {"type": "object"},
              "type": {"type": "string"},
              "subType": {"type": "string"},
              "subTypeOther": {"type": "string"},
              "uploadDt": {"type": "date"},
              "link": {"type": "string"},
              "mimeType": {"type": "string"},
              "size": {"type": "number"},
              "originalFilename": {"type": "string"},
              "uploadUserId": {"type": "object"}
            },
            "required": [
              "id",
              "type",
              "uploadDt",
              "link",
              "mimeType",
              "originalFilename",
              "uploadUserId"
            ]
          }
        },
        "extraDocuments": {
          "type": "array",
          "items": {
            "id": "/QuickStartExtraDocument",
            "type": "object",
            "properties": {
              "id": {"type": "object"},
              "type": {"type": "string", "enum": ["budget", "contract", "protocol"]},
              "category": {"type": "string", "enum": ["screen", "review", "active"]},
              "uploadDt": {"type": "date"},
              "link": {"type": "string"},
              "mimeType": {"type": "string"},
              "size": {"type": "number"},
              "originalFilename": {"type": "string"},
              "uploadUserId": {"type": "object"},
              "visibility": {
                "type": "array",
                "items": {"type": "string", "enum": ["site", "sponsor"]}
              },
              "name": {}
            },
            "required": [
              "id",
              "type",
              "category",
              "uploadDt",
              "link",
              "mimeType",
              "originalFilename",
              "uploadUserId",
              "name"
            ]
          }
        }
      },
      "required": [
        "id",
        "institutionId",
        "researchCoordinatorId",
        "status",
        "useProtocolDefaults",
        "useContractDefaults",
        "useBudgetDefaults",
        "approvals",
        "protocol",
        "budget",
        "contract"
      ]
    },
    "institution": {
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
          "required": ["streetAddress", "locality", "region", "postalCode"]
        }
      },
      "required": ["id", "code", "name", "type", "status", "address"]
    },
    "centreApplication": {
      "type": "object",
      "id": "/QuickStartSiteCentreApplication",
      "properties": {
        "status": {
          "type": "string",
          "enum": [
            "Active",
            "Completed",
            "Expired",
            "None",
            "Not Approved",
            "Pending",
            "Suspended",
            "Terminated",
            "Withdrawn"
          ]
        },
        "initialApprovalDt": {"type": "date"},
        "initialReviewType": {"type": "string"},
        "createDt": {"type": "date"}
      },
      "required": ["status", "createDt"]
    },
    "study": {
      "type": "object",
      "id": "QuickStartSiteStudy",
      "properties": {
        "status": {
          "type": "string",
          "enum": [
            "Active",
            "Completed",
            "Expired",
            "None",
            "Not Approved",
            "Pending",
            "Suspended",
            "Terminated",
            "Withdrawn"
          ]
        },
        "initialApprovalDt": {"type": ["date"]},
        "initialReviewType": {
          "type": ["string"],
          "enum": ["Full Board Review", "Delegated Review", "Admin Review"]
        },
        "createDt": {"type": "date"},
        "history": {
          "type": "array",
          "items": {
            "type": "object",
            "id": "QuickStartSiteStudyHistory",
            "properties": {
              "applicationType": {"type": "string", "enum": ["PIA", "CIA", "OPIA", "OCIA"]},
              "event": {"type": "string"},
              "eventDt": {"type": "date"}
            },
            "required": ["applicationType", "event", "eventDt"]
          }
        }
      },
      "required": ["status", "createDt"]
    }
  },
  "required": ["quickStartSite", "institution"]
}
```


Gets all the info related to one site on the quickStart application.

### HTTP Request

`GET /quick-start/:quickStartId/sites/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | * | quickStart|N/A
quickStartSite | * | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteRecordSentDt - <em>QuickSTART Site Record Document Sent Date</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/record-sent-date"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTSiteRecordSentDtBody",
    "type": "object",
    "properties": {
      "type": {"type": "string", "enum": ["budget", "contract"]},
      "documentSentDt": {"type": "string", "format": "date-time"}
    },
    "required": ["type", "documentSentDt"]
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


Updates an existing QuickSTART Site with the.

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/record-sent-date`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A

## QuickSTARTSiteRemoveUser - <em>QuickSTART Site Remove User</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/users/:userId/role/:role"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteRemoveUserParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "userId": {"type": "string"},
      "role": {"type": "string", "enum": ["readonly"]}
    },
    "required": ["quickStartId", "institutionId", "userId", "role"]
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


Removes a Read-Only user from a QuickSTART site.  All other users must be managed through adding and replacing.

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/users/:userId/role/:role`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|The user can only specify a role that they currently have.
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteResponse - <em>QuickSTART Site Response</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/response"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTSiteResponseBody",
    "type": "object",
    "properties": {
      "type": {"type": "string", "enum": ["budget", "contract"]},
      "comment": {"type": "string"}
    },
    "required": ["type", "comment"]
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


Submit a sponsor response for one section of data for a QuickSTART site

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/response`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartAdmin | quickStart|N/A

## QuickSTARTSiteRestore - <em>QuickSTART Site Restore Defaults</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/restore-defaults/:section"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteRestoreParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "section": {"type": "string", "enum": ["protocol", "contract", "budget"]}
    },
    "required": ["quickStartId", "institutionId", "section"]
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


Updates an existing QuickSTART Site portion to use the defaults from the overall application.

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/restore-defaults/:section`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteReview - <em>QuickSTART Site Review</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/review"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickSTARTSiteReviewBody",
    "type": "object",
    "properties": {
      "type": {"type": "string", "enum": ["budget", "contract"]},
      "action": {"type": "string", "enum": ["comment", "approve"]},
      "comment": {"type": "string"}
    },
    "required": ["type", "action"]
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


Submit a review for one section of data for a QuickSTART site

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/review`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | budget | quickStartSite|The user must be assigned to the specific approval.
quickStartSite | contract | quickStartSite|The user must be assigned to the specific approval.

## QuickSTARTSiteSendToPreScreen - <em>QuickSTART Site Send to Pre-Screen</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/pre-screen"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
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


Sends a QuickSTART Site to Pre-Screen with CTO

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/pre-screen`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteUpdate - <em>QuickSTART Site Update</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {"id": "/QuickSTARTSiteUpdateBody", "type": "object", "required": []}
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


Updates an existing QuickSTART Site portion of an application in the system.

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSites - <em>QuickSTART Sites</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}},
    "required": ["quickStartId"]
  }
}
```


> Response Schema

```json
{
  "id": "/QuickStartSitesResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "id": "/QuickStartSiteShortProfile",
        "properties": {
          "id": {"type": "object"},
          "institutionId": {"type": "object"},
          "researchCoordinatorId": {"type": "object"},
          "principalInvestigatorId": {"type": "object"},
          "institution": {
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
                "required": ["streetAddress", "locality", "region", "postalCode"]
              }
            },
            "required": ["id", "code", "name", "type", "status", "address"]
          },
          "status": {
            "type": "string",
            "enum": ["pending", "screen", "review", "active", "completed"]
          },
          "times": {
            "id": "/QuickStartSiteTimes",
            "type": "object",
            "properties": {"active": {"type": "number"}, "toComplete": {"type": "number"}},
            "required": ["active", "toComplete"]
          },
          "approvals": {
            "type": "object",
            "properties": {
              "timerStartDt": {"type": "date"},
              "timerCompleteDt": {"type": "date"},
              "actualCompleteDt": {"type": "date"}
            }
          }
        },
        "required": ["id", "institutionId", "institution", "researchCoordinatorId", "status"]
      }
    }
  },
  "required": ["data"]
}
```


Gets all the basic info related to the sites on the quickStart application.

### HTTP Request

`GET /quick-start/:quickStartId/sites`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | * | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A
quickStartSite | * | quickStart|The data is filtered to only include QuickSTART and QuickSTART site applications that the user is participating on.

## QuickSTARTUpdate - <em>QuickSTART Update</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTUpdateParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}},
    "required": ["quickStartId"]
  },
  "body": {
    "id": "/QuickSTARTUpdateBody",
    "type": "object",
    "properties": {
      "quickStartSiteId": {
        "type": "string",
        "description": "If passed along with content, the site will be updated instead of the overall QuickSTART application"
      }
    },
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


Updates an existing QuickSTART application in the system.

### HTTP Request

`PUT /quick-start/:quickStartId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickStartCheckUniqueProjectIdNumber - <em>Check QuickSTART unique stream project Id number</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/unique-project-id-number/:projectIdNumber/:quickStartId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTUniqueProjectIdNumberParams",
    "type": "object",
    "properties": {"projectIdNumber": {"type": "string"}, "quickStartId": {"type": "string"}},
    "required": ["projectIdNumber"]
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


Checks to see if a QuickSTART stream project Id number is already in use or not.

### HTTP Request

`GET /quick-start/unique-project-id-number/:projectIdNumber/:quickStartId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | N/A|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | N/A|N/A

## QuickStartCheckUniqueQuickStartIdentifier - <em>Check QuickSTART unique Identifier</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/unique-quick-start-identifier/:quickStartIdentifier/:quickStartId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTUniqueQuickStartIdentifierParams",
    "type": "object",
    "properties": {"quickStartIdentifier": {"type": "string"}, "quickStartId": {"type": "string"}},
    "required": ["quickStartIdentifier"]
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


Checks to see if a QuickSTART Identifier is already in use or not.

### HTTP Request

`GET /quick-start/unique-quick-start-identifier/:quickStartIdentifier/:quickStartId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | N/A|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | N/A|N/A

## QuickStartCheckUniqueShortTitle - <em>Check QuickSTART unique short title</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start/unique-short-title/:shortTitle/:quickStartId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickSTARTUniqueShortTitleParams",
    "type": "object",
    "properties": {"shortTitle": {"type": "string"}, "quickStartId": {"type": "string"}},
    "required": ["shortTitle"]
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


Checks to see if a QuickSTART short title is already in use or not.

### HTTP Request

`GET /quick-start/unique-short-title/:shortTitle/:quickStartId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | N/A|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
institution | quickStartSponsor | N/A|N/A