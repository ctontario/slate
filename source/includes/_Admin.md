
# Admin


## ModerateUser - <em>Admin User Institution Moderation</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/admin/moderation/user/institution"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/UserInstitutionModeration",
  "type": "object",
  "properties": {
    "userId": {"type": "string", "description": "User ID"},
    "userInstitutionId": {
      "type": "string",
      "description": "The ID of the user institution to moderate",
      "default": false
    },
    "assignRoles": {"type": "array", "items": {"type": "string"}},
    "removeRoles": {"type": "array", "items": {"type": "string"}},
    "status": {"type": "string", "description": "set the status of the user institution"}
  },
  "required": ["userId", "userInstitutionId"]
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



        Lets an admin moderate a users institution request.  As all new registrations must come with an institution,
        new registrations are considered "institution requests" in the system and our moderated using the same feature
        as moderating a new institution request for an existing user.
        
        - if the user has the <strong>system:admin</strong> role, then they can process moderations for all users
        
        - if the user has the <strong>institution:admin</strong> role, they can only process moderations for users at their
        institution(s)
        
        

### HTTP Request

`POST /admin/moderation/user/institution`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | user

## ModerateUserRole - <em>Admin User Institution Role Moderation</em>


```shell
curl -X PUT "https://cto.local:9000/api/v1/admin/moderation/user/:userId/institution/:userInstitutionId/role/:roleId/status/:status"  
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



        
        Lets an admin moderate a users role request at a specified institution
        
        - if the user has the <strong>system:admin</strong> role, then they can process role moderations for all users
        
        - if the user has the <strong>institution:admin</strong> role, they can only process role moderations for users at their
        institution(s)
        
        

### HTTP Request

`PUT /admin/moderation/user/:userId/institution/:userInstitutionId/role/:roleId/status/:status`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | user

## ModerationList - <em>Admin User Moderation List</em>


```shell
curl "https://cto.local:9000/api/v1/admin/moderation/user"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/AdminModerationRequestListResponse",
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
          "account": {
            "type": "object",
            "properties": {
              "status": {"type": "string", "description": ""},
              "isNewAccount": {"type": "boolean", "description": ""}
            },
            "required": ["status", "isNewAccount"]
          },
          "username": {"type": "string", "description": ""},
          "title": {"type": "string", "description": ""},
          "firstName": {"type": "string", "description": ""},
          "middleName": {"type": "string", "description": ""},
          "lastName": {"type": "string", "description": ""},
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
                    "streetAddress": {"type": "string", "description": ""},
                    "locality": {"type": "string", "description": ""},
                    "region": {"type": "string", "description": ""},
                    "postalCode": {"type": "string", "description": ""},
                    "extendedAddress": {"type": "array", "items": {"type": "string"}},
                    "countryName": {"type": "string", "description": ""}
                  },
                  "required": ["streetAddress", "locality", "region", "postalCode"]
                },
                "id": {"type": "object", "description": ""},
                "institutionId": {"type": "object", "description": ""},
                "suggestedId": {"type": "object", "description": ""},
                "status": {"type": "string", "description": ""},
                "requiresModeration": {"type": "boolean", "description": ""},
                "isInvestigator": {"type": "boolean", "description": ""},
                "email": {"type": "email", "description": ""},
                "emailValidationToken": {"type": "string", "description": ""},
                "isNewInstitution": {"type": "boolean", "description": ""},
                "nextAction": {"type": "string", "description": ""},
                "institutionNameSuggested": {"type": "string", "description": ""},
                "code": {"type": "string", "description": ""},
                "name": {"type": "string", "description": ""},
                "roles": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object", "description": ""},
                      "code": {"type": "string", "description": ""},
                      "status": {"type": "string", "description": ""},
                      "requiresModeration": {"type": "boolean", "description": ""},
                      "label": {"type": "string", "description": ""}
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
          "nextAction": {"type": "string", "description": ""}
        },
        "required": ["id", "account", "username", "title", "firstName", "lastName", "nextAction"]
      }
    }
  }
}
```



        
        Gets the list of users that the authenticated user can moderate.  This will include new accounts, institutions
        added to accounts, and roles added to users at institutions.
        
        
        - If the user has the <strong>system:admin</strong> role, then they will get the full list of users to be moderated in the system  
        
        - If the user has the <strong>institution:admin</strong> role, they will get the list of users to be moderated for their specific institution(s)
        
        

### HTTP Request

`GET /admin/moderation/user`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | N/A