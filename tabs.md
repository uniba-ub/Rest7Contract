# Tabs Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/layout/tabs**   

Not implemented

## Single Tab
**/api/layout/tabs/<:id>**

Provide detailed information about a specific tab. The JSON response document is as follow
```json
{
  "id": 1,
  "shortname": "info",
  "header": "Profile",
  "entity-type": "researcherpage",
  "priority": 1,
  "security": 0,
  "type": "tab"
}
```

Attributes
* the *header* attribute is the label or the i18n key to use to present the section to the user
* the *security* attribute is a constant where 0 mean public, 1 mean administrators, 2 mean owner only, 3 owner & administrators, 4 custom metadata

Exposed links:
* boxes: link to the boxes that belong to this tab
* securityMetadata: link to the metadatafields that defined the security

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the resourcepolicy
* 404 Not found - if the resourcepolicy doesn't exist (or was already deleted)

## Linked entities
### Boxes
#### Retrieve included boxes
**GET /api/layout/tabs/<:id>/boxes**

It returns all the boxes included in the tab. The boxes are sorted by priority ascending. This endpoint is reserved to system administrators

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the resourcepolicy
* 404 Not found - if the resourcepolicy doesn't exist (or was already deleted)

### SecurityMetadata
#### Retrieve SecurityMetadata of the tab
**GET /api/layout/tabs/<:id>/securitymetadata**

It returns all the metadatafields that defined the security. This endpoint is reserved to system administrators

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the resourcepolicy
* 404 Not found - if the resourcepolicy doesn't exist (or was already deleted)

## Search methods
### findByItem
**/api/layout/tabs/search/findByItem?uuid=<:item-uuid>**

It returns the tabs that are available for the specified item. The tabs are sorted by priority ascending. This are filtered based on the permission of the current user and available data. Empty tabs are filter out.

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the resourcepolicy
* 404 Not found - if the resourcepolicy doesn't exist (or was already deleted)

### findByEntityType
**/api/layout/tabs/search/findByEntityType?type=<:string>**

It returns the tabs that are available for the items of the specified type. This endpoint is reserved to system administrators

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the resourcepolicy
* 404 Not found - if the resourcepolicy doesn't exist (or was already deleted)
