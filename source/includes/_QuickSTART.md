
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
    "id": "/QuickStartSiteApprovalParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "approvalId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "approvalId"]
  },
  "body": {
    "id": "/QuickStartApprovalBody",
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


Records the users signature for the approval using their account password.

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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartApprovalBody",
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


Creates an approval record for a quickSTART site. The site must not be completed

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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
quickStartSite | approver | quickStartSite|N/A
quickStartSite | investigator | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTApprovalDelete - <em>QuickSTART Site Delete Approval</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/approvals/:approvalId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteApprovalDeleteParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "approvalId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "approvalId"]
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


Deletes an approval record for a quickSTART site. The site must not be completed

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/approvals/:approvalId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteApprovalUpdateParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "approvalId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "approvalId"]
  },
  "body": {
    "id": "/QuickStartApprovalBody",
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


Updates or creates an approval record for a quickSTART site. The site must not be completed

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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
quickStartSite | approver | quickStartSite|N/A
quickStartSite | investigator | quickStartSite|N/A
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
    "id": "/QuickStartSiteParams",
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
          "dueType": {"type": "string", "enum": ["fixed", "variable"]},
          "dueAfterEvent": {
            "type": "string",
            "enum": ["contractApproved", "budgetApproved", "fullApproval"]
          },
          "dueDay": {"type": "integer", "minimum": 1},
          "dueDt": {"type": ["date", "null"]},
          "doneDt": {"type": "date"},
          "approvalNotes": {"type": "string"},
          "daysLeft": {"type": ["number", "null"]},
          "daysToComplete": {"type": ["number", "null"]},
          "daysOverdue": {"type": ["number", "null"]},
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


Gets the list of approvals recorded for the site

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
    "id": "/QuickStartCreationRequestBody",
    "type": "object",
    "properties": {
      "shortTitle": {"type": "string"},
      "sponsorInstitutionId": {"type": "string"},
      "sponsorUsers": {
        "type": "array",
        "minItems": 1,
        "uniqueItems": true,
        "items": {
          "type": "object",
          "properties": {
            "userId": {"type": "string"},
            "role": {"type": "string", "enum": ["full", "contract", "budget"]}
          },
          "required": ["userId", "role"]
        }
      },
      "croInstitutionId": {"type": ["string", "null"]},
      "croUsers": {
        "type": "array",
        "minItems": 0,
        "uniqueItems": true,
        "items": {
          "type": "object",
          "properties": {
            "userId": {"type": "string"},
            "role": {"type": "string", "enum": ["full", "contract", "budget"]}
          },
          "required": ["userId", "role"]
        }
      },
      "studyType": {"type": "string", "enum": ["phase1", "phase2", "phase3", "phase4", "other"]},
      "studyTypeOther": {"type": ["string", "null"]},
      "therapeuticArea": {"type": "string"},
      "isSingleSiteStudy": {"type": "boolean"},
      "reb": {
        "properties": {"name": {"type": "string"}, "committeeId": {"type": ["string", "null"]}},
        "required": ["name"]
      },
      "quickStartIdentifier": {"type": ["string", "null"]},
      "projectIdNumber": {"type": ["string", "null"]},
      "status": {"type": "string", "enum": ["pending", "screen", "active", "completed"]}
    },
    "required": [
      "shortTitle",
      "sponsorInstitutionId",
      "sponsorUsers",
      "croInstitutionId",
      "croUsers",
      "therapeuticArea",
      "isSingleSiteStudy",
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
    "id": "/QuickStartDocumentDeleteParams",
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartDocumentDownloadParams",
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
    "id": "/QuickStartDocumentUploadBody",
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
    "id": "/QuickStartDocumentUploadParams",
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartExtraDocumentDeleteParams",
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartExtraDocumentBody",
    "type": "object",
    "properties": {
      "documentId": {"type": "string"},
      "category": {
        "type": "string",
        "enum": ["paused", "pending", "screen", "review", "active", "completed"]
      },
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartExtraDocumentUploadBody",
    "properties": {
      "category": {
        "type": "string",
        "description": "The document type",
        "enum": ["paused", "pending", "screen", "review", "active", "completed"]
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
quickStart | cro | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTHistoryDelete - <em>QuickSTART Site Delete History</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/history/:type/:historyId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteHistoryDeleteParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "historyId": {"type": "string"},
      "type": {"type": "string", "enum": ["budget", "contract"]}
    },
    "required": ["quickStartId", "institutionId", "historyId"]
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


Deletes a history record for a quickSTART site. The site must not be completed

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/history/:type/:historyId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

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
    "id": "/QuickStartListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"}
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
          "therapeuticArea": {"type": "string"},
          "projectIdNumber": {"type": "number"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "quickStartIdentifier",
          "status",
          "shortTitle",
          "studyType",
          "therapeuticArea",
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
    "id": "/QuickStartParams",
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
        "isSingleSiteStudy": {"type": "boolean"},
        "status": {"type": "string", "enum": ["pending", "screen", "active", "completed"]},
        "protocol": {
          "id": "/QuickStartProtocol",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "documentName": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "documentName"]
        },
        "budget": {
          "id": "/QuickStartBudget",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "documentName": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "documentName"]
        },
        "contract": {
          "id": "/QuickStartContract",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "documentName": {"type": "string"},
            "strategy": {"type": "string"},
            "strategyOther": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "documentName", "strategy"]
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
        "creationProgress": {
          "type": "array",
          "items": {"type": "string", "enum": ["study", "studyDocuments", "contract", "budget"]}
        }
      },
      "required": [
        "id",
        "quickStartIdentifier",
        "shortTitle",
        "studyType",
        "therapeuticArea",
        "isSingleSiteStudy",
        "creationProgress"
      ]
    },
    "reb": {
      "type": "object",
      "id": "/QuickStartREB",
      "properties": {"committeeId": {"type": "object"}, "name": {"type": "string"}},
      "required": ["name"]
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
        "type": "object",
        "id": "/QuickStartSponsorUser",
        "properties": {
          "user": {
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
          "role": {"type": "string", "enum": ["full", "contract", "budget"]}
        },
        "required": ["user", "role"]
      },
      "minItems": 1
    },
    "cro": {
      "type": "object",
      "id": "/QuickStartCro",
      "properties": {
        "institutionId": {"type": "object"},
        "code": {"type": "string"},
        "name": {"type": "string"}
      },
      "required": ["institutionId", "code", "name"]
    },
    "croUsers": {
      "type": "array",
      "items": {
        "type": "object",
        "id": "/QuickStartSponsorUser",
        "properties": {
          "user": {
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
          "role": {"type": "string", "enum": ["full", "contract", "budget"]}
        },
        "required": ["user", "role"]
      }
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

## QuickSTARTRebEventDelete - <em>QuickSTART Site Delete REB Event</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/reb-event/:eventId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartRebEventDeleteParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "eventId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "eventId"]
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


Removes one quick start site REB event that was previously recorded in the system

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/reb-event/:eventId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A

## QuickSTARTRebEventSave - <em>QuickSTART Site REB Event Save</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/reb-event"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartRebEventBody",
    "type": "object",
    "properties": {
      "event": {
        "type": "string",
        "enum": [
          "submit",
          "review",
          "investigatorQuestions",
          "sponsorQuestions",
          "response",
          "approvalSent",
          "approvalReceived"
        ]
      },
      "isDone": {"type": "boolean"},
      "eventDt": {"type": "string", "format": "date-time"},
      "eventId": {"type": "string", "description": "If passed in, will update the event"},
      "comment": {"type": "string"}
    },
    "required": ["event"]
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


Adds or updates an REB event for the related quick start site.

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/reb-event`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A

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
    "id": "/QuickStartSiteParams",
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


Sends a QuickSTART pre-screened application to the Site.  The site status must be 'review'

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/send-to-site`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | cro | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartSiteAddUserBody",
    "type": "object",
    "properties": {
      "userId": {"type": "string"},
      "label": {
        "type": "string",
        "description": "The label text to display for the user, only applicable to read-only users"
      },
      "role": {"type": "string", "enum": ["contract", "budget", "investigator", "rc", "readonly"]}
    },
    "required": ["userId", "role"]
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


Adds a user to a QuickSTART site with the specified role. The site must not be completed

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/users`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A
quickStart | sponsor | quickStart|N/A
quickStart | cro | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
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


Marks a QuickSTART Site Pre-Screen as complete by CTO.  The site status must be 'screen'

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/pre-screen/complete`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

## QuickSTARTSiteConfigureNotifications - <em>QuickSTART Site Configure Notifications</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/configure-notifications"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "QuickStartSiteNotificationConfigurationBody",
    "type": "object",
    "properties": {
      "siteReviewerReminder": {"type": "boolean"},
      "siteSponsorReminder": {"type": "boolean"},
      "siteReviewerDue": {"type": "boolean"},
      "siteSponsorDue": {"type": "boolean"},
      "siteCustomApprovalReminder": {"type": "boolean"},
      "siteCustomApprovalDue": {"type": "boolean"},
      "statusUpdates": {"type": "array", "items": {"type": "number"}}
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


Updates an existing QuickSTART Site to disable notifications, set status updates, etc. If the site is completed, an error will be returned

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/configure-notifications`



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
    "id": "/QuickStartSiteCreationParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}},
    "required": ["quickStartId"]
  },
  "body": {
    "id": "/QuickStartSiteCreationRequestBody",
    "type": "object",
    "properties": {
      "institutionId": {"type": "string"},
      "researchCoordinatorId": {"type": "string"},
      "principalInvestigatorId": {"type": ["string", "null"]}
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
    "id": "/QuickStartDocumentDeleteParams",
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteDocumentDownloadParams",
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartSiteDocumentUploadBody",
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSitePauseEventDelete - <em>QuickSTART Site Delete Pause Event</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/pause-event/:pauseEventId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartPauseEventDeleteParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "pauseEventId": {"type": "string"}
    },
    "required": ["quickStartId", "institutionId", "pauseEventId"]
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


Deletes a pause event for an existing QuickSTART site.

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/pause-event/:pauseEventId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

## QuickSTARTSitePauseEventSave - <em>QuickSTART Site Save Pause Event</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/pause-event"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartPauseEventBody",
    "type": "object",
    "properties": {
      "pauseEventId": {"type": "string"},
      "startDt": {"type": "string", "format": "date-time"},
      "stopDt": {"type": "string", "format": "date-time"},
      "title": {"type": "string"},
      "description": {"type": "string"}
    },
    "required": ["title"]
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


Creates or updates a pause event for an existing QuickSTART site.

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/pause-event`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartPreScreenCommentBody",
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


Adds or updates a comment on a QuickSTART Site Pre-Screen.  The site status must be 'screen'

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
    "id": "/QuickStartPreScreenCommentDeleteParams",
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


Adds a comment to a QuickSTART Site to Pre-Screen.  The site status must be 'screen'

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
    "id": "/QuickStartSiteParams",
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
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
        "studyId": {
          "type": "object",
          "description": "If a stream project id number was set and there is a corresponding study in the system, the document id for the study."
        },
        "institutionId": {"type": "object"},
        "users": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "userId": {"type": "object"},
              "role": {
                "type": "string",
                "enum": ["contract", "budget", "investigator", "rc", "readonly"]
              },
              "label": {"type": "string"}
            },
            "required": ["userId", "role"]
          }
        },
        "status": {
          "type": "string",
          "enum": ["paused", "pending", "screen", "review", "active", "completed"]
        },
        "activeDt": {"type": "date"},
        "useProtocolDefaults": {"type": "boolean"},
        "useContractDefaults": {"type": "boolean"},
        "useBudgetDefaults": {"type": "boolean"},
        "pauseEvents": {
          "type": "array",
          "items": {
            "id": "QuickStartPauseEvent",
            "type": "object",
            "properties": {
              "id": {"type": "object"},
              "createDt": {"type": "date"},
              "updateDt": {"type": "date"},
              "startDt": {"type": "date"},
              "stopDt": {"type": "date"},
              "duration": {
                "type": "number",
                "description": "the number of days the event is active for from the start and stop dates"
              },
              "status": {"type": "string", "enum": ["pending", "active", "completed", "no-start"]},
              "title": {"type": "string"},
              "description": {"type": "string"}
            },
            "required": ["id", "createDt", "updateDt", "title", "status"]
          }
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
                "documentSentDt": {"type": "date"},
                "documentSentUserId": {"type": "object"},
                "assignedDt": {"type": "date"},
                "approvedDt": {"type": "date"},
                "status": {"type": "string", "enum": ["pending", "site", "sponsor", "approved"]},
                "history": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "id": "/QuickStartSiteApprovalHistory",
                    "properties": {
                      "id": {"type": "object"},
                      "userId": {"type": "object"},
                      "action": {
                        "type": "string",
                        "enum": [
                          "reviewer_comment",
                          "send_sponsor",
                          "assign",
                          "sponsor_comment",
                          "send_site",
                          "sponsor_approve"
                        ]
                      },
                      "comment": {"type": "string"},
                      "actionDt": {"type": "date"}
                    },
                    "required": ["id", "action", "actionDt"]
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
                          "dueDt": {"type": ["date", "null"]},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]},
                          "daysOverdue": {"type": ["number", "null"]}
                        },
                        "required": ["dueDt", "startDt"]
                      },
                      "sponsor": {
                        "properties": {
                          "action": {"type": ["string", "null"]},
                          "dueDt": {"type": ["date", "null"]},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]},
                          "daysOverdue": {"type": ["number", "null"]}
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
                "documentSentDt": {"type": "date"},
                "documentSentUserId": {"type": "object"},
                "assignedDt": {"type": "date"},
                "approvedDt": {"type": "date"},
                "status": {"type": "string", "enum": ["pending", "site", "sponsor", "approved"]},
                "history": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "id": "/QuickStartSiteApprovalHistory",
                    "properties": {
                      "id": {"type": "object"},
                      "userId": {"type": "object"},
                      "action": {
                        "type": "string",
                        "enum": [
                          "reviewer_comment",
                          "send_sponsor",
                          "assign",
                          "sponsor_comment",
                          "send_site",
                          "sponsor_approve"
                        ]
                      },
                      "comment": {"type": "string"},
                      "actionDt": {"type": "date"}
                    },
                    "required": ["id", "action", "actionDt"]
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
                          "dueDt": {"type": ["date", "null"]},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]},
                          "daysOverdue": {"type": ["number", "null"]}
                        },
                        "required": ["dueDt", "startDt"]
                      },
                      "sponsor": {
                        "properties": {
                          "action": {"type": ["string", "null"]},
                          "dueDt": {"type": ["date", "null"]},
                          "startDt": {"type": "date"},
                          "completeDt": {"type": ["date", "null"]},
                          "daysToComplete": {"type": ["number", "null"]},
                          "daysLeft": {"type": ["number", "null"]},
                          "daysOverdue": {"type": ["number", "null"]}
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
        "notificationConfiguration": {
          "id": "QuickStartSiteNotificationConfigurationBody",
          "type": "object",
          "properties": {
            "siteReviewerReminder": {"type": "boolean"},
            "siteSponsorReminder": {"type": "boolean"},
            "siteReviewerDue": {"type": "boolean"},
            "siteSponsorDue": {"type": "boolean"},
            "siteCustomApprovalReminder": {"type": "boolean"},
            "siteCustomApprovalDue": {"type": "boolean"},
            "statusUpdates": {"type": "array", "items": {"type": "number"}}
          }
        },
        "timers": {
          "id": "QuickStartSiteTimers",
          "type": "object",
          "properties": {
            "active": {"type": "number"},
            "daysToApprove": {"type": "number"},
            "contract": {
              "type": "object",
              "properties": {
                "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
                "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
              },
              "required": ["siteDaysToAction", "sponsorDaysToRespond"]
            },
            "budget": {
              "type": "object",
              "properties": {
                "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
                "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
              },
              "required": ["siteDaysToAction", "sponsorDaysToRespond"]
            }
          },
          "required": ["active", "daysToApprove", "contract", "budget"]
        },
        "protocolDocumentSentDt": {"type": "date"},
        "protocolDocumentSentUserId": {"type": "object"},
        "protocol": {
          "id": "/QuickStartProtocol",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "documentName": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "documentName"]
        },
        "budget": {
          "id": "/QuickStartBudget",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "documentName": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "documentName"]
        },
        "contract": {
          "id": "/QuickStartContract",
          "type": "object",
          "properties": {
            "documentLocation": {"type": "string", "enum": ["upload", "manual"]},
            "documentName": {"type": "string"},
            "strategy": {"type": "string"},
            "strategyOther": {"type": "string"},
            "notes": {"type": "string"}
          },
          "required": ["documentLocation", "documentName", "strategy"]
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
              "category": {
                "type": "string",
                "enum": ["paused", "pending", "screen", "review", "active", "completed"]
              },
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
        },
        "rebEvents": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "id": {"type": "object"},
              "event": {
                "type": "string",
                "enum": [
                  "submit",
                  "review",
                  "investigatorQuestions",
                  "sponsorQuestions",
                  "response",
                  "approvalSent",
                  "approvalReceived"
                ]
              },
              "eventDt": {"type": "date"},
              "isDone": {"type": "boolean"},
              "isDeletable": {"type": "boolean"},
              "comment": {"type": "string"}
            },
            "required": ["id", "event", "isDone"]
          }
        },
        "customData": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {"label": {"type": "string"}, "value": {"type": "string"}},
            "required": ["label", "value"]
          }
        },
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"}
      },
      "required": [
        "id",
        "institutionId",
        "users",
        "status",
        "useProtocolDefaults",
        "useContractDefaults",
        "useBudgetDefaults",
        "timers",
        "protocol",
        "budget",
        "contract",
        "createDt",
        "updateDt"
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
          "required": []
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
        "reb": {
          "type": "object",
          "id": "/QuickStartREB",
          "properties": {"committeeId": {"type": "object"}, "name": {"type": "string"}},
          "required": ["name"]
        },
        "initialApprovalDt": {"type": "date"},
        "initialReviewType": {
          "type": "string",
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
      "required": ["status", "reb", "createDt"]
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartSiteRecordSentDtBody",
    "type": "object",
    "properties": {
      "type": {"type": "string", "enum": ["budget", "contract", "protocol"]},
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


Updates an existing QuickSTART Site with the send date of a document, specified by type.  The application must be active, or an error is returned.

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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

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
    "id": "/QuickStartSiteRemoveUserParams",
    "type": "object",
    "properties": {
      "quickStartId": {"type": "string"},
      "institutionId": {"type": "string"},
      "userId": {"type": "string"},
      "role": {"type": "string", "enum": ["contract", "budget", "investigator", "rc", "readonly"]}
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


Removes a user from a QuickSTART site. Restrictions are listed per role.  An error is returned if the final RC is attempted to be removed. The site must not be completed

### HTTP Request

`DELETE /quick-start/:quickStartId/sites/:institutionId/users/:userId/role/:role`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|The user can only specify a role that they currently have.
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | contract | quickStartSite|The user can only specify a role that they currently have.
quickStartSite | budget | quickStartSite|The user can only specify a role that they currently have.
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartSiteResponseBody",
    "type": "object",
    "properties": {
      "historyId": {"type": "string"},
      "type": {"type": "string", "enum": ["budget", "contract"]},
      "action": {"type": "string", "enum": ["sponsor_comment", "send_site", "sponsor_approve"]},
      "actionDt": {"type": "string", "format": "date-time"},
      "comment": {"type": "string"}
    },
    "required": ["type", "action", "actionDt"]
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteRestoreParams",
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartTSiteReviewBody",
    "type": "object",
    "properties": {
      "historyId": {"type": "string"},
      "type": {"type": "string", "enum": ["budget", "contract"]},
      "action": {"type": "string", "enum": ["reviewer_comment", "send_sponsor"]},
      "actionDt": {"type": "string", "format": "date-time"},
      "comment": {"type": "string"}
    },
    "required": ["type", "action", "actionDt"]
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


Submit a review for one section of data for a QuickSTART site.  The site status must be active

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

## QuickSTARTSiteSaveCustomData - <em>QuickSTART Site Save Custom Data</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/custom-data"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "/QuickStartSiteCustomDataBody",
    "type": "object",
    "properties": {"label": {"type": "string"}, "value": {"type": ["string", "null"]}},
    "required": ["label"]
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



        Saves a custom data point to a QuickSTART site application.  Will also delete existing custom data fields if the value is passed in is empty/null.
        The site status must be not be completed.
        

### HTTP Request

`POST /quick-start/:quickStartId/sites/:institutionId/custom-data`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
quickStartSite | rc | quickStartSite|N/A
quickStartSite | investigator | quickStartSite|N/A
quickStartSite | approver | quickStartSite|N/A
quickStartSite | contract | quickStartSite|N/A
quickStartSite | budget | quickStartSite|N/A
institution | quickStartSponsor | quickStart|N/A

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
    "id": "/QuickStartSiteParams",
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


Sends a QuickSTART Site to Pre-Screen with CTO.  The site status must be 'pending'

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/pre-screen`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A
quickStart | sponsor | quickStart|N/A
quickStart | cro | quickStart|N/A
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
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {"id": "/QuickStartSiteUpdateBody", "type": "object", "required": []}
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


Updates an existing QuickSTART Site portion of an application in the system. If the site is completed, an error will be returned

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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
institution | quickStartSponsor | quickStart|N/A

## QuickSTARTSiteUpdateTimers - <em>QuickSTART Site Update Timers</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start/:quickStartId/sites/:institutionId/timers"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  },
  "body": {
    "id": "QuickStartSiteTimersBody",
    "type": "object",
    "properties": {
      "startDt": {"type": "string", "format": "date-time"},
      "daysToApprove": {"type": "number"},
      "contract": {
        "type": "object",
        "properties": {
          "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
          "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
        },
        "required": ["siteDaysToAction", "sponsorDaysToRespond"]
      },
      "budget": {
        "type": "object",
        "properties": {
          "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
          "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
        },
        "required": ["siteDaysToAction", "sponsorDaysToRespond"]
      }
    },
    "required": ["startDt", "daysToApprove", "contract", "budget"]
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


Updates an existing QuickSTART Site Timers in the system. If the site is completed, an error will be returned

### HTTP Request

`PUT /quick-start/:quickStartId/sites/:institutionId/timers`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

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
    "id": "/QuickStartParams",
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
          "users": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "userId": {"type": "object"},
                "role": {
                  "type": "string",
                  "enum": ["contract", "budget", "investigator", "rc", "readonly"]
                },
                "label": {"type": "string"}
              },
              "required": ["userId", "role"]
            }
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
                "required": []
              }
            },
            "required": ["id", "code", "name", "type", "status", "address"]
          },
          "status": {
            "type": "string",
            "enum": ["paused", "pending", "screen", "review", "active", "completed"]
          },
          "activeDt": {"type": "date"},
          "timers": {
            "id": "QuickStartSiteTimers",
            "type": "object",
            "properties": {
              "active": {"type": "number"},
              "daysToApprove": {"type": "number"},
              "contract": {
                "type": "object",
                "properties": {
                  "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
                  "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
                },
                "required": ["siteDaysToAction", "sponsorDaysToRespond"]
              },
              "budget": {
                "type": "object",
                "properties": {
                  "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
                  "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
                },
                "required": ["siteDaysToAction", "sponsorDaysToRespond"]
              }
            },
            "required": ["active", "daysToApprove", "contract", "budget"]
          },
          "approvals": {
            "type": "object",
            "properties": {
              "timerStartDt": {"type": "date"},
              "timerCompleteDt": {"type": "date"},
              "actualCompleteDt": {"type": "date"}
            }
          },
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "institutionId",
          "institution",
          "timers",
          "users",
          "status",
          "createDt",
          "updateDt"
        ]
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
    "id": "/QuickStartUpdateParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}},
    "required": ["quickStartId"]
  },
  "body": {
    "id": "/QuickStartUpdateBody",
    "type": "object",
    "properties": {
      "quickStartSiteId": {
        "type": "string",
        "description": "If passed along with content, the site will be updated instead of the overall QuickSTART application"
      },
      "creationProgress": {
        "type": "array",
        "items": {"type": "string", "enum": ["study", "studyDocuments", "contract", "budget"]},
        "description": "any strings passed in will update the quick start creation progress status to true for that key.  Has no effect if quick start site id is passed"
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
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartUniqueProjectIdNumberParams",
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
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartUniqueQuickStartIdentifierParams",
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
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
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
    "id": "/QuickStartUniqueShortTitleParams",
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
quickStart | sponsor | quickStart|N/A
quickStart | sponsor-contract | quickStart|N/A
quickStart | sponsor-budget | quickStart|N/A
quickStart | cro | quickStart|N/A
quickStart | cro-contract | quickStart|N/A
quickStart | cro-budget | quickStart|N/A
institution | quickStartSponsor | N/A|N/A