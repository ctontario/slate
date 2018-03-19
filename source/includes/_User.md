
# User


## UserConfidentiality - <em>Update Confidentiality</em>


```shell
curl -X PUT "https://cto.local:9000/api/v1/user/:userId/confidentiality"  
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


Lets a user update there agreement to the confidentiality agreement

### HTTP Request

`PUT /user/:userId/confidentiality`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A

## UserCreation - <em>Create a new user account</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/user/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/User",
  "type": "object",
  "properties": {
    "username": {"type": "string", "description": "User ID"},
    "firstName": {"type": "string", "description": "First name"},
    "middleName": {"type": "string", "description": "Middle name"},
    "lastName": {"type": "string", "description": "Last Name"},
    "title": {
      "type": "string",
      "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"],
      "description": "Title"
    },
    "institution": {
      "id": "/UserInstitution",
      "type": "object",
      "properties": {
        "code": {"type": "string", "description": "The institution code"},
        "name": {"type": "string", "maxLength": 200, "description": "The institution name"},
        "isInvestigator": {
          "type": "boolean",
          "description": "Whether the user was indicated as an investigator or not"
        },
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
        "email": {"type": "string", "format": "email", "description": "Email"},
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
        "privacy": {"type": "string", "enum": ["public", "private", "institution", "members"]}
      },
      "anyOf": [{"required": ["name"]}, {"required": ["code"]}],
      "required": ["address", "email", "phones", "isInvestigator"]
    },
    "confidentiality": {
      "type": "boolean",
      "description": "Whether the user agreed to the confidentiality agreement"
    }
  },
  "required": ["username", "firstName", "lastName", "title", "institution"]
}
```


> Response Body Schema

```json
{
  "id": "/RegisterResponse",
  "type": "object",
  "properties": {
    "user": {
      "type": "object",
      "properties": {
        "id": {"type": "object", "description": ""},
        "username": {"type": "string", "description": ""},
        "userInstitutionId": {"type": "object", "description": ""},
        "institutionId": {"type": "object|null", "description": ""},
        "isAccessEmailSent": {"type": "boolean", "description": ""},
        "isAccountModerated": {"type": "boolean", "description": ""},
        "moderationResults": {"type": "object", "description": ""}
      },
      "required": [
        "id",
        "userInstitutionId",
        "institutionId",
        "isAccessEmailSent",
        "isAccountModerated"
      ]
    },
    "validationEmail": {"type": "object", "description": ""},
    "comments": {"type": "array"}
  }
}
```


Task used when a user creates an account for another user. This task is for administrators

### HTTP Request

`POST /user/`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | N/A

## UserDocumentDelete - <em>Delete a User Document</em>


```shell
curl -X DELETE "https://cto.local:9000/api/v1/user/:userId/document/:documentId"  
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


Deletes a specified document from a user account

### HTTP Request

`DELETE /user/:userId/document/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserDocumentUpload - <em>Upload Document</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/upload/user/:userId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/UserDocumentUpload",
  "type": "object",
  "properties": {
    "type": {"type": "string", "description": "The document type"},
    "completeDt": {"type": "date", "description": "The institution name"},
    "vendor": {"type": "string", "description": "The document vendor"},
    "vendorOther": {"type": "string", "description": "The document vendor (other) text"},
    "value": {"type": "string", "description": "The document value, if a medical license number"},
    "description": {"type": "string", "description": "The document description"},
    "subCode": {"type": "string", "description": "The document sub code"}
  },
  "required": ["type"]
}
```


> Response Body Schema

```json
{
  "id": "/UserDocumentUploadResponse",
  "type": "object",
  "properties": {
    "document": {
      "type": "object",
      "properties": {
        "id": {"type": "object", "description": ""},
        "type": {"type": "string", "description": ""},
        "subCode": {"type": "string", "description": ""},
        "expiryDt": {"type": "date", "description": ""},
        "uploadDt": {"type": "date", "description": ""},
        "completeDt": {"type": "date", "description": ""},
        "originalFilename": {"type": "string", "description": ""},
        "filename": {"type": "string", "description": ""}
      },
      "required": [
        "id",
        "type",
        "expiryDt",
        "uploadDt",
        "completeDt",
        "originalFilename",
        "filename"
      ]
    }
  }
}
```


Uploads a document to the specified user.  The document information is contained in the POST

### HTTP Request

`POST /upload/user/:userId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserDownloadDocument - <em>Download User Document</em>


