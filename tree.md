# Tree Endpoints
[Back to the list of all defined endpoints](endpoints.md)

A tree contains hierarchically structured informations about some entities. Additionally every node of the tree has some metrics to show about itself or all subordinated nodes.

## OrgUnittree

**/api/orgunittree**

Provide detailed information about the root node(s) of the tree in an ordered list. The structural relation to the subordinate node is mentioned in the childs attribute containing the uuid as string. Additional metrics about the node and aggregated metrics from all subordinated nodes are in the metrics/aggregatedmetrics attribute. The item itself is embedded inside the node resource.  The JSON response document is as follow:

```json
{  
  "_embedded": {  
    "orgunittreeNodeResources": [  
      { 
      "childs": [],  
        "metrics": {  
          "persons": 0  
        }, 
        "aggregatedmetrics": {  
          "personsaggregated": 0  
        },  
        "uuid": "3550bd51-6369-4897-ae71-9eae5da4d29f",  
        "item": {  
          "id": "3550bd51-6369-4897-ae71-9eae5da4d29f",  
          "uuid": "3550bd51-6369-4897-ae71-9eae5da4d29f",  
          "name": "Fakultät Guk",  
          "handle": "uniba/55555",  
          "metadata": {  
          ... 
          }  
          ...  
          }  
          ...  
          },  
          {...},  
          {...}  
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/server/api/orgunittree"
    }
  },
  "page": {
    "size": 20,
    "totalElements": 7,
    "totalPages": 1,
    "number": 0
  }
```

Return codes:
* 200 OK - if the operation succeed
* 500 Error - Internal Error
* 503 Service Unavailable - if the tree is not enabled


**/api/orgunittree/<:uuid>**  
Provide detailed information about the node specified by :uuid in the tree tree. The structural relation to the subordinate node is mentioned in the childs attribute containing the uuid as string. Additional metrics about the node and aggregated metrics from all subordinated nodes are in the metrics/aggregatedmetrics attribute. The item itself is embedded inside the node resource. The JSON response document is as follow:
```json
{
  "childs": [],
  "metrics": {
    "persons": 0
  },
  "aggregatedmetrics": {
    "personsaggregated": 0
  },
  "uuid": "3550bd51-6369-4897-ae71-9eae5da4d29f",
  "item": {
    "id": "3550bd51-6369-4897-ae71-9eae5da4d29f",
    "uuid": "3550bd51-6369-4897-ae71-9eae5da4d29f",
    "name": "Fakultät Guk",
    "handle": "uniba/55555",
    "metadata": {
	...
    	}
    }
}
```

Return codes:
* 200 OK - if the operation succeed
* 404 NotFound - no node with uuid found inside the tree.
* 500 Error - Internal Error
* 503 Service Unavailable - if the tree is not enabled

**/api/orgunittree/recreate**  
Recreates the tree and delivers the recreated tree. Access is restricted to system administrators. The JSON response document is as follow

```json
{  
  "_embedded": {  
    "orgunittreeNodeResources": [  
      { 
      "childs": [],  
        "metrics": {  
          "persons": 0  
        }, 
        "aggregatedmetrics": {  
          "personsaggregated": 0  
        },  
        "uuid": "3550bd51-6369-4897-ae71-9eae5da4d29f",  
        "item": {  
          "id": "3550bd51-6369-4897-ae71-9eae5da4d29f",  
          "uuid": "3550bd51-6369-4897-ae71-9eae5da4d29f",  
          "name": "Fakultät Guk",  
          "handle": "uniba/55555",  
          "metadata": {  
          ... 
          }  
          ...  
          }  
          ...  
          },  
          {...},  
          {...}  
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/server/api/orgunittree"
    }
  },
  "page": {
    "size": 20,
    "totalElements": 7,
    "totalPages": 1,
    "number": 0
  }
```


Return codes:
* 200 OK - if the operation succeed
* 500 Error - Internal Error
* 401 Unauthorized - if you are not logged in. Only system administrators can access
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators can access
* 503 Service Unavailable - if the tree is not enabled
