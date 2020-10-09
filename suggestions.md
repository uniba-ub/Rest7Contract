# Suggestions Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/integration/suggestions**   

It returns the list of suggestions.

Example:
```json
{
  "_embedded": {
    "suggestions": [
      {
        "id": "24694772",
        "display": "publication one",
        "source": "reciter",
        "external-source-uri": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/pubmed/entryValues/24694772",
        "evidences": {
          "acceptedRejectedEvidence": {
            "score": "2.7",
            "notes": "notes"
          },
          "authorNameEvidence": {
            "score": "0",
            "notes": "notes"
          },
          "journalCategoryEvidence": {
            "score": "6",
            "notes": "notes"
          },
          "affiliationEvidence": {
            "score": "xxx",
            "notes": "notes"
          },
          "relationshipEvidence": {
            "score": "9",
            "notes": "notes"
          },
          "educationYearEvidence": {
            "score": "3.6",
            "notes": "notes"
          },
          "personTypeEvidence": {
            "score": "4",
            "notes": "notes"
          },
          "articleCountEvidence": {
            "score": "6.7",
            "notes": "notes"
          },
          "averageClusteringEvidence": {
            "score": "7",
            "notes": "notes"
          }
        },
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
        "type": "suggestion",
        "_links": {
          "target": {
            "href": "https://dspace7.4science.cloud/server/api/core/items/gf3d657-9d6d-4a87-b905-fef0f8cae26"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/24694772"
          }
        }
      },
      {
        "id": "29339930",
        "display": "publication one",
        "source": "reciter",
        "external-source-uri": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/pubmed/entryValues/29339930",
        "evidences": {
          "acceptedRejectedEvidence": {
            "score": "2.7",
            "notes": "notes"
          },
          "authorNameEvidence": {
            "score": "0",
            "notes": "notes"
          },
          "journalCategoryEvidence": {
            "score": "6",
            "notes": "notes"
          },
          "affiliationEvidence": {
            "score": "xxx",
            "notes": "notes"
          },
          "relationshipEvidence": {
            "score": "9",
            "notes": "notes"
          },
          "educationYearEvidence": {
            "score": "3.6",
            "notes": "notes"
          },
          "personTypeEvidence": {
            "score": "4",
            "notes": "notes"
          },
          "articleCountEvidence": {
            "score": "6.7",
            "notes": "notes"
          },
          "averageClusteringEvidence": {
            "score": "7",
            "notes": "notes"
          }
        },
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
        "type": "suggestion",
        "_links": {
          "target": {
            "href": "https://dspace7.4science.cloud/server/api/core/items/gf3d657-9d6d-4a87-b905-fef0f8cae26"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/29339930"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://dspace7.4science.cloud/server/api/integration/suggestions"
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
## Search methods
### Get suggestions by given person
**/api/integration/suggestions/search/findByPerson?uuid=:person-uuid[&size=10&page=0]**

It returns the list of suggestions and corresponding evidence for individuals

The supported parameters are :
* page, size [see pagination](README.md#Pagination)
* uuid: mandatory, the uuid associated with your target person;

Return codes:
* 200 OK - if the operation succeed
* 400 Bad Request - if the uuid parameter is missing or invalid

sample for a search /server/api/integration/suggestions/search/findByPerson?uuid=gf3d657-9d6d-4a87-b905-fef0f8cae26c
```json
{
  "_embedded": {
    "reciterSourceEntries": [
{
        "id": "24694772",
        "display": "publication one",
        "source": "reciter",
        "external-source-uri": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/pubmed/entryValues/24694772",
        "evidences": {
          "acceptedRejectedEvidence": {
            "score": "2.7",
            "notes": "notes"
          },
          "authorNameEvidence": {
            "score": "0",
            "notes": "notes"
          },
          "journalCategoryEvidence": {
            "score": "6",
            "notes": "notes"
          },
          "affiliationEvidence": {
            "score": "xxx",
            "notes": "notes"
          },
          "relationshipEvidence": {
            "score": "9",
            "notes": "notes"
          },
          "educationYearEvidence": {
            "score": "3.6",
            "notes": "notes"
          },
          "personTypeEvidence": {
            "score": "4",
            "notes": "notes"
          },
          "articleCountEvidence": {
            "score": "6.7",
            "notes": "notes"
          },
          "averageClusteringEvidence": {
            "score": "7",
            "notes": "notes"
          }
        },
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
        "type": "suggestion",
        "_links": {
          "target": {
            "href": "https://dspace7.4science.cloud/server/api/core/items/gf3d657-9d6d-4a87-b905-fef0f8cae26"
          },
          "self": {
            "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/24694772"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/search/findByPerson?uuid=gf3d657-9d6d-4a87-b905-fef0f8cae26c"
    }
  },
  "page": {
    "size": 20,
    "totalElements": 1,
    "totalPages": 1,
    "number": 0
  }
}
```

### single entry
**GET api/integration/suggestions/<:suggestion-id>**

It returns the data from one suggestion

sample for a suggestion /api/integration/suggestions/24694772
```json
{
    "id": "24694772",
    "display": "publication one",
    "source": "reciter",
    "external-source-uri": "https://dspace7.4science.cloud/server/api/integration/reciterSourcesEntry/pubmed/entryValues/24694772",
    "evidences": {
      "acceptedRejectedEvidence": {
        "score": "2.7",
        "notes": "notes"
      },
      "authorNameEvidence": {
        "score": "0",
        "notes": "notes"
      },
      "journalCategoryEvidence": {
        "score": "6",
        "notes": "notes"
      },
      "affiliationEvidence": {
        "score": "xxx",
        "notes": "notes"
      },
      "relationshipEvidence": {
        "score": "9",
        "notes": "notes"
      },
      "educationYearEvidence": {
        "score": "3.6",
        "notes": "notes"
      },
      "personTypeEvidence": {
        "score": "4",
        "notes": "notes"
      },
      "articleCountEvidence": {
        "score": "6.7",
        "notes": "notes"
      },
      "averageClusteringEvidence": {
        "score": "7",
        "notes": "notes"
      }
    },
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
    "type": "suggestion",
    "_links": {
      "target": {
        "href": "https://dspace7.4science.cloud/server/api/core/items/gf3d657-9d6d-4a87-b905-fef0f8cae26"
      },
      "self": {
        "href": "https://dspace7.4science.cloud/server/api/integration/suggestions/24694772"
      }
    }
}
```

## Import suggestion

See the [items endpoint](items.md#creating-an-archived-item-from-an-external-source) for details on how to import a suggestion

## Discard suggestion
**DELETE api/integration/suggestions/<:suggestion-id>**

This discard the given suggestion.

Status codes:
* 201 Created - if the operation succeed
* 404 Not found - if the entry doesn't exist