```shell
curl "https://cto.local:9000/api/v1/download/user/:userId/document/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
undefined
```


Downloads a specified document from the specified user.

### HTTP Request

`GET /download/user/:userId/document/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user
committee | member | user

## UserInstitutionAddRole - <em>Add a role to the owner of current account</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/user/:userId/institution/:institutionId/role"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/UserInstitutionAddRoleRequest",
  "type": "object",
  "properties": {
    "roles": {
      "type": "array",
      "items": {"type": "string"},
      "minItems": 1,
      "maxItems": 5,
      "uniqueItems": true,
      "description": "The list of roles to request"
    }
  },
  "required": ["roles"]
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


This task is used when the owner of an account wants to add a role to his/her account

### HTTP Request

`POST /user/:userId/institution/:institutionId/role`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserInstitutionCreation - <em>Add an institution to a user account</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/user/:userId/institution"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "path": "/UserInstitution",
  "schema": {
    "id": "/UserInstitution",
    "type": "object",
    "properties": {
      "code": {"type": "string", "description": "The institution code"},
      "name": {"type": "string", "maxLength": 200, "description": "The institution name"},
      "isInvestigator": {
        "type": "boolean",
        "description": "Whether the user was indicated as an investigator or not"
      },
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
      "email": {"type": "string", "format": "email", "description": "Email"},
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
      "privacy": {"type": "string", "enum": ["public", "private", "institution", "members"]}
    },
    "anyOf": [{"required": ["name"]}, {"required": ["code"]}],
    "required": ["address", "email", "phones", "isInvestigator"]
  }
}
```


> Response Body Schema

```json
{
  "id": "/RegisterResponse",
  "type": "object",
  "properties": {
    "user": {
      "type": "object",
      "properties": {
        "id": {"type": "object", "description": ""},
        "username": {"type": "string", "description": ""},
        "userInstitutionId": {"type": "object", "description": ""},
        "institutionId": {"type": "object|null", "description": ""},
        "isAccessEmailSent": {"type": "boolean", "description": ""},
        "isAccountModerated": {"type": "boolean", "description": ""},
        "moderationResults": {"type": "object", "description": ""}
      },
      "required": [
        "id",
        "userInstitutionId",
        "institutionId",
        "isAccessEmailSent",
        "isAccountModerated"
      ]
    },
    "validationEmail": {"type": "object", "description": ""},
    "comments": {"type": "array"}
  }
}
```


Add an institution to a user account. The request needs moderation

### HTTP Request

`POST /user/:userId/institution`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserInstitutionDeleteRole - <em>Delete an institution role</em>


```shell
curl -X DELETE "https://cto.local:9000/api/v1/user/:userId/institution/:institutionId/role/:roleId"  
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


This task is used when the owner of an account wants to remove a role to his/her account

### HTTP Request

`DELETE /user/:userId/institution/:institutionId/role/:roleId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserInstitutionProfile - <em>Get the info about one institution from a users account</em>


```shell
curl "https://cto.local:9000/api/v1/user/:userId/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/UserInstitutionResponse",
  "type": "object",
  "properties": {
    "userInstitution": {
      "id": "/UserInstitution",
      "properties": {
        "userInstitutionId": {"type": "object", "description": ""},
        "name": {"type": "string", "description": ""},
        "code": {"type": "string", "description": ""},
        "status": {"type": "string", "description": ""},
        "institutionId": {"type": "object", "description": ""},
        "isPrimary": {"type": "boolean", "description": ""},
        "isPublished": {"type": "boolean", "description": ""},
        "isEmailValidated": {"type": "boolean", "description": ""},
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
        "email": {"type": "email", "description": ""},
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
        "roles": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "id": {"type": "object", "description": ""},
              "code": {"type": "string", "description": ""},
              "label": {"type": "string", "description": ""},
              "status": {"type": "string", "description": ""}
            },
            "required": ["id", "code", "label", "status"]
          }
        }
      },
      "required": [
        "userInstitutionId",
        "name",
        "code",
        "status",
        "isPrimary",
        "isPublished",
        "isEmailValidated",
        "address",
        "email",
        "phones",
        "roles"
      ]
    }
  }
}
```


