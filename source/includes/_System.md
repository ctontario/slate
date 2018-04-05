
# System


## SystemDocumentation - <em>System Documentation</em>


```shell
curl "https://ctoregistry.com/api/v1/system/documentation"  
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

`GET /system/documentation`



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