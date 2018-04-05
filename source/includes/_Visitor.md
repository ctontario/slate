
# Visitor


## EmailCheckExists - <em>Verify if an email address is already used</em>


```shell
curl "https://www.ctoregistry.com/api/v1/visitor/email/unique/:email"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserUniqueEmail",
    "type": "object",
    "properties": {"email": {"type": "string"}, "userId": {"type": "string"}},
    "required": ["email"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Verify if an email address is already used in the system. This is used during the registration process 
        to make sure that no two users have the same email

### HTTP Request

`GET /visitor/email/unique/:email`



### Authorization
 
N/A

## EmailCheckExistsExceptUser - <em>Verify if an email address is already used except by user with id set to 'userId'</em>


```shell
curl "https://www.ctoregistry.com/api/v1/visitor/email/unique/:email/:userId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserUniqueEmail",
    "type": "object",
    "properties": {"email": {"type": "string"}, "userId": {"type": "string"}},
    "required": ["email"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Verify if an email address is already used in the system except in the specified user account. 
        This is used during the process to add an institution to make sure that no two users use the same email

### HTTP Request

`GET /visitor/email/unique/:email/:userId`



### Authorization
 
N/A

## EmailValidation - <em>Validate an email address with a token</em>


```shell
curl "https://www.ctoregistry.com/api/v1/validation/email/:token"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/EmailValidation",
    "type": "object",
    "properties": {"token": {"type": "string"}},
    "required": ["token"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Task used to validate a user's email with a token. The token is embedded in a link that is send
        to email address provided by the user

### HTTP Request

`GET /validation/email/:token`



### Authorization
 
N/A

## EmailValidationResend - <em>Resend Email Validation</em>


```shell
curl "https://www.ctoregistry.com/api/v1/validation/resend/:userId/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/EmailValidationResend",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["userId", "institutionId"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Re-sends a validation email to an existing email address for an existing user account

### HTTP Request

`GET /validation/resend/:userId/:institutionId`



### Authorization
 
N/A

## InstitutionSearch - <em>Search Institutions</em>


```shell
curl "https://www.ctoregistry.com/api/v1/dictionary/institution/:searchString"  
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
        "required": ["id", "code", "name", "type", "address"]
      }
    }
  }
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Searchs for institutions whose name matches the search string.

### HTTP Request

`GET /dictionary/institution/:searchString`



### Authorization
 
N/A

## PasswordResetRequest - <em>Request to reset user's password</em>


```shell
curl -X POST "https://www.ctoregistry.com/api/v1/visitor/password/reset/request"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/PasswordResetRequest",
    "type": "object",
    "properties": {"email": {"type": "string"}},
    "required": ["email"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Request a password change for a user that forgot his password. A link will be sent to the email
        provided of the email address exists in the system

### HTTP Request

`POST /visitor/password/reset/request`



### Authorization
 
N/A

## PasswordResetToken - <em>Reset user's password with a token</em>


```shell
curl -X POST "https://www.ctoregistry.com/api/v1/visitor/password/reset"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/PasswordResetToken",
    "type": "object",
    "properties": {"password": {"type": "string"}, "token": {"type": "string"}},
    "required": ["password", "token"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Reset the password of a user using a token embedded in a link send to the email provided 
        during the reset password request

### HTTP Request

`POST /visitor/password/reset`



### Authorization
 
N/A

## UserCreationByVisitor - <em>Create a new user account</em>


```shell
curl -X POST "https://www.ctoregistry.com/api/v1/visitor/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/UserCreationByVisitor",
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
      },
      "password": {"type": "string", "minLength": 7, "description": "The user's password"}
    },
    "required": ["username", "firstName", "lastName", "title", "institution", "password"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Task used when a user creates an account. 
                      The account is setup so that the account will need to be reviewed by an administrator.

### HTTP Request

`POST /visitor/`



### Authorization
 
N/A

## UsernameCheckExists - <em>Verify if a username is already used</em>


```shell
curl "https://www.ctoregistry.com/api/v1/visitor/username/unique/:username"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserUniqueUsername",
    "type": "object",
    "properties": {"username": {"type": "string"}, "currentUsername": {"type": "string"}},
    "required": ["username"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Verify if a username is already used in the system. This is used during the registration process 
        to make sure that no two users have the same username

### HTTP Request

`GET /visitor/username/unique/:username`



### Authorization
 
N/A

## UsernameCheckExistsExceptUser - <em>Verify if a username is already used by a different user than the current user.</em>


```shell
curl "https://www.ctoregistry.com/api/v1/visitor/username/unique/:username/:currentUsername"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserUniqueUsername",
    "type": "object",
    "properties": {"username": {"type": "string"}, "currentUsername": {"type": "string"}},
    "required": ["username"]
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



<aside class="notice">This route is public and does not require authentication</aside>


Verify if a username is already used in the system. This is used during the registration process 
        to make sure that no two users have the same username

### HTTP Request

`GET /visitor/username/unique/:username/:currentUsername`



### Authorization
 
N/A