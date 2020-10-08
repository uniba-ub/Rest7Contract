# Suggestiontargetss Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/integration/suggestiontargets**   

It returns the list of targets with their suggestion count.

Example:
```json
{
  "_embedded": {
    "suggestiontargets": [
      {
        "id": "gf3d657-9d6d-4a87-b905-fef0f8cae26",
        "display": "Bollini, Andrea",
        "totals" : {
          "reciter": 31,
          "scopus": 12
        },	
        "type": "suggestiontarget",
        "_links": {
          "target": {
            "href": "https://dspace7.4science.cloud/server/api/core/items/gf3d657-9d6d-4a87-b905-fef0f8cae26"
          },
          "suggestions": {
            "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/search/findByPerson?uuid=gf3d657-9d6d-4a87-b905-fef0f8cae26c"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/suggestiontargets/gf3d657-9d6d-4a87-b905-fef0f8cae26"
          }
        }
      },
      {
        "id": "nhy567-9d6d-ty67-b905-fef0f8cae26",
        "display": "Digilio, Giuseppe",
        "totals" : {
          "reciter": 12,
          "scopus": 5
        },	
        "type": "suggestiontarget",
        "_links": {
          "target": {
            "href": "https://dspace7.4science.cloud/server/api/core/items/nhy567-9d6d-ty67-b905-fef0f8cae26"
          },
          "suggestions": {
            "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/search/findByPerson?uuid=nhy567-9d6d-ty67-b905-fef0f8cae26"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/suggestiontargets/nhy567-9d6d-ty67-b905-fef0f8cae26"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://dspace7.4science.cloud/server/api/integration/suggestiontargets"
    }
  },
  "page": {
    "size": 20,
    "totalElements": 2,
    "totalPages": 1,
    "number": 0
  }
}
```

### single entry
**GET api/integration/suggestiontargets/<:target-id>**

It returns the data from one target

sample for a suggestion /api/integration/suggestiontargets/24694772
```json
{
    "id": "nhy567-9d6d-ty67-b905-fef0f8cae26",
    "display": "Digilio, Giuseppe",
    "totals" : {
      "reciter": 12,
      "scopus": 5
    },	
    "type": "suggestiontarget",
    "_links": {
      "target": {
        "href": "https://dspace7.4science.cloud/server/api/core/items/nhy567-9d6d-ty67-b905-fef0f8cae26"
      },
      "suggestions": {
        "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/search/findByPerson?uuid=nhy567-9d6d-ty67-b905-fef0f8cae26"
      },
      "self": {
        "href": "https://dspace7.4science.cloud/server/api/integration/suggestiontargets/nhy567-9d6d-ty67-b905-fef0f8cae26"
      }
    }
}
```
