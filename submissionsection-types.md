# Submission Section Types
[Submission-Sections Endpoints](submissionsections.md)

The following table summarize for each sectionType available out-of-box in DSpace 7 the endpoint used to retrieve the extra configuration where needed and the link to the documentation about the data representation returned in the workspaceitem

sectionType | configuration endpoint | data representation
------------ | ------------- | -------------
collection | n/a | ```json { collection: 'uuid-of-the-collection'}```
submission-form | [/config/submissionforms](submissionforms.md) | [example](workspaceitem-data-metadata.md)
upload | [/config/submissionuploads](submissionuploads.md) | [example](workspaceitem-data-upload.md)
license | [it is retrieved from the collection following the *license* link](collections.md#License) | [example](workspaceitem-data-license.md)
cclicense | [/config/submissioncclicenses](submissioncclicenses.md) | [example](workspaceitem-data-cclicense.md)
custom-url | n/a | [example](workspaceitem-data-custom-url.md)
access | [/config/submissionaccessoptions](submissionaccessoptions.md) | [example](workspaceitem-data-access.md)
detect-duplicate|t.b.d | [example](workspaceitem-data-detect-duplicate.md)
sherpaPolicies | n/a | [example](workspaceitem-data-sherpa-policy.md)
identifiers | n/a | [example](workspaceitem-data-identifiers.md)

n/a --> not applicable. The sectionType doesn't require/support any extra configuration
t.b.d. --> to be defined. We still need to discuss that
