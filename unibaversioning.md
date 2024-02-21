
# Uniba Versioning Endpoints  
[Back to the list of all defined endpoints](endpoints.md)

## Create Version
PUT **/api/core/unibaversioning/<:uuid>

Create a new item from <:uuid> with the copy of all metadatafields in the submit-forms for the belonging Collection. The originated item is being added as some additional metadatafield information. Checks authorizations from the versioning configuration (extandable filter check) whether some version is allowed to be created.
Provide informations about the newly created workspaceitem. The JSON response is as follow:
```json
{
  "id": 1911,
  "lastModified": "2017-06-24T00:40:54.970+0000",
  "sections": {
  	 "collection": "05457c63-b392-4629-a373-f2d66ee9ee33",
  	 "traditional-page1": {
  	 	"dc.title" : [{value: "La question de la licéité des images dans le judaïsme ancien à travers l’exemple des pavements en mosaïque de deux synagogues africaines"}],
      "dc.relation.versionof" : [{value: "uniba/56128", authority: "6835a474-c2ab-40fe-b671-1ffd1a70802e", confidence: 600}],
  	 },
  	 "license": {},
  	 "uploads": []
  	},
  	 "cclicense": {}
  },
  "type": "workspaceitem"
}
```

Return codes:
* 201 Created - if the item was created
* 401 Unauthorized - if you are not authenticated
* 403 if you are not logged in with sufficient permissions to edit one of the item based on the configuration or the feature is deactivated

## Change Version
POST **/api/core/unibaversioning/change/<:uuid>

Change the main version of some version group. The item with uuid <:uuid> is set to the main member and all related versioning references to this item are updated. Checks authorizations from the versioning configuration (extandable filter check) whether the current user is allowed to change the version.
Provide informations about the changed item The JSON response is as follow:
```json
{
  "uuid": "1911e8a4-6939-490c-b58b-a5d70f8d91fb",
  "name": "Practices of research data curation in institutional repositories: A qualitative view from repository staff",
  "handle": "10673/20",
  "metadata": {
    "dc.contributor.author": [
      {
        "value": "Stvilia, Besiki",
        "language": "en",
        "authority": null,
        "confidence": -1,
        "place": 0
      },
      {
        "value": "Lee, Dong Joon",
        "language": "en",
        "authority": null,
        "confidence": -1,
        "place": 1
      }
    ],
    "dc.identifier.url": [
      {
        "value": "http://europepmc.org/abstract/MED/28301533",
        "language": "en",
        "authority": null,
        "confidence": -1,
        "place": 0
      }
    ],
    "dc.title": [
      {
        "value": "Practices of research data curation in institutional repositories: A qualitative view from repository staff",
        "language": "en",
        "authority": null,
        "confidence": -1,
        "place": 0
      }
    ],
    "dc.type": [
      {
        "value": "Journal Article",
        "language": "en",
        "authority": null,
        "confidence": -1,
        "place": 0
      }
    ]
  },
  "inArchive": true,
  "discoverable": true,
  "withdrawn": false,
  "lastModified": "2017-06-24T00:40:54.970+0000",
  "type": "item"
}
```

Return codes:
* 201 Created - if the item was created
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions to change the versionof
* 404 Not Found - if the specified item (<:uuid>) was not found
* 409 Conflict - if some change in the version group is not possible because this would create some invalid structure inside the version group
* 500 Internal Error - if some error occured

## Check Version group
GET **/api/core/unibaversioning/check/<:uuid>

Check the version group where this item with <:uuid> belongs to.
Returns an empty List or an list of string error descriptions for all items in this version group. Only for authenticated users.
```
['error1','error2']
```

Return codes:
* 200 OK - if the check has succeded
* 401 Unauthorized - if you are not authenticated
* 404 Not Found - if the specified item (<:uuid>) was not found
* 500 Internal Error - if some error occured


## Get all Version group members
GET **/api/core/unibaversioning/group/<:uuid>

Get all versions of the version group wehere Item with <:uuid> item is member in. The main version should be at first place of the list. Returns an empty list if no entries were found or the check fails (check can be disabled by parameter). Otherwise returns an PaginatedList of Item. Only for authenticated users.

The supported parameters are:
* ignorecheck : disable the check for valid versioning structure and deliver all version members

Return codes:
* 200 OK - if the operation succeed. It might result in an empty list
* 401 Unauthorized - if you are not authenticated and the items are not visible to anonymous users
* 403 Forbidden - if you are not logged in with sufficient permissions.
* 404 Not found - if the item doesn't exist
