# WorkspaceItem data of custom url sectionType
[Back to the definition of the workspaceitems endpoint](workspaceitems.md)

This section data represent the data about the item's custom url

```json
{
  "url": "john-smith",
  "redirected-urls": [
    "smith-john",
    "john"
  ]
}
```

* url: the custom defined URL for the related item
* redirected-urls: the older values of the custom defined URL

## Patch operations
The PATCH method expects a JSON body according to the [JSON Patch specification RFC6902](https://tools.ietf.org/html/rfc6902)

Each successful Patch operation will return a HTTP 200 CODE with the new workspaceitem as body. See also the [General rules for the Patch operation](patch.md) for more details.

### Replace url

To set an url the client must send a JSON Patch REPLACE operation as follow

`curl --data '{[ { "op": "replace", "path": "/sections/<:name-of-the-form>/url", "value": "<new-url>"}]}' -X PATCH ${dspace7-url}/api/submission/workspaceitems/<:id>`

If the new value is equals to the previous one, no operation is performed.

If the new value is equals to one of the redirected urls, that url is removed from the list; the previously configured url is added to the redirected url list.

### Add redirected-url
It is possible to add an redirected custom url as follow
`curl --data '{[ { "op": "remove", "path": "/sections/<:name-of-the-form>/redirected-urls", "value": "<redirected-url>"}]' -X PATCH ${dspace7-url}/api/submission/workspaceitems/<:id>`

### Remove redirected-url
It is possible to remove an old custom defined url as follow
`curl --data '{[ { "op": "remove", "path": "/sections/<:name-of-the-form>/redirected-urls/<:index>"}]' -X PATCH ${dspace7-url}/api/submission/workspaceitems/<:id>`

## Section errors

Based on the data set in the section, there may be the following errors in the resulting workspace item:

* **empty url**: message error.validation.custom-url.empty and path /sections/<:step-id>/url
* **url with invalid characters**: message error.validation.custom-url.invalid-characters and path /sections/<:step-id>/url
* **already used url**: message error.validation.custom-url.conflict and path /sections/<:step-id>/url