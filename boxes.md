# Boxes Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/layout/boxes**   

Not implemented

## Single Box
**/api/layout/boxes/<:id>**

Provide detailed information about a specific box. The JSON response document is as follow
```json
{
  "id": 1,
  "shortname": "primary",
  "header": "Primary Information",
  "entity-type": "researcherpage",
  "collapsed": false,
  "minor": false,
  "style": "col-md-6",
  "priority": 1,
  "group": 1,
  "security": 0,
  "box-type": "search",
  "type": "box"
}
```

Attributes
* the *header* attribute is the label or the i18n key to use to present the section to the user
* the *security* attribute is a constant where 0 mean public, 1 mean administrators, 2 mean owner only, 3 owner & administrators, 4 custom metadata
* the *minor* attribute is used to flag box that should be ignored in the determination of the tab visualization
* the box-type attribute is used to choice the appropriate component. It could be metadata, search, bibliometrics 

Exposed links:
* configuration: link to a configuration entity with more information specific for the box type
* fields: link to the fields that belong to this tab
* securityMetadata: link to the metadatafields that defined the security

## Linked entities
### Fields
#### Retrieve included boxes
**GET /api/layout/boxes/<:id>/fields**

It returns all the fields included in the box.

## Search methods
### findByItem
**/api/layout/boxes/search/findByItem?uuid=<:item-uuid>&tab=<:id>**

It returns the boxes that are available for the specified item in the requested tab. The boxes are sorted by priority ascending. This are filtered based on the permission of the current user and available data in the items (empty boxes are not included).

### findByEntityType
**/api/layout/boxes/search/findByEntityType?type=<:string>**

It returns the boxes that are available for the items of the specified type. This endpoint is reserved to system administrators