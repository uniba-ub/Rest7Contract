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