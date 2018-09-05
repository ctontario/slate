
# System


## SystemDictionaries - <em>System Dictionaries</em>


```shell
curl "https://ctoregistry.com/api/v1/dictionary/system"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
undefined
```


Gets various smaller dictionaries used throughout the program to decode returned values

### HTTP Request

`GET /dictionary/system`



### Authorization
 
N/A

## SystemResponseInterfaces - <em>System Documentation</em>


```shell
curl "https://ctoregistry.com/api/v1/system/response-interfaces"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
undefined
```



<aside class="notice">This route is public and does not require authentication</aside>


Provides the system documentation of all available routes

### HTTP Request

`GET /system/response-interfaces`



### Authorization
 
N/A

## SystemTaskAuths - <em>System Task Auths</em>


```shell
curl "https://ctoregistry.com/api/v1/system/task-auths"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
undefined
```



<aside class="notice">This route is public and does not require authentication</aside>


Provides the system documentation of all available routes with their authorization requirements and request/response schemas.

### HTTP Request

`GET /system/task-auths`



### Authorization
 
N/A

## SystemVersion - <em>System Version</em>


```shell
curl "https://ctoregistry.com/api/v1/system/version"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/SystemVersionResponse",
  "type": "object",
  "properties": {
    "version": {
      "type": "object",
      "properties": {
        "apiVersion": {"type": "number"},
        "major": {"type": "number"},
        "minor": {"type": "number"},
        "dot": {"type": "number"},
        "codeName": {"type": "string"},
        "releaseDate": {"type": "date-time"}
      },
      "required": ["apiVersion", "major", "minor", "dot", "codeName", "releaseDate"]
    }
  }
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Provides the system version

### HTTP Request

`GET /system/version`



### Authorization
 
N/A