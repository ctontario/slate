
# Study


## StudyList - <em>Get Studies</em>


```shell
curl "https://ctoregistry.com/api/v1/study/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/StudyListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"},
      "csv": {"type": "boolean"},
      "institutionIds": {
        "type": ["string", "array"],
        "description": "an array of sponsor institution IDs"
      },
      "committeeIds": {"type": ["string", "array"], "description": "an array of committee IDs"}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/StudyListResponse",
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
        "id": "/Study",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "isInvestigatorInitiatedStudy": {"type": "boolean"},
          "sponsor": {
            "type": ["string", "null"],
            "description": "@Deprecated: Use studySponsor.name instead."
          },
          "studySponsor": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": ["string", "null"]}},
            "required": ["name"]
          },
          "ohrp": {"type": "boolean"},
          "fda": {"type": "boolean"},
          "observational": {"type": "boolean"},
          "provincialStatus": {
            "type": "string",
            "enum": [
              "Active",
              "Completed",
              "Expired",
              "None",
              "Not Approved",
              "Pending",
              "Suspended",
              "Terminated",
              "Withdrawn"
            ]
          },
          "expiryDt": {"type": ["date", "null"]},
          "shortTitle": {"type": "string"},
          "title": {"type": ["string", "null"]},
          "reviewerLink": {"type": "string"},
          "applicantLink": {"type": "string"},
          "reb": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
            "required": ["name"]
          },
          "projectIdNumber": {"type": "number"},
          "roles": {
            "type": "array",
            "items": {
              "type": "string",
              "description": "The users role on the study, only set when returned as part of the user studies route."
            }
          },
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "isInvestigatorInitiatedStudy",
          "studySponsor",
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
        Uses list pagination to limit the results.
        

### HTTP Request

`GET /study/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A
institution | member | N/A|User has a collaborator role for the target study.
institution | admin | N/A|Study has a centre application for the target institution of the privilege.
committee | member | N/A|Study REB is set to the target of the privilege.

## StudyProfile - <em>Get Study</em>


