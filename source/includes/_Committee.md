
# Committee


## CommitteeAddMember - <em>Committee Add Member</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/committee/:committeeId/members/add"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/CommitteeMember",
  "type": "object",
  "properties": {
    "userId": {
      "type": "string",
      "description": "The userId of the user's account to add as a committee member"
    },
    "role": {
      "type": "string",
      "description": "The role of the member",
      "enum": ["chair", "member", "staff", "director", "contact"]
    },
    "status": {
      "type": "string",
      "description": "The status of the member",
      "enum": ["pending", "active", "suspended", "ended"]
    },
    "joinDt": {"type": "string", "description": "The date the member joined the committee"}
  },
  "required": ["userId", "role", "status"]
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


Adds a user for one existing committee

### HTTP Request

`POST /committee/:committeeId/members/add`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeCheckUniqueCode - <em>Check Committee Unique Code</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-code/:code/:committeeId?"  
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


Checks to see if an committee code is already in use or not.

### HTTP Request

`GET /committee/unique-code/:code/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeCheckUniqueName - <em>Check Committee Unique Name</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-name/:name/:committeeId?"  
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


Checks to see if an committee name is already in use or not.

### HTTP Request

`GET /committee/unique-name/:name/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeCheckUniqueShortName - <em>Check Committee Unique Short Name</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-short-name/:shortName/:committeeId?"  
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


Checks to see if an committee short name is already in use or not.

### HTTP Request

`GET /committee/unique-short-name/:shortName/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeCheckUniqueStreamName - <em>Check Committee Unique Stream Name</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-stream-name/:streamName/:committeeId?"  
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


Checks to see if an committee Stream Name is already in use or not.

### HTTP Request

`GET /committee/unique-stream-name/:streamName/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeCreation - <em>Create Committee</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/committee/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/CommitteeCreation",
  "type": "object",
  "properties": {
    "code": {"type": "string", "description": "The committee's code"},
    "name": {"type": "string", "description": "The name of the committee"},
    "shortName": {"type": "string", "description": "The short name of the committee"},
    "streamName": {"type": "string", "description": "The name of the committee in CTO Stream"},
    "type": {"type": "string", "description": "The type of committee", "enum": ["reb", "steering"]},
    "status": {
      "type": "string",
      "description": "The status of the committee",
      "enum": ["pending", "active", "deleted", "suspended"]
    },
    "statusEffectiveChangeDt": {
      "type": "string",
      "description": "The effective date of a change of status"
    },
    "parentInstitutionId": {"type": "string", "description": "The ID of the parent institution"}
  },
  "required": ["name", "code", "type", "status", "parentInstitutionId"]
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


Creates a new committee

### HTTP Request

`POST /committee/`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeDictionary - <em>Committee Dictionary</em>


```shell
curl "https://cto.local:9000/api/v1/dictionary/committee"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/CommitteeDictionaryResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object", "description": ""},
          "name": {"type": "string", "description": ""},
          "streamName": {"type": "string", "description": ""},
          "code": {"type": "string", "description": ""}
        },
        "required": ["id", "name", "streamName", "code"]
      }
    }
  }
}
```


Gets the list of committees that are present in the system

### HTTP Request

`GET /dictionary/committee`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeEditMember - <em>Committee Edit Member</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/committee/:committeeId/members/edit"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/CommitteeMemberEdit",
  "type": "object",
  "properties": {
    "userId": {
      "type": "string",
      "description": "The userId of the user's account to add as a committee member"
    },
    "role": {
      "type": "string",
      "description": "The role of the member",
      "enum": ["chair", "member", "staff", "director", "contact"]
    },
    "status": {
      "type": "string",
      "description": "The status of the member",
      "enum": ["pending", "active", "suspended", "ended"]
    },
    "joinDt": {"type": "string", "description": "The date the member joined the committee"},
    "memberId": {
      "type": "string",
      "description": "The userId of the user's account to add as a committee member"
    }
  },
  "required": ["userId", "role", "status", "memberId"]
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


updates user information for one existing committee

### HTTP Request

`POST /committee/:committeeId/members/edit`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeList - <em>Get Committee List</em>


```shell
curl "https://cto.local:9000/api/v1/committee/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/CommitteeListResponse",
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
          "institution": {
            "type": "object",
            "properties": {
              "id": {"type": "object", "description": ""},
              "code": {"type": "string", "description": ""},
              "name": {"type": "string", "description": ""}
            },
            "required": ["id", "code", "name"]
          },
          "createDt": {"type": "date", "description": ""},
          "updateDt": {"type": "date", "description": ""}
        },
        "required": ["id", "code", "name", "type", "status", "institution", "createDt", "updateDt"]
      }
    }
  }
}
```


Gets the list of all committees.

### HTTP Request

`GET /committee/`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## CommitteeListForUser - <em>Committees for User</em>


