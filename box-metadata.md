# Metadata Layout Box

[Back to the list of all defined box types](boxes-types.md)

## Configuration structure

Provide detailed information about the metadata included in the box

```json
{
  "rows": [
    {
	  "fields": [
	  	{
	  		metadata: "dc.contibutor.author",
	  		label: "Authors",
	  		rendering: "browselink",
	  		fieldType: "metadata",
	  		style: null
	  	},
	  	{
	  		bitstream: {
	  			bundle: "ORIGINAL", 
	  			metadataField: "dc.type",
	  			metadataValue: "picture"
	  		},
	  		label: "Authors",
	  		rendering: "thumbnail",
	  		fieldType: "bitstream",
	  		style: null
	  	}
  	}
  ]
}
```

It provides the configuration for a component that visualize a list of metadata according to specific rules

Attributes
* the *label* attribute is the i18n key for the field label to visualize
* the *rendering* attribute defines the component to use to visualize the field. Examples are browselink, longtext, identifier, date, etc. for metadata field and preview, thubmnail, etc. for bitstream field 
* the *style* attribute allows to set arbitrary css styles to the generated html
* the *fieldType" is one of metadata or bitstream a corresponding attribute will be present
* metadata: is the canonical name of the metadata to use (eg dc.contributor.author, dc.title, etc.)
* bitstream: is an object containing details to filter the bitstreams to use. It can be the name of the bundle to use and/or the value of specfic bitstream metadata
 
## Patch operations

### Adding metadata
It is possible to add an metadata
`curl -X PATCH '{dspace7-url}/api/layout/metadatacomponents/<:id>'
-H "Authorization: Bearer ..." -H 'Content-Type: application/json'
--data '[{"op":"add","path":"/rows/0/<:fields>/0/0", "value":{"metadata":""orgunit.identifier.name"",
          "label":"Department Name", "rendering":"browselink", "fieldType":"metadata", "style":null }}]'

that will transform

 ```json
{
  "id": "box-shortname",
  "rows": [
    {
	  "fields": [
	  	{
	  		metadata: "dc.contibutor.author",
	  		label: "Authors",
	  		rendering: "browselink",
	  		fieldType: "metadata",
	  		style: null
	  	},
	  	{
	  		bitstream: {
	  			bundle: "ORIGINAL", 
	  			metadataField: "dc.type",
	  			metadataValue: "picture"
	  		},
	  		label: "Authors",
	  		rendering: "thumbnail",
	  		fieldType: "bitstream",
	  		style: null
	  	}
  	}
  ],
  "type": "metadatacomponent"
}
```
in

```
{
  "id": "box-shortname",
  "rows": [
    {
	  "fields": [
	  	{
	  		metadata: "orgunit.identifier.name",
	  		label: "Department Name",
	  		rendering: "browselink",
	  		fieldType: "metadata",
	  		style: null
	  	},
	  	{
	  		metadata: "dc.contibutor.author",
	  		label: "Authors",
	  		rendering: "browselink",
	  		fieldType: "metadata",
	  		style: null
	  	},
	  	{
	  		bitstream: {
	  			bundle: "ORIGINAL", 
	  			metadataField: "dc.type",
	  			metadataValue: "picture"
	  		},
	  		label: "Authors",
	  		rendering: "thumbnail",
	  		fieldType: "bitstream",
	  		style: null
	  	}
  	}
  ],
  "type": "metadatacomponent"
}
```
Return codes:
* 200 Ok if the path operation succeed
* 401 Unauthorized - if you are not authenticated.  Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators or user with ADMIN permission over the target resource can use the endpoint
* 404 Not found - if the resource policy doesn't exist (or was already deleted)
* 422 Unprocessable Entity - if the metadata don't exist

### Removing metadata
It is possible to remove an metadata
curl --data '[{ "op": "remove", "path": "/rows/0/<:fields>/0"}]'
 -X PATCH ${dspace7-url}/api/layout/metadatacomponents/<:id>
 
that will transform
 
 ```json
{
  "id": "box-shortname",
  "rows": [
    {
	  "fields": [
	  	{
	  		metadata: "dc.contibutor.author",
	  		label: "Authors",
	  		rendering: "browselink",
	  		fieldType: "metadata",
	  		style: null
	  	},
	  	{
	  		bitstream: {
	  			bundle: "ORIGINAL", 
	  			metadataField: "dc.type",
	  			metadataValue: "picture"
	  		},
	  		label: "Authors",
	  		rendering: "thumbnail",
	  		fieldType: "bitstream",
	  		style: null
	  	}
  	}
  ],
  "type": "metadatacomponent"
}
```
in

 ```json
{
  "id": "box-shortname",
  "rows": [
    {
	  "fields": [
	  	{
	  		bitstream: {
	  			bundle: "ORIGINAL", 
	  			metadataField: "dc.type",
	  			metadataValue: "picture"
	  		},
	  		label: "Authors",
	  		rendering: "thumbnail",
	  		fieldType: "bitstream",
	  		style: null
	  	}
  	}
  ],
  "type": "metadatacomponent"
}
```

 Return codes:
 * 204: if the delete succeeded
 * 401  Unauthorized - if you are not authenticated
 * 403  Forbidden - if you are not logged in with sufficient permissions 
 * 422: if the specified metadata don't exist
    