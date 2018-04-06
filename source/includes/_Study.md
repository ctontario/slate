
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



        Gets a list of all the studies in the system that the currently authenticated user can access. 
        Uses list pagination to limit the results.
        

### HTTP Request

`GET /study/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
institution | member | N/A|User has a collaborater role for the target study.
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
        "sponsor": {"type": ["string", "null"]},
        "sponsorId": {"type": "object"},
        "ctaita": {"type": "boolean"},
        "ctaitaTypes": {
          "type": "array",
          "items": {"type": "string", "enum": ["ctaFda", "ctaNhp", "itaMedDevices"]},
          "description": "Dictionary: Clinical Trial CTA/ITA Types"
        },
        "ohrp": {"type": "boolean"},
        "fda": {"type": "boolean"},
        "observational": {"type": "boolean"},
        "provincialStatus": {"type": "string"},
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
        "overallSampleSize": {"type": "string"},
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
              "cognitivelyImpared",
              "physicalDisabilities",
              "speechImpared",
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
                "email": {"type": "string|null"},
                "firstName": {"type": "string|null"},
                "lastName": {"type": "string|null"},
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
                "email": {"type": "string|null"},
                "firstName": {"type": "string|null"},
                "lastName": {"type": "string|null"},
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
                "email": {"type": "string|null"},
                "firstName": {"type": "string|null"},
                "lastName": {"type": "string|null"},
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
            "properties": {
              "institutionId": {
                "type": "object",
                "description": "The document Id of the institution.  This may be empty due to a data linking issue."
              },
              "name": {"type": "string"},
              "status": {"type": "string"},
              "startDate": {
                "type": "string",
                "description": "The textual start date for the centre"
              },
              "principalInvestigator": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": "string|null"},
                  "firstName": {"type": "string|null"},
                  "lastName": {"type": "string|null"},
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
                  "email": {"type": "string|null"},
                  "firstName": {"type": "string|null"},
                  "lastName": {"type": "string|null"},
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
                  "email": {"type": "string|null"},
                  "firstName": {"type": "string|null"},
                  "lastName": {"type": "string|null"},
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
system | admin | N/A|N/A
study | applicant | study|Study data is filtered to only contain centre applications for the target institution.
committee | member | study|N/A
institution | admin | study|Study data is filtered to only contain centre applications for the target institution.