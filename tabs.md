# Tabs Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**GET /api/layout/tabs**   

Not implemented

## New Tab
**POST /api/layout/tabs**
To create a new Tab perform as POST with the follow JSON:

```json
{
  "shortname": "info",
  "header": "Profile",
  "entityType": "Person",
  "priority": 1,
  "security": 0,
  "type": "tab"
}
```
This endpoint is reserved to system administrators, its returns the created tab.

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions
* 422 UNPROCESSABLE ENTITY - if the json body is unprocessable for CrisLayoutTabRest entity

## Delete tab
**DELETE /api/layout/tabs/<:id>**

Delete a Tab. This endpoint is reserved to system administrators.

Return codes:
* 204 No content - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions
* 404 Not found - if the tab doesn't exist (or was already deleted)

## Single Tab
**GET /api/layout/tabs/<:id>**

Provide detailed information about a specific tab. The JSON response document is as follow

```json
{
  "id": 1,
  "shortname": "info",
  "header": "Profile",
  "entityType": "Person",
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
* 201 Created - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the tab
* 404 Not found - if the tab doesn't exist (or was already deleted)

## Linked entities
### Boxes
**GET /api/layout/tabs/<:id>/boxes**

It returns all the boxes included in the tab. The boxes are sorted by priority ascending. This endpoint is reserved to system administrators

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated. Please note that this also apply to resource policy related to the Anonymous group
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators, users with ADMIN right on the target resource, users mentioned in the policy (eperson or member of the group) can access the resourcepolicy
* 404 Not found - if the tab doesn't exist (or was already deleted)


**GET /api/layout/tabs/<:id>/boxes/<:id>**

_Unsupported._ If you want detailed information about a single box in the tab, use the `/api/layout/boxes/<:box.id>` endpoint.

**POST /api/layout/tabs/<:id>/boxes**

A POST request will result in creating a new mapping between the tab and box.
If the tab and box exist and are related to the same type of entity the relation should be created.

The box(es) MUST be included in the body using the `text/uri-list` content type
 
Return codes:
 * 204 No Content - if the update succeeded (including the case of no-op if the mapping was already as requested)
 * 401 Unauthorized - if you are not authenticated
 * 403 Forbidden - if you are not logged in as administrator 
 * 404 Not found - if the tab doesn't exist (or was already deleted)
 * 422 Unprocessable Entity - if the specified tab and box are related to different entity-types or the box is not found

**PUT /api/layout/tabs/<:id>/boxes**

_Unsupported._ You may replace or update mapped box using DELETE requests and/or POST requests.

**DELETE /api/layout/tabs/<:id>/boxes**

_Unsupported._ At this time, we do not support removing all mapped Boxes in a single request. Please use `DELETE /api/layout/tabs/<:id>/boxes/<:box.id>` to remove mapped boxes one by one.

**DELETE /api/layout/tabs/<:id>/boxes/<:box.id>**

A DELETE request will result in removing an existing mapping between the tab and box.
If the box exists and is included in the tab, the relation should be deleted.

Return codes:
 * 204 if the delete succeeded (including the case of no-op if the box was not mapped) 
 * 401  Unauthorized - if you are not authenticated
 * 403  Forbidden - if you are not logged in as administrator 
 * 422 Unprocessable Entity - if the specified uri cannot resolve to a box (if the uri is valid but the box is not found, 204 is expected)


### SecurityMetadata
**GET /api/layout/tabs/<:id>/securitymetadata**

It returns all the metadatafields that defined the security.

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated.
* 403 Forbidden - if you are not logged in as an administrator
* 404 Not found - if the tab doesn't exist (or was already deleted)

**GET /api/layout/tabs/<:id>/securitymetadata/<:id>**

_Unsupported._ If you want detailed information about a single metadatafield in the tab, use the `/api/core/metadatafields/<:metadatafield.id>` endpoint.

**POST /api/layout/tabs/<:id>/securitymetadata**

A POST request will result in adding the metadatafield to the list of metadata used to evaluate access permission to the tab.

The metadata (also more than one) MUST be included in the body using the `text/uri-list` content type
 
Return codes:
 * 204 No Content - if the update succeeded (including the case of no-op if the mapping was already as requested)
 * 401 Unauthorized - if you are not authenticated
 * 403 Forbidden - if you are not logged in as administrator 
 * 404 Not found - if the tab doesn't exist (or was already deleted)
 * 422 Unprocessable Entity - if the specified metadata is not found

**PUT /api/layout/tabs/<:id>/securitymetadata**

_Unsupported._ You may replace or update the security metadata using DELETE requests and/or POST requests.

**DELETE /api/layout/tabs/<:id>/securitymetadata**

_Unsupported._ At this time, we do not support removing all security metadata in a single request. Please use `DELETE /api/layout/tabs/<:id>/securitymetadata/<:metadatafield.id>` to remove metadatafield one by one.

**DELETE /api/layout/tabs/<:id>/securitymetadata/<:metadatafield.id>**

A DELETE request will result in removing the metadatafield from the current list.

Return codes:
 * 204 No Content if the delete succeeded (including the case of no-op if the metadata was not mapped) 
 * 401 Unauthorized - if you are not authenticated
 * 403 Forbidden - if you are not logged in as administrator
 * 404 Not found - if the tab doesn't exist (or was already deleted)
 * 422 Unprocessable Entity - if the specified uri cannot resolve to a metadatafield (if the uri is valid but the metadatafield is not found, 204 is expected)


## Search methods
### findByItem
**GET /api/layout/tabs/search/findByItem?uuid=<:item-uuid>**

It returns the tabs that are available for the specified item. The tabs are sorted by priority ascending. This are filtered based on the permission of the current user and available data. Empty tabs are filter out.

Return codes:
* 200 OK - if the operation succeed
* 400 Bad Request - if the uuid param is missing or is not an uuid
* 401 Unauthorized - if you are not authenticated and the item is not accessible to anonymous users
* 403 Forbidden - if you are not logged in with sufficient permissions to READ the item


### findByEntityType
**GET /api/layout/tabs/search/findByEntityType?type=<:string>**

It returns the tabs that are available for the items of the specified type. This endpoint is reserved to system administrators

Return codes:
* 200 OK - if the operation succeed
* 400 Bad Request - if the type param is missing
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions
