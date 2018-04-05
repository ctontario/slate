
# Admin


## AdminModerationList - <em>Admin User Moderation List</em>


```shell
curl "https://www.ctoregistry.com/api/v1/admin/moderation/user"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/ListQuery",
    "type": "object",
    "properties": {
      "count": {"type": "string"},
      "offset": {"type": "string"},
      "limit": {"type": "string"},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "institutions": {"type": ["string", "array"], "description": "an array of institution IDs"}
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
                  "required": ["streetAddress", "locality", "region", "postalCode"]
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
institution | admin | N/A|User is a member at, or their request involves the target institution of the privilege.

## AdminUserModeration - <em>Admin User Institution Moderation</em>


```shell
curl -X POST "https://www.ctoregistry.com/api/v1/admin/moderation/user/institution"  
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
    "id": {"type": "object|null"},
    "result": {"type": "object|array|string"}
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
institution | admin | user|N/A

## AdminUserRoleModeration - <em>Admin User Institution Role Moderation</em>


```shell
curl -X PUT "https://www.ctoregistry.com/api/v1/admin/moderation/user/:userId/institution/:userInstitutionId/role/:roleId/status/:status"  
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
    "id": {"type": "object|null"},
    "result": {"type": "object|array|string"}
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
institution | admin | user|N/A