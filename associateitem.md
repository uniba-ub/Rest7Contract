# AssociateItem Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Create AssociateItem
PUT **/api/core/associateitem/create?sourceuuid=<:sourceuuid>&targetuuid=<:targetuuid>&modename=<:modename>**

Create a metadatafield from <:sourceuuid> pointing with its authority value to <:targetuuid< with the configuration from <:modename>. Checks authorizations from the mode configuration (extended permission check) on both items.
Provide information about whether the operation succeeded. The response is a simple boolean text value.
```text  
true|false
```
Return codes:
* 200 OK - if the metadata already existed
* 201 Created - if the metadata was created
* 401 Unauthorized - if you are not authenticated
* 403 if you are not logged in with sufficient permissions to edit one of the item based on the configuration
* 503 if the feature is globally deactivated

## Delete AssociateItem
DELETE **/api/core/associateitem/delete?sourceuuid=<:sourceuuid>&targetuuid=<:targetuuid>&modename=<:modename>**

Delete a metadatafield from <:sourceuuid> pointing with its authority value to <:targetuuid< with the configuration from <:modename>-
Provide information about whether the operation succeeded. The response is a simple boolean text value.
```text  
true|false
```
Return codes:
* 200 OK - if the metadata was deleted
* 401 Unauthorized - if you are not authenticated
* 403 if you are not logged in with sufficient permissions to edit one of the item based on the configuration
* 503 if the feature is globally deactivated

## Find available associateitem modes
**/api/core/associateitemmodes/search/search/findModesById?uuid=<:id>**

Provide detailed information about associate item modes available to current user for Item having uuid passed as input parameter.
The JSON response document is as follows:
```json
{
  "_embedded": {
    "associateitemmodes": [
      {
        "id": "PROJECTPUBLICATION",
        "name": "PROJECTPUBLICATION",
        "label": null,
        "discovery": "fundings",
				"metadatafield": "dc.relation.funding",
        "type": "associateitemmode",
        "_links": {
          "self": {
            "href": "https://{dspace-cris-backend-url}/server/api/core/associateitemmodes/PROJECTPUBLICATION"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://{dspace-cris-backend-url}/server/api/core/associateitemmodes/search/findModesById?uuid=9880d9e1-5441-4e14-a6e8-6cf453bc25f9"
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
Return codes:
* 200 OK - if the operation succeed
* 400 Bad request - if the id parameter is missing or invalid