Gets the full information about a users institution for use in the edit institution page.

### HTTP Request

`GET /user/:userId/institution/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user
committee | member | user

## UserInstitutionUpdate - <em>Add an institution to a user account</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/user/:userId/institution/:institutionId/update"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/UserInstitutionUpdate",
  "type": "object",
  "properties": {
    "code": {"type": "string", "description": "The institution code"},
    "name": {"type": "string", "maxLength": 200, "description": "The institution name"},
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
    "email": {"type": "string", "format": "email", "description": "Email"},
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
    "privacy": {"type": "string", "enum": ["public", "private", "institution", "members"]}
  }
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


Add an institution to a user account. The request needs moderation. 
        If the email address used is not already validated in the users account then the status returned will be 
        "emailValidationSent 
        

### HTTP Request

`POST /user/:userId/institution/:institutionId/update`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserList - <em>Get the list of users</em>


```shell
curl "https://cto.local:9000/api/v1/user/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/UserListResponse",
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
        "id": "/User",
        "properties": {
          "id": {"type": "object", "description": ""},
          "username": {"type": "string", "description": ""},
          "account": {
            "id": "/UserAccount",
            "properties": {
              "isPasswordSet": {"type": "boolean", "description": ""},
              "isNewAccount": {"type": "boolean", "description": ""},
              "updateDt": {"type": "date", "description": ""},
              "createDt": {"type": "date", "description": ""},
              "status": {
                "type": "string",
                "description": "",
                "enum": ["verified", "disabled", "unverified", "suspended", "deleted"]
              }
            },
            "required": ["isPasswordSet", "isNewAccount", "updateDt", "createDt", "status"]
          },
          "contact": {
            "id": "/UserContact",
            "properties": {
              "status": {"type": "string", "description": ""},
              "title": {
                "type": "string",
                "description": "",
                "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
              },
              "firstName": {"type": "string", "description": ""},
              "middleName": {"type": "string|null", "description": ""},
              "lastName": {"type": "string", "description": ""},
              "privacy": {
                "type": "string",
                "description": "",
                "enum": ["public", "private", "institution", "members"]
              },
              "isDraft": {"type": "boolean", "description": ""}
            },
            "required": ["status", "title", "firstName", "lastName", "privacy", "isDraft"]
          },
          "confidentiality": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "agreeDt": {"type": "date", "description": ""},
                "version": {"type": "string", "description": ""}
              },
              "required": ["agreeDt", "version"]
            }
          },
          "institutionIds": {"type": "array", "items": {"type": "object"}},
          "committeeIds": {"type": "array", "items": {"type": "object"}}
        },
        "required": [
          "id",
          "username",
          "account",
          "contact",
          "confidentiality",
          "institutionIds",
          "committeeIds"
        ]
      }
    }
  }
}
```


Returns the list of all the users in the system

### HTTP Request

`GET /user/`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | admin | N/A
committee | member | N/A

## UserPasswordUpdate - <em>Update Password</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/user/password/update"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/UserPasswordUpdate",
  "type": "object",
  "properties": {
    "userId": {"type": "string", "description": "User ID"},
    "password": {"type": "string", "description": "The current password"},
    "newPassword": {"type": "string", "description": "The new password"}
  },
  "required": ["userId", "newPassword"]
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


Lets a user update there password

### HTTP Request

`POST /user/password/update`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A

## UserPrivilegeCreation - <em>Add User Privilege</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/user/:userId/privileges"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/UserPrivilegeCreation",
  "type": "object",
  "properties": {
    "scope": {
      "type": "string",
      "description": "The scope of the privilege",
      "enum": ["system", "institution", "account"]
    },
    "target": {
      "type": ["string", "null"],
      "description": "The target (e.g.: the institution ID if the scope is 'institution' or a user ID if the scope is 'account')"
    },
    "role": {"type": "string", "description": "The role assigned to the privilege"},
    "expiryDt": {"type": "Date", "description": "The date the privilege will expire"}
  },
  "required": ["scope", "role"]
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


Adds a new privilege to a user account

### HTTP Request

`POST /user/:userId/privileges`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## UserPrivilegeDelete - <em>Delete a User Privilege</em>


```shell
curl -X DELETE "https://cto.local:9000/api/v1/user/:userId/privileges/:privilegeId"  
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


