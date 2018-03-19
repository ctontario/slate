
# Study


## StudyList - <em>Get Studies</em>


```shell
curl "https://cto.local:9000/api/v1/study/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/StudyListResponse",
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



        Gets a list of all the studies in the system that the currently authenticated user can access.  
        
        - <strong>system:admin</strong> all studies
        
        - <strong>institution:member</strong> all the studies the user is participating on
        
        - <strong>institution:admin</strong> all studies that the institution is participating on
        
        - <strong>committee:member</strong> all studies that the committee has been assigned as the REB
        


### HTTP Request

`GET /study/`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
institution | member | N/A
institution | admin | N/A
committee | member | N/A

## StudyProfile - <em>Get Study</em>


```shell
curl "https://cto.local:9000/api/v1/study/:studyId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Body Schema

```json
{
  "id": "/StudyProfileResponse",
  "type": "object",
  "properties": {
    "study": {
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
```


Get the data record of one study.  Some sections of the data will only be available 
        depending on the authenticated users privileges and participation.
        
        - <strong>system:admin</strong>: Full Data
        
        - <strong>committee:member</strong>: Full Data
        
        - <strong>institution:admin</strong>: The overall study data, and the data for the participants own site.
        
        - <strong>participant:study</strong> The overall study data, and the data for the participants own site.    
            
        

### HTTP Request

`GET /study/:studyId`



### Authorization
 
    
 Scope      | Role       | Auth Source
------------|------------|-------------
system | admin | N/A
study | participant | study
committee | member | study
institution | admin | study