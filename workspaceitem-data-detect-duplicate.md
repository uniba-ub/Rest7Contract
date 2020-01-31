# WorkspaceItem data of detect duplicate sectionType
[Back to the definition of the workspaceitems endpoint](workspaceitems.md)

The section data represent the data about duplicates detected during submission

```json
{
  "matches" : {
	"9db079fc-359f-4aa4-ad4f-2dd2f0afaac6" : {
	  "submitterDecision" : null,
	  "workflowDecision" : null,
	  "adminDecision" : null,
	  "submitterNote" : null,
	  "workflowNote" : null,
	  "matchObject" : {
		"id" : "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6",
		"uuid" : "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6",
		"name" : "Sample submission",
		"handle" : "123456789/28381",
		...
	  }
	},
   ...
  }
}
```

## Patch operations
The PATCH method expects a JSON body according to the [JSON Patch specification RFC6902](https://tools.ietf.org/html/rfc6902)

Each successful Patch operation will return a HTTP 200 CODE with the new workspaceitem as body 

### Add

To check for duplicates, the client must send a JSON Patch ADD operation to  the *detect-duplicate* path as follow
`curl --data '[ { "op": "add", "path": "/sections/detect-duplicate/matches/<:object-id>/submitterDecision", "value": {"value":"verify","note":"test"}}]' -X PATCH ${dspace7-url}/api/submission/workspaceitems/<:id>`

for example if a item exist with the following metadata
```json
{
 "id": "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6",
 "uuid": "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6",
 "name": "Sample submission",
 "handle": "123456789/28381",
 "metadata": [
   {
	 "key": "dc.contributor.author",
	 "value": "Francesco, Cadili",
	 "language": null,
	 "authority": "rp05896",
	 "confidence": 600
   },
   {
	 "key": "dc.contributor.editor",
	 "value": "Matteo, Perelli",
	 "language": null,
	 "authority": "rp05897",
	 "confidence": 600
   },
   ...
   {
	   "key": "dc.title",
	   "value": "Sample submission",
	   "language": null,
	   "authority": null,
	   "confidence": -1
	 }
   ],
   "inArchive": true,
   "discoverable": true,
   "withdrawn": false,
   "lastModified": "2020-01-31T10:53:37.227+0000",
   "type": "item"
}	
```

and we are submitting a workspace item:
```json
{
  "id": 43366,
  ...,
  "_embedded": {
    ...,
    "item": {
      "id": "8a4d8ed1-9ad0-413f-8122-710231bea28e",
      "uuid": "8a4d8ed1-9ad0-413f-8122-710231bea28e",
      "name": "sample submission",
      "handle": null,
      "metadata": [
        {
          "key": "dc.title",
          "value": "sample submission",
          "language": null,
          "authority": null,
          "confidence": -1
        }
      ],
      "inArchive": false,
      "discoverable": true,
      "withdrawn": false,
      "lastModified": "2020-01-31T11:58:03.355+0000",
      "type": "item",
      "_links": {
        "bitstreams": {
          "href": "http://localhost:8082/spring-rest/api/core/items/8a4d8ed1-9ad0-413f-8122-710231bea28e/bitstreams"
        },
        "owningCollection": {
          "href": "http://localhost:8082/spring-rest/api/core/items/8a4d8ed1-9ad0-413f-8122-710231bea28e/owningCollection"
        },
        "templateItemOf": {
          "href": "http://localhost:8082/spring-rest/api/core/items/8a4d8ed1-9ad0-413f-8122-710231bea28e/templateItemOf"
        },
        "self": {
          "href": "http://localhost:8082/spring-rest/api/core/items/8a4d8ed1-9ad0-413f-8122-710231bea28e"
        }
      },
      "_embedded": {
        "owningCollection": null,
        "templateItemOf": null,
        "bitstreams": null
      }
    }
}
```

the following request:
`curl --data 'curl --data '[ { "op": "add", "path": "/sections/detect-duplicate/matches/8a4d8ed1-9ad0-413f-8122-710231bea28e/submitterDecision", "value": {"value":"verify","note":"test"}}]' -X PATCH ${dspace7-url}/api/submission/workspaceitems/43366`

will result in
```json
{
  "id": 43366,
  ...
  "sections": {
    ...,
    "detect-duplicate": {
      "matches": {
        "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6": {
		  ...,
          "matchObject": {
            "id": "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6",
            "uuid": "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6",
            "name": "Sample submission",
            "handle": "123456789/28381",
            "metadata": [
              {
                "key": "dc.contributor.author",
                "value": "Francesco, Cadili",
                "language": null,
                "authority": "rp05896",
                "confidence": 600
              },
              {
                "key": "dc.contributor.editor",
                "value": "Matteo, Perelli",
                "language": null,
                "authority": "rp05897",
                "confidence": 600
              },
              ...,
              {
                "key": "dc.title",
                "value": "Sample submission",
                "language": null,
                "authority": null,
                "confidence": -1
              },
              ...
            ],
            "inArchive": true,
            "discoverable": true,
            "withdrawn": false,
            "lastModified": "2020-01-31T10:53:37.227+0000",
            "type": "item"
          }
        },
        "1320eb17-b7e5-4452-bf93-9f9ec234b8d5": {
          ...,
          "matchObject": {
            "id": "1320eb17-b7e5-4452-bf93-9f9ec234b8d5",
            "uuid": "1320eb17-b7e5-4452-bf93-9f9ec234b8d5",
            "name": "Sample submission",
            "handle": null,
            "metadata": [
              {
                "key": "dc.title",
                "value": "Sample submission",
                "language": null,
                "authority": null,
                "confidence": -1
              },
              ...
            ],
            "inArchive": false,
            "discoverable": true,
            "withdrawn": false,
            "lastModified": "2020-01-31T11:25:30.584+0000",
            "type": "item"
          }
        }
      }
    },
    ...
  }
}
```

nside the Json result, two matching items are returned: the item "9db079fc-359f-4aa4-ad4f-2dd2f0afaac6" and the one related to the workspace item 43366.

### Replace

### Remove

### Move, Test & copy
No plan to implement the move, test and copy operations at the current stage