```shell
curl "https://cto.local:9000/api/v1/committee/user/:userId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/UserCommitteesResponse",
  "type": "object",
  "properties": {
    "user": {
      "id": "/UserShortProfile",
      "properties": {
        "id": {"type": "object", "description": ""},
        "username": {"type": "string", "description": ""},
        "contact": {
          "type": "object",
          "properties": {
            "firstName": {"type": "string", "description": ""},
            "middleName": {"type": "string", "description": ""},
            "lastName": {"type": "string", "description": ""},
            "title": {
              "type": "string",
              "description": "",
              "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
            }
          },
          "required": ["firstName", "lastName", "title"]
        },
        "institutionIds": {"type": "array", "items": {"type": "object", "description": ""}}
      },
      "required": ["id", "username", "contact", "institutionIds"]
    },
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "committee": {
            "type": "object",
            "properties": {
              "id": {"type": "object", "description": ""},
              "name": {"type": "string", "description": ""}
            },
            "required": ["id", "name"]
          },
          "id": {"type": "object", "description": ""},
          "role": {"type": "string", "description": ""},
          "status": {"type": "string", "description": ""},
          "joinDt": {"type": "date", "description": ""},
          "endDt": {"type": "date", "description": ""}
        },
        "required": ["committee", "id", "role", "status", "joinDt"]
      }
    }
  }
}
```


Get the committees that a user belongs too

### HTTP Request

`GET /committee/user/:userId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## CommitteeMembers - <em>Committee Members</em>


```shell
curl "https://cto.local:9000/api/v1/committee/:committeeId/members"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/CommitteeMembersResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object", "description": ""},
          "role": {"type": "string", "description": ""},
          "status": {"type": "string", "description": ""},
          "createDt": {"type": "date", "description": ""},
          "endDt": {"type": "date", "description": ""},
          "user": {
            "id": "/UserShortProfile",
            "properties": {
              "id": {"type": "object", "description": ""},
              "username": {"type": "string", "description": ""},
              "contact": {
                "type": "object",
                "properties": {
                  "firstName": {"type": "string", "description": ""},
                  "middleName": {"type": "string", "description": ""},
                  "lastName": {"type": "string", "description": ""},
                  "title": {
                    "type": "string",
                    "description": "",
                    "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                  }
                },
                "required": ["firstName", "lastName", "title"]
              },
              "institutionIds": {"type": "array", "items": {"type": "object", "description": ""}}
            },
            "required": ["id", "username", "contact", "institutionIds"]
          }
        },
        "required": ["id", "role", "status", "createDt", "user"]
      }
    }
  }
}
```


gets all the members of a committee

### HTTP Request

`GET /committee/:committeeId/members`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
committee | member | committee

## CommitteeProfile - <em>Get Committee</em>


```shell
curl "https://cto.local:9000/api/v1/committee/:committeeId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/CommitteeProfileResponse",
  "type": "object",
  "properties": {
    "committee": {
      "type": "object",
      "properties": {
        "id": {"type": "object", "description": ""},
        "code": {"type": "string", "description": ""},
        "name": {"type": "string", "description": ""},
        "type": {"type": "string", "description": ""},
        "status": {"type": "string", "description": ""},
        "shortName": {"type": "string", "description": ""},
        "streamName": {"type": "string", "description": ""},
        "institution": {
          "type": "object",
          "properties": {
            "id": {"type": "object", "description": ""},
            "code": {"type": "string", "description": ""},
            "name": {"type": "string", "description": ""}
          },
          "required": ["id", "code", "name"]
        },
        "createDt": {"type": "date", "description": ""},
        "updateDt": {"type": "date", "description": ""}
      },
      "required": [
        "id",
        "code",
        "name",
        "type",
        "status",
        "shortName",
        "streamName",
        "institution",
        "createDt",
        "updateDt"
      ]
    }
  }
}
```


Gets the data associated to one committee.

### HTTP Request

`GET /committee/:committeeId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
committee | member | committee

## CommitteeUpdate - <em>Update Committee</em>


```shell
curl -X PUT "https://cto.local:9000/api/v1/committee/:committeeId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/CommitteeUpdate",
  "type": "object",
  "properties": {
    "code": {"type": "string", "description": "The committee's code"},
    "name": {"type": "string", "description": "The name of the committee"},
    "shortName": {"type": "string", "description": "The short name of the committee"},
    "streamName": {"type": "string", "description": "The name of the committee in CTO Stream"},
    "type": {"type": "string", "description": "The type of committee", "enum": ["reb", "steering"]},
    "status": {
      "type": "string",
      "description": "The status of the committee",
      "enum": ["pending", "active", "deleted", "suspended"]
    },
    "statusEffectiveChangeDt": {
      "type": "string",
      "description": "The effective date of a change of status"
    },
    "parentInstitutionId": {"type": "string", "description": "The ID of the parent institution"}
  },
  "required": ["name", "type"]
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


Updates an existing committee

### HTTP Request

`PUT /committee/:committeeId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A