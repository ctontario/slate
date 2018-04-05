
# Security


## Authentication - <em>Authentication</em>


```shell
curl -X POST "https://www.ctoregistry.com/api/v1/security/authentication"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/Authentication",
    "type": "object",
    "properties": {"username": {"type": "string"}, "password": {"type": "string"}},
    "required": ["username", "password"]
  }
}
```


> Response Schema

```json
{
  "id": "/AuthenticationResponse",
  "type": "object",
  "properties": {
    "id": {"type": "object"},
    "token": {"type": "string"},
    "privilege": {"type": "string"}
  },
  "required": ["id", "token", "privilege"]
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Tests a users credentials, and if successful returns a token to access the system

### HTTP Request

`POST /security/authentication`



### Authorization
 
N/A

## CheckToken - <em>Check Token</em>


```shell
curl -X POST "https://www.ctoregistry.com/api/v1/security/token"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/CheckToken",
    "type": "object",
    "properties": {"token": {"type": "string"}, "service": {"type": "string"}},
    "required": ["token", "service"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckTokenResponse",
  "type": "object",
  "properties": {"tokenStatus": {"type": "string", "enum": ["invalid", "valid"]}},
  "required": ["tokenStatus"]
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Validates an authentication token

### HTTP Request

`POST /security/token`



### Authorization
 
N/A

## PrivilegeToken - <em>Get Privilege Token</em>


```shell
curl "https://www.ctoregistry.com/api/v1/security/privilegeToken"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/PrivilegeTokenResponse",
  "type": "object",
  "properties": {"privilege": {"type": "string"}},
  "required": ["privilege"]
}
```


Gets the currently authenticated users privilege token

### HTTP Request

`GET /security/privilegeToken`



### Authorization
 
N/A