
# System


## SystemDictionaries - <em>System Dictionaries</em>


```shell
curl "https://ctoregistry.com/api/v1/dictionary/system"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/SystemDictionary",
  "type": "object",
  "properties": {
    "study": {
      "id": "StudyDictionaries",
      "properties": {
        "ctaitaTypes": {
          "id": "StudyCtaitaTypeDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {
                "code": {"type": "string"},
                "label": {"type": "string"},
                "question": {"type": "string"}
              },
              "required": ["code", "label", "question"]
            }
          }
        },
        "interventions": {
          "id": "StudyInterventionDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {
                "code": {"type": "string"},
                "label": {"type": "string"},
                "question": {"type": "string"}
              },
              "required": ["code", "label", "question"]
            }
          }
        },
        "funding": {
          "id": "StudyFundingDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {
                "code": {"type": "string"},
                "label": {"type": "string"},
                "question": {"type": "string"}
              },
              "required": ["code", "label", "question"]
            }
          }
        },
        "populations": {
          "id": "StudyPopulationDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {
                "code": {"type": "string"},
                "label": {"type": "string"},
                "question": {"type": "string"}
              },
              "required": ["code", "label", "question"]
            }
          }
        }
      },
      "required": ["ctaitaTypes", "interventions", "funding", "populations"]
    },
    "contact": {
      "id": "ContactDictionaries",
      "properties": {
        "title": {"type": "array", "items": {"type": "string"}},
        "phoneType": {"type": "array", "items": {"type": "string"}}
      },
      "required": ["title", "phoneType"]
    },
    "user": {
      "id": "UserDictionaries",
      "properties": {
        "accountStatus": {"type": "array", "items": {"type": "string"}},
        "dataStatus": {"type": "array", "items": {"type": "string"}},
        "privileges": {
          "id": "UserPrivilegeDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {
                "code": {"type": "string"},
                "label": {"type": "string"},
                "isAddable": {"type": "boolean"},
                "roles": {
                  "type": "array",
                  "items": {
                    "properties": {
                      "code": {"type": "string"},
                      "label": {"type": "string"},
                      "isAddable": {"type": "boolean"},
                      "targetRequired": {"type": "boolean"}
                    },
                    "required": ["code", "label"]
                  }
                }
              },
              "required": ["code", "label", "isAddable", "roles"]
            }
          }
        }
      },
      "required": ["accountStatus", "dataStatus", "privileges"]
    },
    "committee": {
      "id": "CommitteeDictionaries",
      "properties": {
        "type": {
          "id": "CommitteeTypeDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
              "required": ["code", "label"]
            }
          }
        },
        "member": {
          "properties": {
            "role": {
              "id": "CommitteeMemberRoleDictionary",
              "patternProperties": {
                "^[a-zA-Z_$][\\w$]*$": {
                  "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
                  "required": ["code", "label"]
                }
              }
            },
            "status": {
              "id": "CommitteeMemberStatusDictionary",
              "patternProperties": {
                "^[a-zA-Z_$][\\w$]*$": {
                  "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
                  "required": ["code", "label"]
                }
              }
            }
          },
          "required": ["role", "status"]
        }
      },
      "required": ["type", "member"]
    },
    "quickStart": {
      "id": "QuickStartDictionaries",
      "properties": {
        "status": {"type": "array", "items": {"type": "string"}},
        "creationProgress": {
          "type": "array",
          "items": {"type": "string", "enum": ["study", "studyDocuments", "contract", "budget"]}
        },
        "site": {
          "properties": {
            "status": {"type": "array", "items": {"type": "string"}},
            "comments": {
              "id": "QuickStartSiteCommentDictionary",
              "patternProperties": {
                "^[a-zA-Z_$][\\w$]*$": {
                  "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
                  "required": ["code", "label"]
                }
              }
            },
            "rebEvents": {
              "id": "QuickStartSiteRebEventsDictionary",
              "patternProperties": {
                "^[a-zA-Z_$][\\w$]*$": {
                  "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
                  "required": ["code", "label"]
                }
              }
            },
            "approveAfterEvents": {
              "id": "QuickStartSiteApproveAfterEvents",
              "patternProperties": {
                "^[a-zA-Z_$][\\w$]*$": {
                  "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
                  "required": ["code", "label"]
                }
              }
            },
            "timers": {
              "id": "QuickStartSiteTimers",
              "type": "object",
              "properties": {
                "daysToApprove": {"type": "number"},
                "contract": {
                  "type": "object",
                  "properties": {
                    "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
                    "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
                  },
                  "required": ["siteDaysToAction", "sponsorDaysToRespond"]
                },
                "budget": {
                  "type": "object",
                  "properties": {
                    "siteDaysToAction": {"type": "array", "items": {"type": "number"}},
                    "sponsorDaysToRespond": {"type": "array", "items": {"type": "number"}}
                  },
                  "required": ["siteDaysToAction", "sponsorDaysToRespond"]
                }
              },
              "required": ["daysToApprove", "contract", "budget"]
            }
          },
          "required": ["status", "comments", "rebEvents", "approveAfterEvents", "timers"]
        },
        "approvalTypes": {
          "id": "QuickStartApprovalTypeDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
              "required": ["code", "label"]
            }
          }
        },
        "documentType": {"type": "array", "items": {"type": "string"}}
      },
      "required": ["status", "creationProgress", "site", "approvalTypes", "documentType"]
    },
    "document": {
      "id": "DocumentDictionaries",
      "properties": {
        "mimeTypes": {
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "patternProperties": {"^[a-zA-Z_$][\\w$]*$": {"type": "string"}}
            }
          }
        },
        "allowedMimeTypes": {
          "properties": {
            "quickStart": {"type": "array", "items": {"type": "string"}},
            "institution": {"type": "array", "items": {"type": "string"}},
            "fundingHstExemption": {"type": "array", "items": {"type": "string"}}
          },
          "required": ["quickStart", "institution", "fundingHstExemption"]
        },
        "maxFileSize": {"type": "number"}
      },
      "required": ["mimeTypes", "allowedMimeTypes", "maxFileSize"]
    },
    "email": {
      "id": "EmailDictionaries",
      "properties": {
        "template": {
          "id": "EmailTemplateDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
              "required": ["code", "label"]
            }
          }
        },
        "event": {
          "id": "EmailEventDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
              "required": ["code", "label"]
            }
          }
        }
      },
      "required": ["template", "event"]
    },
    "studyFunding": {
      "id": "StudyFundingDictionaries",
      "properties": {
        "paymentTypes": {
          "id": "StudyFundingPaymentTypeDictionary",
          "patternProperties": {
            "^[a-zA-Z_$][\\w$]*$": {
              "properties": {"code": {"type": "string"}, "label": {"type": "string"}},
              "required": ["code", "label"]
            }
          }
        }
      },
      "required": ["paymentTypes"]
    }
  },
  "required": [
    "study",
    "contact",
    "user",
    "committee",
    "quickStart",
    "document",
    "email",
    "studyFunding"
  ]
}
```


