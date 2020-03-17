
# Metrics


## MetricsCommitteeShare - <em>Committee Share Metrics</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/committee/share"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/MetricsCommitteeShare",
    "type": "object",
    "properties": {
      "excludeCommitteeIds": {
        "type": ["string", "array"],
        "description": "an array of committee IDs to exclude"
      },
      "csv": {
        "type": "string",
        "description": "Return the report as CSV content instead of the default JSON"
      }
    }
  }
}
```


> Response Schema

```json
{
  "id": "/MetricsCommitteeShareResponse",
  "type": "object",
  "properties": {
    "totals": {
      "id": "/MetricsCommitteeShareTotals",
      "type": "object",
      "properties": {
        "studyCount": {"type": "integer"},
        "studyCountFunded": {"type": "integer"},
        "centreCount": {"type": "integer"},
        "centreCountFunded": {"type": "integer"}
      },
      "required": ["studyCount", "studyCountFunded", "centreCount", "centreCountFunded"]
    },
    "data": {
      "type": "array",
      "items": {
        "id": "/MetricsCommitteeShareData",
        "type": "object",
        "properties": {
          "committeeId": {"type": "object"},
          "committeeName": {"type": "string"},
          "studyCount": {"type": "integer"},
          "studyCountFunded": {"type": "integer"},
          "centreCount": {"type": "integer"},
          "centreCountFunded": {"type": "integer"},
          "shareOfStudies": {"type": "string"},
          "shareOfCentres": {"type": "string"},
          "joinedVsReviewedPercentDiff": {"type": "string"}
        },
        "required": [
          "committeeId",
          "committeeName",
          "studyCount",
          "studyCountFunded",
          "centreCount",
          "centreCountFunded",
          "shareOfStudies",
          "shareOfCentres",
          "joinedVsReviewedPercentDiff"
        ]
      }
    }
  },
  "required": ["totals", "data"]
}
```


Gets the share metrics report used to determine Committee assigned and for overall review of studies reviewed by board.

### HTTP Request

`GET /metrics/committee/share`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A