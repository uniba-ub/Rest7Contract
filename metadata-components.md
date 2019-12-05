# Metadata Components Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/layout/metadatacomponents**   

Not implemented

## Single Metadata Component
**/api/layout/metadatacomponents/<:string>**

Provide detailed information about a specific community. The JSON response document is as follow
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
	  		field-type: "metadata",
	  		style: null
	  	},
	  	{
	  		bitstream: {
	  			bundle: "ORIGINAL", 
	  			metadata: {
	  				"dc.type": "picture"
	  			}
	  		},
	  		label: "Authors",
	  		rendering: "thumbnail",
	  		field-type: "bitstream",
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
* the *field-type" is one of metadata or bitstream a corresponding attribute will be present
    * metadata: is the canonical name of the metadata to use (eg dc.contributor.author, dc.title, etc.)
    * bitstream: is an object containing details to filter the bitstreams to use. It can be the name of the bundle to use and/or the value of specfic bitstream metadata