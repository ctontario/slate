
# Admin


## AdminModerationList - <em>Admin User Moderation List</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/moderation/user"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/ModerationListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "institutionIds": {
        "type": ["string", "array"],
        "description": "an array of institution IDs to find users to moderate at"
      }
    }
  }
}
```


> Response Schema

```json
{
  "id": "/AdminUserModerationListResponse",
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
        "id": "/AdminUserModeration",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "account": {
            "type": "object",
            "properties": {"status": {"type": "string"}, "isNewAccount": {"type": "boolean"}},
            "required": ["status", "isNewAccount"]
          },
          "username": {"type": "string"},
          "title": {"type": "string"},
          "firstName": {"type": "string"},
          "middleName": {"type": "string"},
          "lastName": {"type": "string"},
          "moderation": {"type": "array", "items": {"type": "object"}},
          "institutions": {
            "type": "array",
            "items": {
              "type": "object",
              "id": "AdminUserModerationInstitution",
              "properties": {
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
                "id": {"type": "object"},
                "institutionId": {"type": "object"},
                "suggestedId": {"type": "object"},
                "status": {"type": "string"},
                "requiresModeration": {"type": "boolean"},
                "isInvestigator": {"type": "boolean"},
                "email": {"type": "email"},
                "emailValidationToken": {"type": "string"},
                "isNewInstitution": {"type": "boolean"},
                "nextAction": {"type": "string"},
                "institutionNameSuggested": {"type": "string"},
                "code": {"type": "string"},
                "name": {"type": "string"},
                "roles": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "id": "AdminUserModerationRole",
                    "properties": {
                      "id": {"type": "object"},
                      "code": {"type": "string"},
                      "status": {"type": "string"},
                      "requiresModeration": {"type": "boolean"},
                      "label": {"type": "string"}
                    },
                    "required": ["id", "code", "status", "requiresModeration", "label"]
                  }
                }
              },
              "required": [
                "address",
                "id",
                "status",
                "requiresModeration",
                "email",
                "isNewInstitution"
              ]
            }
          },
          "nextAction": {"type": "string"}
        },
        "required": ["id", "account", "username", "title", "firstName", "lastName", "nextAction"]
      }
    }
  }
}
```


Gets the list of users that the authenticated user can moderate.  This will include new accounts, institutions added to accounts, and roles added to users at institutions.

### HTTP Request

`GET /admin/moderation/user`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | N/A|User is a member at, or their request involves the target institution of the privilege.

## AdminUserModeration - <em>Admin User Institution Moderation</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/admin/moderation/user/institution"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/UserInstitutionModeration",
    "type": "object",
    "properties": {
      "userId": {"type": "string", "description": "User ID"},
      "userInstitutionId": {
        "type": "string",
        "description": "The ID of the user institution to moderate"
      },
      "assignRoles": {"type": "array", "items": {"type": "string"}},
      "removeRoles": {"type": "array", "items": {"type": "string"}},
      "status": {"type": "string", "description": "set the status of the user institution"}
    },
    "required": ["userId", "userInstitutionId"]
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


Lets an admin moderate a users institution request.  
        As all new registrations must come with an institution,
        new registrations are considered "institution requests" in the system and our moderated using the same feature
        as moderating a new institution request for an existing user.

### HTTP Request

`POST /admin/moderation/user/institution`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | user|N/A

## AdminUserRoleModeration - <em>Admin User Institution Role Moderation</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/admin/moderation/user/:userId/institution/:userInstitutionId/role/:roleId/status/:status"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/AdminUserRoleModeration",
    "type": "object",
    "properties": {
      "userId": {"type": "string"},
      "userInstitutionId": {"type": "string"},
      "roleId": {"type": "string"},
      "status": {"type": "string"}
    },
    "required": ["userId", "userInstitutionId", "roleId", "status"]
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


Lets an admin moderate a users role request at a specified institution

### HTTP Request

`PUT /admin/moderation/user/:userId/institution/:userInstitutionId/role/:roleId/status/:status`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A
institution | admin | user|N/A

## CacheDocumentDownload - <em>Download Cache Document</em>


```shell
curl "https://ctoregistry.com/api/v1/download/cache/:dir/:fileName"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CacheDocumentDownloadRequestParams",
    "type": "object",
    "properties": {
      "dir": {"type": "string", "enum": ["system", "stream", "streamBackup", "streamExtractor"]},
      "fileName": {"type": "string"}
    },
    "required": ["dir", "fileName"]
  },
  "query": {
    "id": "/CacheDocumentDownloadRequestQuery",
    "type": "object",
    "properties": {"csv": {"type": "boolean"}}
  }
}
```


> Response Schema

```json
undefined
```


Downloads one document from the specified cache directory.

### HTTP Request

`GET /download/cache/:dir/:fileName`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## GetCacheFileList - <em>Cache File List</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/cache/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/CacheFileListResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "cache": {"type": "string"},
          "files": {"type": "array", "items": {"type": "string"}}
        },
        "required": ["cache", "files"]
      }
    }
  },
  "required": ["data"]
}
```


