# ItemExportFormats Endpoints
[Back to the list of all defined endpoints](endpoints.md)

An item export format describe a supported way to export items with the same entity type and the allowed molteplicities (single, multi, single and multi). 

## Main Endpoint
**/api/integration/itemexportformat**

Provide access to all the supported formats. The full JSON response document is as follow

```json
{
    "_embedded": {
        "itemexportformats": [
            {
                "id": "endnote",
                "mimeType": "application/x-endnote-refer; charset=UTF-8",
                "entityType": "Publication",
                "molteplicity": "SINGLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/endnote"
                    }
                }
            },
            {
                "id": "person-xls",
                "mimeType": "application/vnd.ms-excel",
                "entityType": "Person",
                "molteplicity": "MULTIPLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/person-xls"
                    }
                }
            },
            {
                "id": "person-pdf",
                "mimeType": "application/pdf",
                "entityType": "Person",
                "molteplicity": "SINGLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/person-pdf"
                    }
                }
            },
            {
                "id": "publication-xml",
                "mimeType": "application/xml; charset=UTF-8",
                "entityType": "Publication",
                "molteplicity": "SINGLE_AND_MULTIPLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/publication-xml"
                    }
                }
            },
            {
                "id": "bibtex",
                "mimeType": "application/x-bibtex; charset=UTF-8",
                "entityType": "Publication",
                "molteplicity": "SINGLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/bibtex"
                    }
                }
            },
            {
                "id": "publication-pdf",
                "mimeType": "application/pdf",
                "entityType": "Publication",
                "molteplicity": "SINGLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/publication-pdf"
                    }
                }
            },
            {
                "id": "person-xml",
                "mimeType": "application/xml; charset=UTF-8",
                "entityType": "Person",
                "molteplicity": "SINGLE_AND_MULTIPLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/person-xml"
                    }
                }
            },
            {
                "id": "person-json",
                "mimeType": "application/json; charset=UTF-8",
                "entityType": "Person",
                "molteplicity": "SINGLE_AND_MULTIPLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/person-json"
                    }
                }
            },
            {
                "id": "person-rtf",
                "mimeType": "application/rtf",
                "entityType": "Person",
                "molteplicity": "SINGLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/person-rtf"
                    }
                }
            },
            {
                "id": "person-csv",
                "mimeType": "text/csv",
                "entityType": "Person",
                "molteplicity": "MULTIPLE",
                "type": "itemexportformat",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/server/person-csv"
                    }
                }
            }
        ]
    },
    "_links": {
        "self": {
            "href": "http://localhost:8080/server/api/integration/itemexportformat"
        },
        "search": {
            "href": "http://localhost:8080/server/api/integration/itemexportformat/search"
        }
    },
    "page": {
        "size": 20,
        "totalElements": 10,
        "totalPages": 1,
        "number": 0
    }
}
```

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in

## Single ItemExportFormats
**/api/integration/itemexportformat/<:string>**

Provide detailed information about a specific item export format. An example JSON response document:
```json
{
    "id": "person-pdf",
    "mimeType": "application/pdf",
    "entityType": "Person",
    "molteplicity": "SINGLE",
    "type": "itemexportformat",
    "_links": {
        "self": {
            "href": "http://localhost:8080/server/person-pdf"
        }
    }
}
```

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in
* 404 Not found - if a section with the given id doesn't exist

### Search methods
#### byEntityTypeAndMolteplicity
**/api/integration/itemexportformat/search/byEntityTypeAndMolteplicity?entitytype=<:string>&molteplicity=<:string>**

It returns the list of the supported item export formats for the given entitytype and molteplicity.

The supported parameters are:
* page, size [see pagination](README.md#Pagination)
* entitytype: required  
* molteplicity: see org.dspace.content.crosswalk.CrosswalkMode can be one of SINGLE, MULTIPLE, SINGLE_AND_MULTIPLE

Return codes:
* 200 OK - if the operation succeed
* 400 Bad Request - if the entitytype parameter is missing or invalid
* 400 Bad Request - if the molteplicity parameter is invalid
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in

