# Subscriptions Endpoints

[Back to the list of all defined endpoints](endpoints.md)

This endpoint contains all of the subscription requested

## Main Endpoint

**/api/core/subscriptions**

Retrieve a pageable list of subscriptions. The subscriptions are ordered by eperson number ascending.

```json
{
  "_embedded": {
    "subscriptions": [
      {
        "id": 60,
        "type": "subscription",
        "subscriptionParameterList": [],
        "subscriptionType": "subscription",
        "_links": {
          "dSpaceObject": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
          },
          "ePerson": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
          },
          "self": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/search/findByEPerson?id=49e5ff01-5467-4acd-be21-9ad7374be929"
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

## Single Subscription Object

**/api/core/subscription/<:id>**

```json
{
  "id": 33,
  "type": "subscription",
  "subscriptionParameterList": [],
  "subscriptionType": "subscription",
  "_links": {
    "dSpaceObject": {
      "href": "http://localhost:8080/server/api/core/subscriptions/33/dSpaceObject"
    },
    "ePerson": {
      "href": "http://localhost:8080/server/api/core/subscriptions/33/ePerson"
    },
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/33"
    }
  }
}
```

## A list of subscriptions based on ePerson

**/api/core/subscription/findByEPerson/<:id>**

```json
{
  "_embedded": {
    "subscriptions": [
      {
        "id": 60,
        "type": "subscription",
        "subscriptionParameterList": [],
        "subscriptionType": "subscription",
        "_links": {
          "dSpaceObject": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
          },
          "ePerson": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
          },
          "self": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/search/findByEPerson?id=49e5ff01-5467-4acd-be21-9ad7374be929"
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

## Adding subscription

It is possible to add a subscription
`curl -X PATCH '{dspace7-url}/api/core/subscriptions?dspace_object_id={id}&eperson_id={id}
' -H "Authorization: Bearer ..." -H 'Content-Type: application/json'

```json
{
  "type": "Test",
  "subscriptionParameterList": [
    {
      "name": "test",
      "value": "test"
    },
    {
      "name": "test1",
      "value": "test2"
    }
  ]
}
```

## Updating subscription

It is possible to update a subscription with id
`curl -X PATCH '{dspace7-url}/api/core/subscriptions/{id}?dspace_object_id={id}&eperson_id={id}
' -H "Authorization: Bearer ..." -H 'Content-Type: application/json'

```json
{
  "type": "Test",
  "subscriptionParameterList": [
    {
      "name": "hybas",
      "value": "fghbfgas"
    }
  ]
}
```

## Finds all subscription by dso and eperson

**GET /api/core/subscriptions?dspace_object_id={id}&eperson_id={id}>**
Find all subscription that a person made for a dataSpaceObject

```json
{
    "subscriptions": [
      {
        "id": 60,
        "type": "subscription",
        "subscriptionParameterList": [],
        "subscriptionType": "subscription",
        "_links": {
          "dSpaceObject": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
          },
          "ePerson": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
          },
          "self": {
            "href": "http://localhost:8080/server/api/core/subscriptions/60"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/search/findByEPerson?id=49e5ff01-5467-4acd-be21-9ad7374be929"
    }
  },
  "page": {
    "size": 20,
    "totalElements": 1,
    "totalPages": 1,
    "number": 0
  
}
```

## Patch operations

### Adding subscription parameter

It is possible to add a subscription parameter
`curl -X PATCH '{dspace7-url}/api/core/subscriptions/{id}' -H "Authorization: Bearer ..." -H 'Content-Type:
application/json' --data '[{
"op": "add",
"path": "/subscriptionsParameter",
"value" :{
"name": "Frequency",
"value":"Daily"
} }]'

that will transform

 ```json
{
  "id": 60,
  "type": "subscription",
  "subscriptionParameterList": [
    {
      "id": 112,
      "name": "test@123fghnfh",
      "value": "test@vn"
    }
  ],
  "subscriptionType": "subscription",
  "_links": {
    "dSpaceObject": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
    },
    "ePerson": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
    },
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60"
    }
  }
}
```

in

```json
{
  "id": 60,
  "type": "subscription",
  "subscriptionParameterList": [
    {
      "id": 112,
      "name": "Existent",
      "value": "Existent"
    },
    {
      "id": 113,
      "name": "Frequency",
      "value": "Daily"
    }
  ],
  "subscriptionType": "subscription",
  "_links": {
    "dSpaceObject": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
    },
    "ePerson": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
    },
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60"
    }
  }
}
```

Return codes:

* 200 OK if the path operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators can use the endpoint
* 404 Not found - if box doesn't exist (or was already deleted)
* 422 Unprocessable Entity - if the metadata doesn't exist

### Removing metadata

It is possible to remove an metadata curl --data '[{ "op": "remove", "path": "/subscriptionsParameter/112"}]'
-X PATCH ${dspace7-url}/api/core/subscriptions/60

that will transform

 ```json
{
  "id": 60,
  "type": "subscription",
  "subscriptionParameterList": [
    {
      "id": 112,
      "name": "Existent",
      "value": "Existent"
    },
    {
      "id": 113,
      "name": "Frequency",
      "value": "Daily"
    }
  ],
  "subscriptionType": "subscription",
  "_links": {
    "dSpaceObject": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
    },
    "ePerson": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
    },
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60"
    }
  }
}
```

in

 ```json
{
  "id": 60,
  "type": "subscription",
  "subscriptionParameterList": [
    {
      "id": 113,
      "name": "Frequency",
      "value": "Daily"
    }
  ],
  "subscriptionType": "subscription",
  "_links": {
    "dSpaceObject": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
    },
    "ePerson": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
    },
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60"
    }
  }
}
```

Return codes:

* 200 OK if the path operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators can use the endpoint
* 404 Not found - if box doesn't exist (or was already deleted)
* 422 Unprocessable Entity - if the metadata doesn't exist


### Replacing subscription parameter

It is possible to replace a subscription parameter
`curl -X PATCH '{dspace7-url}/api/core/subscriptions/{id}' -H "Authorization: Bearer ..." -H 'Content-Type:
application/json' --data '[{
"op": "replace",
"path": "/subscriptionsParameter/113",
"value" :{
"name": "Test",
"value":"Test"
} }]'

that will transform

 ```json
{
  "id": 60,
  "type": "subscription",
  "subscriptionParameterList": [
    {
      "id": 113,
      "name": "Frequency",
      "value": "Daily"
    }
  ],
  "subscriptionType": "subscription",
  "_links": {
    "dSpaceObject": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
    },
    "ePerson": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
    },
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60"
    }
  }
}
```

in

```json
{
  "id": 60,
  "type": "subscription",
  "subscriptionParameterList": [
    {
      "id": 113,
      "name": "Test",
      "value": "Test"
    }
  ],
  "subscriptionType": "subscription",
  "_links": {
    "dSpaceObject": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/dSpaceObject"
    },
    "ePerson": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60/ePerson"
    },
    "self": {
      "href": "http://localhost:8080/server/api/core/subscriptions/60"
    }
  }
}
```

Return codes:

* 200 OK if the path operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators can use the endpoint
* 404 Not found - if box doesn't exist (or was already deleted)
* 422 Unprocessable Entity - if the metadata doesn't exist

## Deleting a Subscription Object

**DELETE /api/core/subscriptions/<:id>**

Deletes a subscription with id.

* 204 No content - if the operation succeed.
* 401 Unauthorized - if you are not authenticated.
* 403 Forbidden - if you are not logged in with sufficient permissions. It must be creator or administrator.
* 500 Not found - if the subscription with id doesn't exist (or was already deleted).