Gets the details about the cache files stored in the system


### HTTP Request

`GET /admin/cache/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## GetEmailLog - <em>Email Log</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/email/:emailLogId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/EmailLogParams",
    "type": "object",
    "properties": {"emailLogId": {"type": "string"}},
    "required": ["emailLogId"]
  }
}
```


> Response Schema

```json
{
  "id": "/EmailLogResponse",
  "type": "object",
  "properties": {
    "emailLog": {
      "id": "EmailLog",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "email": {"type": "string"},
        "template": {"type": "string"},
        "categories": {"type": "array", "items": {"type": "string"}},
        "lastEvent": {
          "type": "string",
          "enum": [
            "processed",
            "dropped",
            "delivered",
            "deferred",
            "bounce",
            "open",
            "click",
            "spamreport",
            "unsubscribe",
            "group_unsubscribe",
            "group_resubscribe"
          ]
        },
        "eventCount": {"type": "number"},
        "isDelivered": {"type": "boolean"},
        "isOpened": {"type": "boolean"},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"}
      },
      "required": [
        "id",
        "email",
        "template",
        "categories",
        "lastEvent",
        "eventCount",
        "isDelivered",
        "isOpened",
        "createDt",
        "updateDt"
      ]
    },
    "events": {
      "type": "array",
      "items": {
        "id": "EmailLogEvent",
        "properties": {
          "id": {"type": "object"},
          "event": {
            "type": "string",
            "enum": [
              "processed",
              "dropped",
              "delivered",
              "deferred",
              "bounce",
              "open",
              "click",
              "spamreport",
              "unsubscribe",
              "group_unsubscribe",
              "group_resubscribe"
            ]
          },
          "useragent": {"type": "string"},
          "IP": {"type": "string"},
          "attempt": {"type": "string"},
          "reason": {"type": "string"},
          "status": {"type": "string"},
          "response": {"type": "string"},
          "url": {"type": "string"},
          "bounceType": {"type": "string"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": ["id", "event", "createDt", "updateDt"]
      }
    },
    "required": ["emailLog", "events"]
  }
}
```


Gets the details about one email log entry from the system



### HTTP Request

`GET /admin/email/:emailLogId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A

## GetEmailLogs - <em>Email Logs</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/email"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/EmailLogsQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "categories": {"type": ["string", "array"], "items": {"type": "string"}},
      "templates": {"type": ["string", "array"], "items": {"type": "string"}}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/EmailLogsResponse",
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
        "id": "EmailLog",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "email": {"type": "string"},
          "template": {"type": "string"},
          "categories": {"type": "array", "items": {"type": "string"}},
          "lastEvent": {
            "type": "string",
            "enum": [
              "processed",
              "dropped",
              "delivered",
              "deferred",
              "bounce",
              "open",
              "click",
              "spamreport",
              "unsubscribe",
              "group_unsubscribe",
              "group_resubscribe"
            ]
          },
          "eventCount": {"type": "number"},
          "isDelivered": {"type": "boolean"},
          "isOpened": {"type": "boolean"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "email",
          "template",
          "categories",
          "lastEvent",
          "eventCount",
          "isDelivered",
          "isOpened",
          "createDt",
          "updateDt"
        ]
      }
    }
  }
}
```


Gets the list of emails that have been sent in the system

### HTTP Request

`GET /admin/email`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A

