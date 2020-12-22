# Displaying statistics categories
[Back to the list of all defined endpoints](endpoints.md)

## Statistics for a DSpaceObject
**GET /api/statistics/categories**

As we don't have a use case to iterate over all the existing categories, the main endpoint is not implemented and a 405 error code is returned according to our [general error response codes](README.md#Error-codes).

## Single statistic
**GET /api/statistics/categories/<:id>**

This endpoint provides a specific statistic category

An example JSON response document to `/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries`:
```json
{
    "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries",
    "type": "category",
    "category-type": "TopCountries",
    "_links" : {
     "usagereports" : {
       "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries/usagereports"
     },
     "self" : {
       "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries"
     }
    }
}
```

The ID is built from a concatenation of the UUID and the type of report for the given UUID

Possible response status

- 200 OK - The specific statistics category has been found, and the category has been properly returned.
* 401 Unauthorized - if you are not authenticated, and the statistics category is not available to the Anonymous user
* 403 Forbidden - if you are not logged in with sufficient permissions, and the statistics category is not available to the Anonymous user
- 404 Not Found - The specified ID has been not found

## Search Statistics for a DSpaceObject
**GET /api/statistics/categories/search/object**

This endpoint provides a paginated list of statistics category for a DSpaceObject. 

The DSpaceObject is given through the following parameters:
- `uri` The object to retrieve statistics for. The full URI of the rest resource must be specified, i.e. https://{dspace.url}/server/api/core/community/{uuid}
- `startDate` If present represent the date from which the statistics are to be taken into account (date format YYYY-MM)
- `endDate` If present represent the date until which the statistics are to be taken into account (date format YYYY-MM)

The usual parameters for paginated lists are supported as well:
- `page` The page number 
- `size` The number of reports in a page

An example JSON response document to `/api/statistics/categories/search/object?page=0&size=2&uri=https://{dspace.url}/server/api/core/site/6d65c6a2-3fe7-44dd-bacb-79271257c35d`:

```json
{
    "_embedded": {
        "categories": [
            {
                "id": "6d65c6a2-3fe7-44dd-bacb-79271257c35d_TotalVisits",
                "type": "category",
                "category-type": "TotalVisits",
                "_links" : {
                  "usagereports" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/6d65c6a2-3fe7-44dd-bacb-79271257c35d_TotalVisits/usagereports"
                  },
                  "self" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/6d65c6a2-3fe7-44dd-bacb-79271257c35d_TotalVisits"
                  }
                }
            }
        ]
    }
}
```

An example JSON response document to `/api/statistics/categories/search/object?uri=https://{dspace.url}/server/api/core/item/1911e8a4-6939-490c-b58b-a5d70f8d91fb`:

```json
{
    "_embedded": {
        "usagereports": [
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisits",
                "type": "category",
                "category-type": "TotalVisits",
                "_links" : {
                  "usagereports" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisits/usagereports"
                  },
                  "self" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisits"
                  }
                }
            },
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisitsPerMonth",
                "type": "category",
                "category-type": "TotalVisitsPerMonth",
                "_links" : {
                  "usagereports" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisitsPerMonth/usagereports"
                  },
                  "self" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisitsPerMonth"
                  }
                }
            },
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalDownloads",
                "type": "category",
                "report-type": "TotalDownloads",
                "_links" : {
                  "usagereports" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalDownloads/usagereports"
                  },
                  "self" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalDownloads"
                  }
                }
            },
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries",
                "type": "category",
                "report-type": "TopCountries",
                "_links" : {
                  "usagereports" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries/usagereports"
                  },
                  "self" : {
                    "href" : "https://{dspace.url}/server/api/statistics/categories/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries"
                  }
                }
            }
        ]
    }
}
```

Possible response status:
* 200 OK - The DSpaceObject has been found, and the data has been properly returned.
* 400 Bad Request - The uri parameter format is incorrect
* 401 Unauthorized - if you are not authenticated, and the statistics categories are not available to the Anonymous user
* 403 Forbidden - if you are not logged in with sufficient permissions, and the statistics categories are not available to the Anonymous user