Deletes a specified privilege from a user account

### HTTP Request

`DELETE /user/:userId/privileges/:privilegeId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A

## UserPrivileges - <em>User's privileges</em>


```shell
curl "https://cto.local:9000/api/v1/user/:userId/privileges"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/UserPrivilegesResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object|null", "description": ""},
          "scope": {"type": "string", "description": ""},
          "role": {"type": "string", "description": ""},
          "target": {"type": "object|null", "description": ""},
          "targetName": {"type": "string|null", "description": ""},
          "createDt": {"type": "date", "description": ""},
          "updateDt": {"type": "date", "description": ""}
        },
        "required": ["id", "scope", "role", "target", "targetName", "createDt", "updateDt"]
      }
    }
  }
}
```


Returns the list of the privileges assigned to a user

### HTTP Request

`GET /user/:userId/privileges`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserProfile - <em>Get User Profile</em>


```shell
curl "https://cto.local:9000/api/v1/user/:userId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/UserProfileResponse",
  "type": "object",
  "properties": {
    "user": {
      "id": "/User",
      "properties": {
        "id": {"type": "object", "description": ""},
        "username": {"type": "string", "description": ""},
        "account": {
          "id": "/UserAccount",
          "properties": {
            "isPasswordSet": {"type": "boolean", "description": ""},
            "isNewAccount": {"type": "boolean", "description": ""},
            "updateDt": {"type": "date", "description": ""},
            "createDt": {"type": "date", "description": ""},
            "status": {
              "type": "string",
              "description": "",
              "enum": ["verified", "disabled", "unverified", "suspended", "deleted"]
            }
          },
          "required": ["isPasswordSet", "isNewAccount", "updateDt", "createDt", "status"]
        },
        "contact": {
          "id": "/UserContact",
          "properties": {
            "status": {"type": "string", "description": ""},
            "title": {
              "type": "string",
              "description": "",
              "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
            },
            "firstName": {"type": "string", "description": ""},
            "middleName": {"type": "string|null", "description": ""},
            "lastName": {"type": "string", "description": ""},
            "privacy": {
              "type": "string",
              "description": "",
              "enum": ["public", "private", "institution", "members"]
            },
            "isDraft": {"type": "boolean", "description": ""}
          },
          "required": ["status", "title", "firstName", "lastName", "privacy", "isDraft"]
        },
        "confidentiality": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "agreeDt": {"type": "date", "description": ""},
              "version": {"type": "string", "description": ""}
            },
            "required": ["agreeDt", "version"]
          }
        },
        "institutionIds": {"type": "array", "items": {"type": "object"}},
        "committeeIds": {"type": "array", "items": {"type": "object"}},
        "institutions": {
          "type": "array",
          "items": {
            "id": "/UserInstitution",
            "properties": {
              "userInstitutionId": {"type": "object", "description": ""},
              "name": {"type": "string", "description": ""},
              "code": {"type": "string", "description": ""},
              "status": {"type": "string", "description": ""},
              "institutionId": {"type": "object", "description": ""},
              "isPrimary": {"type": "boolean", "description": ""},
              "isPublished": {"type": "boolean", "description": ""},
              "isEmailValidated": {"type": "boolean", "description": ""},
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
              "email": {"type": "email", "description": ""},
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
              "roles": {
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "object", "description": ""},
                    "code": {"type": "string", "description": ""},
                    "label": {"type": "string", "description": ""},
                    "status": {"type": "string", "description": ""}
                  },
                  "required": ["id", "code", "label", "status"]
                }
              }
            },
            "required": [
              "userInstitutionId",
              "name",
              "code",
              "status",
              "isPrimary",
              "isPublished",
              "isEmailValidated",
              "address",
              "email",
              "phones",
              "roles"
            ]
          }
        },
        "documents": {
          "type": "object",
          "properties": {
            "uploaded": {
              "type": "array",
              "items": {
                "id": "/UserDocument",
                "properties": {
                  "id": {"type": "object", "description": ""},
                  "type": {"type": "string", "description": ""},
                  "subCode": {"type": "string", "description": ""},
                  "expiryDt": {"type": "date", "description": ""},
                  "value": {"type": "string", "description": ""},
                  "vendor": {"type": "string", "description": ""},
                  "vendorOther": {"type": "string", "description": ""},
                  "completeDt": {"type": "date", "description": ""},
                  "originalFilename": {"type": "string", "description": ""},
                  "uploadDt": {"type": "date", "description": ""},
                  "description": {"type": "string", "description": ""},
                  "filename": {"type": "string", "description": ""}
                },
                "required": ["id", "type", "uploadDt"]
              }
            },
            "required": {"type": "array"},
            "allowed": {"type": "array"}
          }
        }
      },
      "required": [
        "id",
        "username",
        "account",
        "contact",
        "confidentiality",
        "institutionIds",
        "committeeIds"
      ]
    }
  }
}
```


Get the profile for the user with id

### HTTP Request

`GET /user/:userId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
committee | member | user
institution | admin | user