## GetTaskLogIssues - <em>Task Log Issues</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/sync/taskLogs/:taskLogId/issues"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/TaskLogIssuesRequest",
    "type": "object",
    "properties": {"taskLogId": {"type": "string"}},
    "required": ["taskLogId"]
  },
  "query": {
    "id": "/TaskLogIssuesQuery",
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
  "id": "/TaskLogIssuesResponse",
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
        "id": "/TaskLogIssue",
        "properties": {
          "id": {"type": "object"},
          "taskLogId": {"type": "object"},
          "rownum": {"type": "string"},
          "issueType": {"type": "string"},
          "issue": {"type": ["string"]},
          "isResolved": {"type": "boolean"},
          "rawData": {"type": ["object", "string"]},
          "data": {
            "properties": {
              "id": {"type": "string"},
              "email": {"type": "string"},
              "firstName": {"type": "string"},
              "lastName": {"type": "string"},
              "institution": {"type": "string"}
            }
          }
        },
        "required": ["id", "data", "taskLogId", "issueType", "isResolved"]
      }
    }
  },
  "required": ["meta", "data"]
}
```


Gets the issues related to the last run of the specified taskName

### HTTP Request

`GET /admin/sync/taskLogs/:taskLogId/issues`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A

## GetTaskLogs - <em>Task Logs</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/sync/taskLogs"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/TaskLogsResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/TaskLog",
        "properties": {
          "id": {"type": "object"},
          "taskName": {"type": "string"},
          "runDt": {"type": "date"},
          "issues": {
            "type": "object",
            "properties": {"total": {"type": "integer"}, "resolved": {"type": "integer"}},
            "required": ["total", "resolved"]
          },
          "results": {
            "type": "object",
            "properties": {"total": {"type": "integer"}, "errors": {"type": "integer"}},
            "required": ["total", "errors"]
          },
          "error": {"type": ["object", "any"]}
        },
        "required": ["id", "taskName", "runDt", "issues", "results"]
      }
    }
  }
}
```


Lets an admin review the logs from the last round of synchronization
If taskName is passed then only that task log is returned, or an error if not found.  If no task
name is passed in then all tasks from the previous run will be included        


### HTTP Request

`GET /admin/sync/taskLogs`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A

## TaskLogIssueMarkResolved - <em>Update Task Log Issue</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/admin/sync/taskLogs/:taskLogId/issues/:issueId/:resolved"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/TaskLogIssueUpdateRequest",
    "type": "object",
    "properties": {
      "taskLogId": {"type": "string"},
      "issueId": {"type": "string"},
      "resolved": {"type": "boolean"}
    },
    "required": ["taskLogId", "issueId", "resolved"]
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


Updates the issues with the new isResolved value

### HTTP Request

`PUT /admin/sync/taskLogs/:taskLogId/issues/:issueId/:resolved`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A

## TaskLogList - <em>Task Logs List</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/sync/taskLogs/list"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/TaskLogListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "taskName": {"type": ["string", "array"]}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/TaskLogListResponse",
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
        "id": "/TaskLog",
        "properties": {
          "id": {"type": "object"},
          "taskName": {"type": "string"},
          "runDt": {"type": "date"},
          "issues": {
            "type": "object",
            "properties": {"total": {"type": "integer"}, "resolved": {"type": "integer"}},
            "required": ["total", "resolved"]
          },
          "results": {
            "type": "object",
            "properties": {"total": {"type": "integer"}, "errors": {"type": "integer"}},
            "required": ["total", "errors"]
          },
          "error": {"type": ["object", "any"]}
        },
        "required": ["id", "taskName", "runDt", "issues", "results"]
      }
    }
  },
  "required": ["meta", "data"]
}
```


access the full paginated list of task logs in the system


### HTTP Request

`GET /admin/sync/taskLogs/list`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A

## TaskLogProfile - <em>Task Log Profile</em>


```shell
curl "https://ctoregistry.com/api/v1/admin/sync/taskLogs/:taskLogId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/TaskLogProfileRequest",
    "type": "object",
    "properties": {"taskLogId": {"type": "string"}},
    "required": ["taskLogId"]
  }
}
```


> Response Schema

```json
{
  "id": "/TaskLogProfileResponse",
  "type": "object",
  "properties": {
    "taskLog": {
      "id": "/TaskLog",
      "properties": {
        "id": {"type": "object"},
        "taskName": {"type": "string"},
        "runDt": {"type": "date"},
        "issues": {
          "type": "object",
          "properties": {"total": {"type": "integer"}, "resolved": {"type": "integer"}},
          "required": ["total", "resolved"]
        },
        "results": {
          "type": "object",
          "properties": {"total": {"type": "integer"}, "errors": {"type": "integer"}},
          "required": ["total", "errors"]
        },
        "error": {"type": ["object", "any"]}
      },
      "required": ["id", "taskName", "runDt", "issues", "results"]
    }
  },
  "required": ["taskLog"]
}
```


Gets the information for one task log

### HTTP Request

`GET /admin/sync/taskLogs/:taskLogId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A