```shell
curl "https://ctoregistry.com/api/v1/study/:studyId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyParams",
    "type": "object",
    "properties": {"studyId": {"type": "string"}},
    "required": ["studyId"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyProfileResponse",
  "type": "object",
  "properties": {
    "study": {
      "id": "/StudyFull",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "isInvestigatorInitiatedStudy": {"type": "boolean"},
        "sponsor": {
          "type": ["string", "null"],
          "description": "@Deprecated: Use studySponsor.name instead."
        },
        "studySponsor": {
          "type": "object",
          "properties": {
            "id": {"type": "object"},
            "name": {"type": ["string", "null"]},
            "contact": {
              "properties": {
                "userId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]}
              },
              "required": ["firstName", "lastName", "email"]
            }
          },
          "required": ["name"]
        },
        "studyCro": {
          "type": "object",
          "properties": {
            "id": {"type": "object"},
            "name": {"type": ["string", "null"]},
            "contact": {
              "properties": {
                "userId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]}
              },
              "required": ["firstName", "lastName", "email"]
            }
          },
          "required": ["name", "contact"]
        },
        "ctaita": {"type": "boolean"},
        "ctaitaTypes": {
          "type": "array",
          "items": {"type": "string", "enum": ["ctaFda", "ctaNhp", "itaMedDevices"]},
          "description": "Dictionary: Clinical Trial CTA/ITA Types"
        },
        "ohrp": {"type": "boolean"},
        "fda": {"type": "boolean"},
        "observational": {"type": "boolean"},
        "provincialStatus": {
          "type": "string",
          "enum": [
            "Active",
            "Completed",
            "Expired",
            "None",
            "Not Approved",
            "Pending",
            "Suspended",
            "Terminated",
            "Withdrawn"
          ]
        },
        "expiryDt": {"type": ["date", "null"]},
        "shortTitle": {"type": "string"},
        "title": {"type": ["string", "null"]},
        "reviewerLink": {"type": "string"},
        "applicantLink": {"type": "string"},
        "reb": {
          "type": "object",
          "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
          "required": ["name"]
        },
        "projectIdNumber": {"type": "number"},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"},
        "initialApprovalDt": {"type": ["date"]},
        "initialReviewType": {
          "type": ["string"],
          "enum": ["Full Board Review", "Delegated Review", "Admin Review"]
        },
        "summary": {"type": ["string", "null"]},
        "interventions": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["drugs", "health", "devices", "specimen", "radiation", "surveys", "other"]
          },
          "description": "Dictionary: Clinical Trial Interventions"
        },
        "funding": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "charity",
              "government",
              "governmentFundingAgency",
              "grantingAgency",
              "industry",
              "internal",
              "none",
              "other",
              "usFederalFunds",
              "triCouncil"
            ]
          },
          "description": "Dictionary: Clinical Trial Funding Types"
        },
        "fundingOther": {"type": "string"},
        "mta": {"type": "boolean"},
        "overallSampleSize": {"type": ["string", "null"]},
        "populations": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "patients",
              "healthyVolunteers",
              "students",
              "staff",
              "mentalHealth",
              "institutionalized",
              "prisoners",
              "poverty",
              "educationalDisadvantaged",
              "illiterate",
              "children",
              "emergency",
              "lackConsentCapacity",
              "cognitivelyImpaired",
              "physicalDisabilities",
              "speechImpaired",
              "lackConsentTemporary",
              "pregnant",
              "elderly",
              "palliativeCare",
              "longTermCare",
              "minorities",
              "other"
            ]
          },
          "description": "Dictionary: Clinical Trial Populations"
        },
        "populationsOther": {"type": "string"},
        "phase": {"type": "string"},
        "phaseOther": {"type": "string"},
        "dsmb": {"type": "boolean"},
        "ctaApproved": {"type": "boolean"},
        "ctaInvestigational": {"type": "boolean"},
        "provincialApplication": {
          "type": "object",
          "properties": {
            "studyContact": {
              "id": "/StudyUser",
              "properties": {
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]},
                "organization": {"type": ["string", "null"]},
                "institutionId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "user": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "object"},
                    "firstName": {"type": "string"},
                    "lastName": {"type": "string"},
                    "title": {
                      "type": "string",
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
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]},
                "organization": {"type": ["string", "null"]},
                "institutionId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "user": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "object"},
                    "firstName": {"type": "string"},
                    "lastName": {"type": "string"},
                    "title": {
                      "type": "string",
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
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]},
                "organization": {"type": ["string", "null"]},
                "institutionId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "user": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "object"},
                    "firstName": {"type": "string"},
                    "lastName": {"type": "string"},
                    "title": {
                      "type": "string",
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
            "id": "/CentreApplication",
            "properties": {
              "institutionId": {
                "type": "object",
                "description": "The document Id of the institution.  This may be empty due to a data linking issue."
              },
              "name": {"type": "string"},
              "status": {
                "type": "string",
                "enum": [
                  "Active",
                  "Completed",
                  "Expired",
                  "None",
                  "Not Approved",
                  "Pending",
                  "Suspended",
                  "Terminated",
                  "Withdrawn"
                ]
              },
              "startDate": {
                "type": "string",
                "description": "The textual start date for the centre"
              },
              "principalInvestigator": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]},
                  "organization": {"type": ["string", "null"]},
                  "institutionId": {"type": ["object", "null"]},
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object"},
                      "firstName": {"type": "string"},
                      "lastName": {"type": "string"},
                      "title": {
                        "type": "string",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName", "title"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "coInvestigator": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]},
                  "organization": {"type": ["string", "null"]},
                  "institutionId": {"type": ["object", "null"]},
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object"},
                      "firstName": {"type": "string"},
                      "lastName": {"type": "string"},
                      "title": {
                        "type": "string",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName", "title"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "studyContact": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]},
                  "organization": {"type": ["string", "null"]},
                  "institutionId": {"type": ["object", "null"]},
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object"},
                      "firstName": {"type": "string"},
                      "lastName": {"type": "string"},
                      "title": {
                        "type": "string",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName", "title"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "centreSampleSize": {
                "type": "string",
                "description": "Textual description of the planned centre sample size"
              },
              "initialApprovalDt": {"type": "date"},
              "initialReviewType": {
                "type": "string",
                "enum": ["Full Board Review", "Delegated Review", "Admin Review"]
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
        "updateDt",
        "summary",
        "interventions",
        "funding",
        "mta",
        "overallSampleSize",
        "populations",
        "dsmb",
        "ctaApproved",
        "ctaInvestigational"
      ]
    }
  }
}
```



        Gets the data record of one study.  Some sections of the data will only be available depending on the authenticated users privileges and participation.
        Refer to the restrictions listed for each authorization privilege.
        

### HTTP Request

`GET /study/:studyId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A
study | applicant | study|Study data is filtered to only contain centre applications for the target institution.
committee | member | study|N/A
institution | admin | study|Study data is filtered to only contain centre applications for the target institution.