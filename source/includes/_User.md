
# User


## UserConfidentiality - <em>Update Confidentiality</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/user/:userId/confidentiality"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
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


Lets a user update there agreement to the confidentiality agreement

### HTTP Request

`PUT /user/:userId/confidentiality`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A

## UserCreation - <em>Create a new user account</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/user/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/UserCreation",
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
}
```


> Response Schema

```json
{
  "id": "/UserCreationResponse",
  "type": "object",
  "properties": {
    "user": {
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "username": {"type": "string"},
        "userInstitutionId": {"type": "object"},
        "institutionId": {"type": "object|null"},
        "isAccessEmailSent": {"type": "boolean"},
        "isAccountModerated": {"type": "boolean"},
        "moderationResults": {"type": "object"}
      },
      "required": [
        "id",
        "userInstitutionId",
        "institutionId",
        "isAccessEmailSent",
        "isAccountModerated"
      ]
    },
    "validationEmail": {"type": "object"},
    "comments": {"type": "array"}
  }
}
```


Task used when a user creates an account for another user. This task is for administrators

### HTTP Request

`POST /user/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
institution | admin | N/A|If the institution specified in the request matches the target, the request is automatically approved.

## UserDocumentDelete - <em>Delete a User Document</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/user/:userId/document/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserDocumentDelete",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "documentId": {"type": "string"}},
    "required": ["userId", "documentId"]
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


Deletes a specified document from a user account

### HTTP Request

`DELETE /user/:userId/document/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserDocumentDownload - <em>Download User Document</em>


```shell
curl "https://ctoregistry.com/api/v1/download/user/:userId/document/:documentId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/DownloadDocument",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "documentId": {"type": "string"}},
    "required": ["userId", "documentId"]
  }
}
```


> Response Schema

```json
undefined
```


Downloads a specified document from the specified user.

### HTTP Request

`GET /download/user/:userId/document/:documentId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A
committee | member | user|N/A

