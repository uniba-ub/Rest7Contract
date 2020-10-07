# Reciter sources Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/integration/recitersources**   

Provide access to the configured reciter sources. It returns the list of reciter sources.

Example:
```json
{
  "_embedded": {
    "recitersources": [
      {
        "id": "pubmed",
        "name": "pubmed",
        "hierarchical": false,
        "type": "recitersources",
        "_links": {
          "entries": {
            "href": "https://dspace7.4science.cloud/server/api/integration/recitersources/scopus/entries"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/recitersources/scopus"
          }
        }
      },
      {
        "id": "scopus",
        "name": "scopus",
        "hierarchical": false,
        "type": "recitersources",
        "_links": {
          "entries": {
            "href": "https://dspace7.4science.cloud/server/api/integration/recitersources/scopus/entries"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/recitersources/scopus"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://dspace7.4science.cloud/server/api/integration/recitersources"
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
## Linked entities
### external source entries
**/api/integration/recitersources/<:source-name>/entries**

It returns the list of suggestions and corresponding evidence for individuals or groups of individuals

The supported parameters are (having uuid or group parameter is mandatory):
* page, size [see pagination](README.md#Pagination)
* uuid: the uuid associated with your target person;
* group: the group uuid associated with your target group;

Return codes:
* 200 OK - if the operation succeed
* 400 Bad Request - if the uuid parameter is missing or invalid

sample for an reciter source /server/api/integration/recitersources/scopus/entries?uuid=gf3d657-9d6d-4a87-b905-fef0f8cae26c&size=2 
```json
{
  "_embedded": {
    "reciterSourceEntries": [
      {
        "id": "0000-0003-3681-2038",
        "display": "publication one",
        "value": "publication one",
        "metadata": {
            "dc.identifier.uri": [
              {
                "value": "https://publication/0000-0003-3681-2038",
                "language": null,
                "authority": null,
                "confidence": -1,
                "place": -1
              }
            ],
            "dc.title" : [
              {
                "value" : "publication one",
                "language" : null,
                "authority" : null,
                "confidence" : -1
              }
            ],
            "dc.date.issued" : [
              {
                "value" : "2010-11-03",
                "language" : null,
                "authority" : null,
                "confidence" : -1
              }
            ]
        },
        "type": "reciterSourcesEntry",
        "_links": {
          "parent": {
            "href": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/scopus"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/scopus/entryValues/0000-0003-3681-2038"
          }
        }
      },
      {
        "id": "0000-0452-3681-2038",
        "display": "publication two",
        "value": "publication two",
        "metadata": {
            "dc.identifier.uri": [
              {
                "value": "https://publication/0000-0452-3681-2038",
                "language": null,
                "authority": null,
                "confidence": -1,
                "place": -1
              }
            ],
            "dc.title" : [
              {
                "value" : "publication two",
                "language" : null,
                "authority" : null,
                "confidence" : -1
              }
            ],
            "dc.date.issued" : [
              {
                "value" : "2010-11-03",
                "language" : null,
                "authority" : null,
                "confidence" : -1
              }
            ]
        },
        "type": "reciterSourcesEntry",
        "_links": {
          "parent": {
            "href": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/scopus"
          },          
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/scopus/entryValues/0000-0003-3681-2038"
          }
        }
      }
    ]
  }
}
```

### single entry
**GET /api/integration/recitersources/<:source-name>/entryValues/<:entry-id>**

It returns the data from one entry in a reciter source

sample for a reciter source /api/integration/recitersources/scopus/entryValues/0000-0002-4271-0436 
```json
{
  "id": "0000-0452-3681-2038",
  "display": "publication two",
  "value": "publication two",
  "metadata": {
    "dc.identifier.uri": [
      {
        "value": "https://publication/0000-0452-3681-2038",
        "language": null,
        "authority": null,
        "confidence": -1,
        "place": -1
      }
    ],
    "dc.title" : [
      {
        "value" : "publication two",
        "language" : null,
        "authority" : null,
        "confidence" : -1
      }
    ],
    "dc.date.issued" : [
      {
        "value" : "2010-11-03",
        "language" : null,
        "authority" : null,
        "confidence" : -1
      }
    ]
  },
  "_links": {
    "parent": {
      "href": "https://dspace7.4science.cloud/server/api/integration/recitersources/scopus"
    },    
    "self": {
      "href": "https://dspace7.4science.cloud/server/api/integration/recitersources/scopus/entryValues/0000-0452-3681-2038"
    }
  }
}
```

## Import suggestion

See the [items endpoint](items.md#creating-an-archived-item-from-a-reciter-source) for details on how to import a suggestion

## Discard suggestion
**DELETE /api/integration/recitersources/<:source-name>/entryValues/<:entry-id>**

This discard the given suggestion.

Status codes:
* 201 Created - if the operation succeed
* 404 Not found - if the entry doesn't exist
