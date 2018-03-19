
# Security


## Authentication - <em>Authentication</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/security/authentication"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/Authentication",
  "properties": {
    "username": {"type": "string", "required": true, "description": ""},
    "password": {"type": "string", "required": true, "description": ""}
  }
}
```


> Response Body Schema

```json
{
  "id": "/AuthenticationResponse",
  "type": "object",
  "properties": {
    "id": {"type": "object", "description": ""},
    "token": {"type": "string", "description": ""},
    "privilege": {"type": "string", "description": ""}
  },
  "required": ["id", "token", "privilege"]
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Tests a users credentials, and if successful grants access to the system

### HTTP Request

`POST /security/authentication`



### Authorization
 
N/A

## CheckToken - <em>Check Token</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/security/token"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Body Schema

```json
{
  "id": "/CheckToken",
  "properties": {
    "token": {"type": "string", "required": true, "description": ""},
    "service": {"type": "string", "required": true, "description": ""}
  }
}
```


> Response Body Schema

```json
{
  "id": "/CheckTokenResponse",
  "type": "object",
  "properties": {
    "tokenStatus": {"type": "string", "description": "", "enum": ["invalid", "valid"]}
  },
  "required": ["tokenStatus"]
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Validates a token

### HTTP Request

`POST /security/token`



### Authorization
 
N/A

## PrivilegeToken - <em>Get Privilege Token</em>


```shell
curl "https://cto.local:9000/api/v1/security/privilegeToken"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/PrivilegeTokenResponse",
  "type": "object",
  "properties": {"privilege": {"type": "string", "description": ""}},
  "required": ["privilege"]
}
```


Gets the users privilege token

### HTTP Request

`GET /security/privilegeToken`



### Authorization
 
N/A