
# System


## SystemDocumentation - <em>System Documentation</em>


```shell
curl "https://cto.local:9000/api/v1/system/documentation"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
undefined
```



<aside class="notice">This route is public and does not require authentication</aside>


Provides the system documentation of all available routes

### HTTP Request

`GET /system/documentation`



### Authorization
 
N/A

## SystemVersion - <em>System Version</em>


```shell
curl "https://cto.local:9000/api/v1/system/version"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/SystemVersionResponse",
  "type": "object",
  "properties": {
    "version": {
      "type": "object",
      "properties": {
        "apiVersion": {"type": "number", "description": ""},
        "major": {"type": "number", "description": ""},
        "minor": {"type": "number", "description": ""},
        "dot": {"type": "number", "description": ""},
        "codeName": {"type": "string", "description": ""},
        "releaseDate": {"type": "date-time", "description": ""}
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