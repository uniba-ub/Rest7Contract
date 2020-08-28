# Boxes Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint

**/api/layout/sections**   

Provide access to all the configured CRIS layout sections. The full JSON response document is as follow
```json
{
  "_embedded": {
    "sections": [
      {
        "id": "publications",
        "componentRows": [
          [
            {
              "browseNames": [
                "itemdept",
                "author",
                "title",
                "type",
                "dateissued",
                "subject"
              ],
              "componentType": "browse",
              "style": "col-md-4"
            }
          ],
          [
            {
              "discoveryConfigurationName": "publication",
              "sortField": "dateaccessioned_dt",
              "order": "desc",
              "componentType": "top",
              "style": "col-md-6"
            }
          ]
        ],
        "type": "section",
        "_links": {
          "self": {
            "href": "http://localhost:8080/server/api/layout/sections/publications"
          }
        }
      },
      {
        "id": "researcherprofiles",
        "componentRows": [
          [
            {
              "browseNames": [
                "rpname",
                "rpdept"
              ],
              "componentType": "browse",
              "style": "col-md-4"
            }
          ]
        ],
        "type": "section",
        "_links": {
          "self": {
            "href": "http://localhost:8080/server/api/layout/sections/researcherprofiles"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/server/api/layout/sections"
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
## Single Section
**/api/layout/sections/<:id>**

Provide detailed information about a specific CRIS layout section. The JSON response document is as follow
```json
{
  "id": "publications",
  "componentRows": [
    [
      {
        "browseNames": [
          "itemdept",
          "author",
          "title",
          "type",
          "dateissued",
          "subject"
        ],
        "componentType": "browse",
        "style": "col-md-4"
      },
      {
        "discoveryConfigurationName": "publication",
        "componentType": "search",
        "style": "col-md-8"
      }
    ],
    [
      {
        "discoveryConfigurationName": "publication",
        "sortField": "dateaccessioned_dt",
        "order": "desc",
        "componentType": "top",
        "style": "col-md-6"
      },
      {
        "discoveryConfigurationName": "publication",
        "componentType": "facet",
        "style": "col-md-6"
      }
    ]
  ],
  "type": "section"
}
```
Return codes:
* 200 OK - if the operation succeed
* 404 Not found - if a section with the given id doesn't exist

The `componentRows` attribute represent the list of components that compose the section, splitted by rows. There are 4 different types of components, distinguishable by their `componentType` attribute which can have one of the following values: [ `browse`,`top`,`facet`,`search` ]. The attributes of each component may vary according to the type of the component itself. In addition to the `componentType` attribute used to indicate the type of the component, each component type has the following attributes:
* `browse`: has only one attribute named `browseNames` representing a list of names
* `top`: has the `discoveryConfigurationName` indicating the discovery configuration name and two attributes named `sortField` and `order` indicating by which field and in what order to sort the search results
* `facet`: has the `discoveryConfigurationName` indicating the discovery configuration name
* `search`: has the `discoveryConfigurationName` indicating the discovery configuration name
