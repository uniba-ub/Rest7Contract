# Metadata Components Endpoints

[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint

**/api/layout/metadatacomponents**   

Not implemented

## Single Metadata Component

**/api/layout/metadatacomponents/<:string>**

Provide detailed information about a specific Metadata Component. The JSON response document is as follow

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

It provides the configuration for a component that visualize a list of metadata according to specific rules

Attributes
* the *label* attribute is the i18n key for the field label to visualize
* the *rendering* attribute defines the component to use to visualize the field. Examples are browselink, longtext, identifier, date, etc. for metadata field and preview, thubmnail, etc. for bitstream field 
* the *style* attribute allows to set arbitrary css styles to the generated html
* the *fieldType" is one of metadata or bitstream a corresponding attribute will be present
    * metadata: is the canonical name of the metadata to use (eg dc.contributor.author, dc.title, etc.)
    * bitstream: is an object containing details to filter the bitstreams to use. It can be the name of the bundle to use and/or the value of specfic bitstream metadata

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the resourcepolicy
* 404 Not found - if the resourcepolicy doesn't exist (or was already deleted)