Gets various smaller dictionaries used throughout the program to decode returned values

### HTTP Request

`GET /dictionary/system`



### Authorization
 
N/A

## SystemEmailEventNotification - <em>System Email Event Notification</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/system/email/event-notification"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/SystemEmailEventNotificationQuery",
    "type": "object",
    "properties": {"key": {"type": "string"}},
    "required": ["key"]
  },
  "body": {
    "id": "/SystemEmailEventNotificationBody",
    "type": "array",
    "items": {
      "type": "object",
      "properties": {
        "email": {"type": "string"},
        "timestamp": {"type": "number"},
        "event": {
          "type": "string",
          "enum": [
            "processed",
            "dropped",
            "delivered",
            "deferred",
            "bounce",
            "open",
            "click",
            "spamreport",
            "unsubscribe",
            "group_unsubscribe",
            "group_resubscribe"
          ]
        },
        "smtp-id": {"type": "string"},
        "useragent": {"type": "string"},
        "IP": {"type": "string"},
        "sg_event_id": {"type": "string"},
        "sg_message_id": {"type": "string"},
        "reason": {"type": "string"},
        "status": {"type": "string"},
        "response": {"type": "string"},
        "tls": {"type": "number"},
        "url": {"type": "string"},
        "url_offset": {
          "type": "object",
          "properties": {"index": {"type": "number"}, "type": {"type": "string"}},
          "required": ["index", "type"]
        },
        "attempt": {"type": "string"},
        "category": {"type": ["string", "array"], "items": {"type": "string"}},
        "type": {"type": "string"},
        "asm_group_id": {"type": "number"}
      },
      "required": ["email", "timestamp", "event", "sg_event_id", "sg_message_id"]
    }
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
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Handles inbound notifications from the email API to parse delivery results. Requires a query parameters of 'key' to match the key in the internal config

### HTTP Request

`POST /system/email/event-notification`



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
    },
    "system": {
      "type": "object",
      "properties": {
        "environment": {"type": "string"},
        "frontendUrl": {"type": "string"},
        "database": {"type": "string"},
        "confidentiality": {"type": "string"},
        "email": {"type": "boolean"}
      },
      "required": ["environment", "frontendUrl", "database", "confidentiality", "email"]
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