## UserDocumentUpload - <em>Upload Document</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/upload/user/:userId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
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
  },
  "params": {
    "id": "UserDocumentUpdateParams",
    "type": "object",
    "properties": {"userId": {"type": "string"}},
    "required": ["userId"]
  }
}
```


> Response Schema

```json
{
  "id": "/UserDocumentUploadResponse",
  "type": "object",
  "properties": {
    "document": {
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "type": {"type": "string"},
        "subCode": {"type": "string"},
        "expiryDt": {"type": "date"},
        "uploadDt": {"type": "date"},
        "completeDt": {"type": "date"},
        "originalFilename": {"type": "string"},
        "filename": {"type": "string"}
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
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserInstitutionCreation - <em>Add an institution to a user account</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/user/:userId/institution"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
  },
  "body": {
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


> Response Schema

```json
{
  "id": "/UserCreationResponse",
  "type": "object",
  "properties": {
    "user": {
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "username": {"type": "string"},
        "userInstitutionId": {"type": "object"},
        "institutionId": {"type": "object|null"},
        "isAccessEmailSent": {"type": "boolean"},
        "isAccountModerated": {"type": "boolean"},
        "moderationResults": {"type": "object"}
      },
      "required": [
        "id",
        "userInstitutionId",
        "institutionId",
        "isAccessEmailSent",
        "isAccountModerated"
      ]
    },
    "validationEmail": {"type": "object"},
    "comments": {"type": "array"}
  }
}
```


Add an institution to a user account. The request needs moderation

### HTTP Request

`POST /user/:userId/institution`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserInstitutionProfile - <em>Get the info about one institution from a users account</em>


```shell
curl "https://ctoregistry.com/api/v1/user/:userId/institution/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserInstitutionParams",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["userId", "institutionId"]
  }
}
```


> Response Schema

```json
{
  "id": "/UserInstitutionResponse",
  "type": "object",
  "properties": {
    "userInstitution": {
      "id": "/UserInstitution",
      "properties": {
        "userInstitutionId": {"type": "object"},
        "name": {"type": "string"},
        "code": {"type": "string"},
        "status": {"type": "string"},
        "institutionId": {"type": "object"},
        "isPrimary": {"type": "boolean"},
        "isPublished": {"type": "boolean"},
        "isEmailValidated": {"type": "boolean"},
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
        "email": {"type": "email"},
        "phones": {
          "type": "array",
          "items": {
            "id": "/Phone",
            "type": "object",
            "properties": {
              "number": {"type": "string"},
              "extension": {"type": "string|null"},
              "type": {
                "type": "string|null",
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
              "id": {"type": "object"},
              "code": {"type": "string"},
              "label": {"type": "string"},
              "status": {"type": "string"}
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
        "email",
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
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A
committee | member | user|The user has a role on a study, and the study is assigned to the privilege target REB.

## UserInstitutionRoleCreation - <em>Add a role to the owner of current account</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/user/:userId/institution/:institutionId/role"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserInstitutionParams",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["userId", "institutionId"]
  },
  "body": {
    "id": "/UserInstitutionRoleCreation",
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


This task is used when the owner of an account wants to add a role to his/her account

### HTTP Request

`POST /user/:userId/institution/:institutionId/role`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserInstitutionRoleDelete - <em>Delete an institution role</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/user/:userId/institution/:institutionId/role/:roleId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserInstitutionRoleDelete",
    "type": "object",
    "properties": {
      "userId": {"type": "string"},
      "institutionId": {"type": "string"},
      "roleId": {"type": "string"}
    },
    "required": ["userId", "institutionId", "roleId"]
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


This task is used when the owner of an account wants to remove a role to his/her account

### HTTP Request

`DELETE /user/:userId/institution/:institutionId/role/:roleId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserInstitutionUpdate - <em>Add an institution to a user account</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/user/:userId/institution/:institutionId/update"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserInstitutionParams",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["userId", "institutionId"]
  },
  "body": {
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


Add an institution to a user account. The request needs moderation. 
        If the email address used is not already validated in the users account then the status returned will be 
        "emailValidationSent 
        

### HTTP Request

`POST /user/:userId/institution/:institutionId/update`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserList - <em>Get the list of users</em>


```shell
curl "https://ctoregistry.com/api/v1/user/"  
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
      "status": {"type": "string"}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/UserListResponse",
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
        "id": "/User",
        "properties": {
          "id": {"type": "object"},
          "username": {"type": "string"},
          "account": {
            "id": "/UserAccount",
            "properties": {
              "isPasswordSet": {"type": "boolean"},
              "isNewAccount": {"type": "boolean"},
              "updateDt": {"type": "date"},
              "createDt": {"type": "date"},
              "status": {
                "type": "string",
                "enum": ["verified", "disabled", "unverified", "suspended", "deleted"]
              }
            },
            "required": ["isPasswordSet", "isNewAccount", "updateDt", "createDt", "status"]
          },
          "contact": {
            "id": "/UserContact",
            "properties": {
              "status": {"type": "string"},
              "title": {
                "type": "string",
                "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
              },
              "firstName": {"type": "string"},
              "middleName": {"type": "string|null"},
              "lastName": {"type": "string"},
              "privacy": {
                "type": "string",
                "enum": ["public", "private", "institution", "members"]
              },
              "isDraft": {"type": "boolean"}
            },
            "required": ["status", "title", "firstName", "lastName", "privacy", "isDraft"]
          },
          "confidentiality": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {"agreeDt": {"type": "date"}, "version": {"type": "string"}},
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
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
institution | admin | N/A|User is a member at, or their request involves the target institution of the privilege.
committee | member | N/A|The user has a role on a study, and the study is assigned to the privilege target REB.

## UserPasswordUpdate - <em>Update Password</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/user/password/update"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/UserPasswordUpdate",
    "type": "object",
    "properties": {
      "userId": {"type": "string", "description": "User ID"},
      "password": {"type": "string", "description": "The current password"},
      "newPassword": {"type": "string", "description": "The new password"}
    },
    "required": ["userId", "newPassword"]
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


Lets a user update there password

### HTTP Request

`POST /user/password/update`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A

## UserPrivilegeCreation - <em>Add User Privilege</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/user/:userId/privileges"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
  },
  "body": {
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


Adds a new privilege to a user account

### HTTP Request

`POST /user/:userId/privileges`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## UserPrivilegeDelete - <em>Delete a User Privilege</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/user/:userId/privileges/:privilegeId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserPrivilegeDelete",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "privilegeId": {"type": "string"}},
    "required": ["userId", "privilegeId"]
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


Deletes a specified privilege from a user account

### HTTP Request

`DELETE /user/:userId/privileges/:privilegeId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## UserPrivileges - <em>User's privileges</em>


```shell
curl "https://ctoregistry.com/api/v1/user/:userId/privileges"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
  }
}
```


> Response Schema

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
          "id": {"type": "object|null"},
          "scope": {"type": "string"},
          "role": {"type": "string"},
          "target": {"type": "object|null"},
          "targetName": {"type": "string|null"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
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
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserProfile - <em>Get User Profile</em>


```shell
curl "https://ctoregistry.com/api/v1/user/:userId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
  }
}
```


> Response Schema

```json
{
  "id": "/UserProfileResponse",
  "type": "object",
  "properties": {
    "user": {
      "id": "/User",
      "properties": {
        "id": {"type": "object"},
        "username": {"type": "string"},
        "account": {
          "id": "/UserAccount",
          "properties": {
            "isPasswordSet": {"type": "boolean"},
            "isNewAccount": {"type": "boolean"},
            "updateDt": {"type": "date"},
            "createDt": {"type": "date"},
            "status": {
              "type": "string",
              "enum": ["verified", "disabled", "unverified", "suspended", "deleted"]
            }
          },
          "required": ["isPasswordSet", "isNewAccount", "updateDt", "createDt", "status"]
        },
        "contact": {
          "id": "/UserContact",
          "properties": {
            "status": {"type": "string"},
            "title": {
              "type": "string",
              "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
            },
            "firstName": {"type": "string"},
            "middleName": {"type": "string|null"},
            "lastName": {"type": "string"},
            "privacy": {"type": "string", "enum": ["public", "private", "institution", "members"]},
            "isDraft": {"type": "boolean"}
          },
          "required": ["status", "title", "firstName", "lastName", "privacy", "isDraft"]
        },
        "confidentiality": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {"agreeDt": {"type": "date"}, "version": {"type": "string"}},
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
              "userInstitutionId": {"type": "object"},
              "name": {"type": "string"},
              "code": {"type": "string"},
              "status": {"type": "string"},
              "institutionId": {"type": "object"},
              "isPrimary": {"type": "boolean"},
              "isPublished": {"type": "boolean"},
              "isEmailValidated": {"type": "boolean"},
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
              "email": {"type": "email"},
              "phones": {
                "type": "array",
                "items": {
                  "id": "/Phone",
                  "type": "object",
                  "properties": {
                    "number": {"type": "string"},
                    "extension": {"type": "string|null"},
                    "type": {
                      "type": "string|null",
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
                    "id": {"type": "object"},
                    "code": {"type": "string"},
                    "label": {"type": "string"},
                    "status": {"type": "string"}
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
              "email",
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
                  "id": {"type": "object"},
                  "type": {"type": "string"},
                  "subCode": {"type": "string"},
                  "expiryDt": {"type": "date"},
                  "value": {"type": "string"},
                  "vendor": {"type": "string"},
                  "vendorOther": {"type": "string"},
                  "completeDt": {"type": "date"},
                  "originalFilename": {"type": "string"},
                  "uploadDt": {"type": "date"},
                  "description": {"type": "string"},
                  "filename": {"type": "string"}
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
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
committee | admin | user|N/A
institution | admin | user|N/A

## UserProfileUpdate - <em>User Profile Update</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/user/:userId/profile"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
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
  },
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
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


Lets an admin or the user themselves update a users profile information

### HTTP Request

`PUT /user/:userId/profile`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## UserStudyList - <em>Get User Studies</em>


```shell
curl "https://ctoregistry.com/api/v1/user/:userId/study"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
  }
}
```


> Response Schema

```json
{
  "id": "/UserStudyListResponse",
  "type": "object",
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
    "data": {
      "type": "array",
      "items": {
        "id": "/Study",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "isInvestigatorInitiatedStudy": {"type": "boolean"},
          "sponsor": {"type": "string|null"},
          "sponsorId": {"type": "object"},
          "ohrp": {"type": "boolean"},
          "fda": {"type": "boolean"},
          "observational": {"type": "boolean"},
          "provincialStatus": {"type": "string"},
          "expiryDt": {"type": "date|null"},
          "shortTitle": {"type": "string"},
          "title": {"type": "string|null"},
          "reviewerLink": {"type": "string"},
          "applicantLink": {"type": "string"},
          "reb": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
            "required": ["name"]
          },
          "projectIdNumber": {"type": "number"},
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "isInvestigatorInitiatedStudy",
          "sponsor",
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
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A