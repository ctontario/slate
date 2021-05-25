
# Metrics


## FundingMasterReport - <em>Funding Master Report</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/funding/master"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/MetricsFundingMasterQuery",
    "type": "object",
    "properties": {
      "includeCommitteeIds": {
        "type": ["string", "array"],
        "description": "an array of committee IDs to include"
      },
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
  "id": "/MetricsFundingMasterResponse",
  "type": "object",
  "properties": {
    "totals": {
      "id": "/MetricsFundingMasterTotals",
      "type": "object",
      "properties": {
        "subTotal": {"type": "number"},
        "subTotalReceived": {"type": ["number", "string"]},
        "subTotalDifference": {"type": "number"},
        "hst": {"type": "number"},
        "hstReceived": {"type": "number"},
        "hstDifference": {"type": "number"},
        "rebPaymentAmountDue": {"type": ["number", "string"]},
        "rebPaymentAmountSent": {"type": ["number", "string"]},
        "rebPaymentAmountDifference": {"type": "number"},
        "sitePaymentAmountDue": {"type": ["number", "string"]},
        "sitePaymentAmountSent": {"type": ["number", "string"]},
        "sitePaymentAmountDifference": {"type": "number"}
      },
      "required": [
        "subTotal",
        "subTotalReceived",
        "subTotalDifference",
        "hst",
        "hstReceived",
        "hstDifference",
        "rebPaymentAmountDue",
        "rebPaymentAmountSent",
        "rebPaymentAmountDifference",
        "sitePaymentAmountDue",
        "sitePaymentAmountSent",
        "sitePaymentAmountDifference"
      ]
    },
    "data": {
      "type": "array",
      "items": {
        "id": "/MetricsFundingMasterData",
        "type": "object",
        "properties": {
          "projectIdNumber": {"type": "number"},
          "studyId": {"type": "object"},
          "studyFundingId": {"type": "object"},
          "committeeName": {"type": "string"},
          "committeeId": {"type": "object"},
          "applicationType": {"type": "string"},
          "centreName": {"type": "string"},
          "institutionId": {"type": ["null", "object"]},
          "invoiceDt": {"type": "date"},
          "invoiceLastSentDt": {"type": ["date", "null"]},
          "invoiceLastPaymentDt": {"type": ["date", "null"]},
          "invoiceNumber": {"type": "string"},
          "invoiceShortNumber": {"type": "integer"},
          "invoiceId": {"type": "object"},
          "subTotal": {"type": ["number", "string"]},
          "subTotalReceived": {"type": ["number", "string"]},
          "subTotalDifference": {"type": ["number", "string"]},
          "taxExempt": {"type": "string", "description": "boolean (true/false) changed to Y/N"},
          "hst": {"type": ["number", "string"]},
          "hstReceived": {"type": ["number", "string"]},
          "hstDifference": {"type": ["number", "string"]},
          "rebPaymentDt": {"type": ["date", "null"]},
          "rebPaymentAmountDue": {"type": ["number", "string"]},
          "rebPaymentAmountSent": {"type": ["number", "string"]},
          "rebPaymentAmountDifference": {"type": ["number", "string"]},
          "sitePaymentDt": {"type": ["date", "null"]},
          "sitePaymentAmountDue": {"type": ["number", "string"]},
          "sitePaymentAmountSent": {"type": ["number", "string"]},
          "sitePaymentAmountDifference": {"type": ["number", "string"]}
        },
        "required": [
          "projectIdNumber",
          "studyId",
          "studyFundingId",
          "committeeName",
          "applicationType",
          "centreName",
          "invoiceNumber",
          "invoiceShortNumber",
          "invoiceId",
          "invoiceDt",
          "subTotal",
          "subTotalReceived",
          "subTotalDifference",
          "taxExempt",
          "hst",
          "hstReceived",
          "hstDifference"
        ]
      }
    }
  },
  "required": ["totals", "data"]
}
```


Gets the report that includes totals for funding invoices and payments

### HTTP Request

`GET /metrics/funding/master`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A
system | support | N/A|N/A

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
    "id": "/MetricsCommitteeShareQuery",
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

## QuickStartSiteReport - <em>QuickSTART Site Report</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/quick-start/:quickStartId/sites/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  }
}
```


> Response Schema

```json
undefined
```


gets the Excel report for one QuickSTART site

### HTTP Request

`GET /metrics/quick-start/:quickStartId/sites/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A