## UserStudyList - <em>Get User Studies</em>


```shell
curl "https://cto.local:9000/api/v1/user/:userId/study"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/UserStudyListResponse",
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
        "id": "/Study",
        "type": "object",
        "properties": {
          "id": {"type": "object", "description": ""},
          "isInvestigatorInitiatedStudy": {"type": "boolean", "description": ""},
          "sponsor": {"type": "string|null", "description": ""},
          "sponsorId": {"type": "object", "description": ""},
          "ctaita": {"type": "boolean", "description": ""},
          "ctaitaTypes": {
            "type": "array",
            "description": "",
            "items": {"type": "string", "enum": ["cta_fda", "cta_nhp", "ita_med_devices"]}
          },
          "ohrp": {"type": "boolean", "description": ""},
          "fda": {"type": "boolean", "description": ""},
          "observational": {"type": "boolean", "description": ""},
          "provincialStatus": {"type": "string", "description": ""},
          "expiryDt": {"type": "date|null", "description": ""},
          "shortTitle": {"type": "string", "description": ""},
          "title": {"type": "string|null", "description": ""},
          "reviewerLink": {"type": "string", "description": ""},
          "applicantLink": {"type": "string", "description": ""},
          "reb": {
            "type": "object",
            "properties": {
              "id": {"type": "object", "description": ""},
              "name": {"type": "string", "description": ""}
            },
            "required": ["name"]
          },
          "projectIdNumber": {"type": "number", "description": ""},
          "createDt": {"type": "date", "description": ""},
          "updateDt": {"type": "date", "description": ""},
          "provincialApplication": {
            "type": "object",
            "properties": {
              "studyContact": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": "string|null", "description": ""},
                  "firstName": {"type": "string|null", "description": ""},
                  "lastName": {"type": "string|null", "description": ""},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object", "description": ""},
                      "firstName": {"type": "string", "description": ""},
                      "lastName": {"type": "string", "description": ""},
                      "title": {
                        "type": "string",
                        "description": "",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName", "title"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "projectOwner": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": "string|null", "description": ""},
                  "firstName": {"type": "string|null", "description": ""},
                  "lastName": {"type": "string|null", "description": ""},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object", "description": ""},
                      "firstName": {"type": "string", "description": ""},
                      "lastName": {"type": "string", "description": ""},
                      "title": {
                        "type": "string",
                        "description": "",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName", "title"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "provincialApplicant": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": "string|null", "description": ""},
                  "firstName": {"type": "string|null", "description": ""},
                  "lastName": {"type": "string|null", "description": ""},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object", "description": ""},
                      "firstName": {"type": "string", "description": ""},
                      "lastName": {"type": "string", "description": ""},
                      "title": {
                        "type": "string",
                        "description": "",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName", "title"]
                  }
                },
                "required": ["firstName", "lastName"]
              }
            }
          },
          "centreApplications": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "institutionId": {"type": "object", "description": ""},
                "name": {"type": "string", "description": ""},
                "status": {"type": "string", "description": ""},
                "principalInvestigator": {
                  "id": "/StudyUser",
                  "properties": {
                    "email": {"type": "string|null", "description": ""},
                    "firstName": {"type": "string|null", "description": ""},
                    "lastName": {"type": "string|null", "description": ""},
                    "user": {
                      "type": "object",
                      "properties": {
                        "id": {"type": "object", "description": ""},
                        "firstName": {"type": "string", "description": ""},
                        "lastName": {"type": "string", "description": ""},
                        "title": {
                          "type": "string",
                          "description": "",
                          "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                        }
                      },
                      "required": ["id", "firstName", "lastName", "title"]
                    }
                  },
                  "required": ["firstName", "lastName"]
                },
                "principalCoInvestigator": {
                  "id": "/StudyUser",
                  "properties": {
                    "email": {"type": "string|null", "description": ""},
                    "firstName": {"type": "string|null", "description": ""},
                    "lastName": {"type": "string|null", "description": ""},
                    "user": {
                      "type": "object",
                      "properties": {
                        "id": {"type": "object", "description": ""},
                        "firstName": {"type": "string", "description": ""},
                        "lastName": {"type": "string", "description": ""},
                        "title": {
                          "type": "string",
                          "description": "",
                          "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                        }
                      },
                      "required": ["id", "firstName", "lastName", "title"]
                    }
                  },
                  "required": ["firstName", "lastName"]
                },
                "mainStudyContact": {
                  "id": "/StudyUser",
                  "properties": {
                    "email": {"type": "string|null", "description": ""},
                    "firstName": {"type": "string|null", "description": ""},
                    "lastName": {"type": "string|null", "description": ""},
                    "user": {
                      "type": "object",
                      "properties": {
                        "id": {"type": "object", "description": ""},
                        "firstName": {"type": "string", "description": ""},
                        "lastName": {"type": "string", "description": ""},
                        "title": {
                          "type": "string",
                          "description": "",
                          "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                        }
                      },
                      "required": ["id", "firstName", "lastName", "title"]
                    }
                  },
                  "required": ["firstName", "lastName"]
                }
              },
              "required": ["name", "status"]
            }
          }
        },
        "required": [
          "id",
          "isInvestigatorInitiatedStudy",
          "sponsor",
          "ctaita",
          "ctaitaTypes",
          "ohrp",
          "fda",
          "observational",
          "provincialStatus",
          "expiryDt",
          "shortTitle",
          "title",
          "reviewerLink",
          "applicantLink",
          "reb",
          "projectIdNumber",
          "createDt",
          "updateDt"
        ]
      }
    }
  }
}
```


Get all the studies that a user can access

### HTTP Request

`GET /user/:userId/study`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user

## UserProfileUpdate - <em>User Profile Update</em>


```shell
curl -X PUT "https://cto.local:9000/api/v1/user/:userId/profile"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/UserProfileUpdate",
  "type": "object",
  "properties": {
    "username": {"type": "string", "description": "Username"},
    "firstName": {"type": "string", "description": "First name"},
    "middleName": {"type": "string", "description": "Middle name"},
    "lastName": {"type": "string", "description": "Last Name"},
    "title": {
      "type": "string",
      "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"],
      "description": "Title"
    }
  },
  "required": ["firstName", "lastName", "title"]
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


Lets an admin or the user themselves update a users profile information

### HTTP Request

`PUT /user/:userId/profile`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
self | N/A | N/A
system | admin | N/A
institution | admin | user