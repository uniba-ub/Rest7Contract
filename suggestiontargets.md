# Suggestion Targets Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/integration/suggestiontargets**   

It returns the list of targets with their suggestion count. Only targets that have at least one suggestion are returned. This endpoint is reserved to administrators

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

Status codes:
* 200 Ok - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in as an administrator


### single entry
**GET api/integration/suggestiontargets/<:target-id>**

It returns the data from one target. This endpoint is accessible to the profile owner and to the administrators

sample for a suggestion /api/integration/suggestiontargets/nhy567-9d6d-ty67-b905-fef0f8cae26
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

Attributes
* the *display* attribute is the preferred name of the linked Person
* the *totals* attribute is a map, the key identifies the source of the suggestion, the value is the number of related suggestions. At least one must be greater than 0

Exposed links:
* target: link to the items that represent the person to whom the suggestions are proposed
* suggestions: link to the suggestions entries

Status codes:
* 200 Ok - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions
* 404 Not found - if there are no suggestions for the requested profile (when 403 doesn't apply) 
