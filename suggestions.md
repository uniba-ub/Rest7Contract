## Main Endpoint
**GET /api/integration/suggestions**

Provide paginated list of suggestions for the specified topic. A sample response is:

```json
[
  {
    "id":"123e4567-e89b-12d3-a456-426614174000",
    "original_id": "oai:www.openstarts.units.it:10077/21486",
    "title":"Index nominum et rerum",
    "topic":"ENRICH/MORE/OPENACCESS_VERSION",
    "trust":"0.375",
    "message" : {
      "type":"doi",
      "value":"10.18848/1447-9494/cgp/v15i09/45934",
      "abstracts":"Abstract Complex functionality of the ...",
      "acronym":"EPSILON",
      "code":"277749",
      "funder":"EC",
      "fundingProgram":"FP7",
      "jurisdiction":"EU",
      "title":"Elliptic Pdes and Symmetry of Interfaces and Layers for Odd Nonlinearities"
    }
  }
]
```

This is a full filled Json example. This situation never happen, because the message fields filled change based on "topic" type:
* ENRICH/MISSING/PID and ENRICH/MORE/PID: fills `message.type` and `message.value`
* ENRICH/MISSING/ABSTRACT: fills `message.abstract`
* ENRICH/MISSING/SUBJECT/ACM: fills `message.type` and `message.value`
* ENRICH/MISSING/PROJECT: fills `acronym`, `code`, `funder`, `fundingProgram`, `jurisdiction` and `title`

## GET Single suggestion
** GET /api/integration/suggestions/<:id_suggestion>

Return a single suggestion:
```json
{
  "id":"123e4567-e89b-12d3-a456-426614174000",
  "original_id": "oai:www.openstarts.units.it:10077/21486",
  "title":"Index nominum et rerum",
  "topic":"ENRICH/MORE/OPENACCESS_VERSION",
  "trust":"0.375",
  "message" : {
    "type":"doi",
    "value":"10.18848/1447-9494/cgp/v15i09/45934",
    "abstracts":"Abstract Complex functionality of the ...",
    "acronym":"EPSILON",
    "code":"277749",
    "funder":"EC",
    "fundingProgram":"FP7",
    "jurisdiction":"EU",
    "title":"Elliptic Pdes and Symmetry of Interfaces and Layers for Odd Nonlinearities"
  }
}
```

## POST Suggestion
POST /api/integration/suggestions/<:id_suggestion>

This method allow users to Accept, Reject or Discard a suggestion. The post body must contains the action:

```json
{
  "action":"{ACCEPT|REJECT|DISCARD}"
}
```

As response, the discarded suggestion will be returned:

```json
{
  "id":"123e4567-e89b-12d3-a456-426614174000",
  "original_id": "oai:www.openstarts.units.it:10077/21486",
  "title":"Index nominum et rerum",
  "topic":"ENRICH/MORE/OPENACCESS_VERSION",
  "trust":"0.375",
  "message" : {
    "type":"doi",
    "value":"10.18848/1447-9494/cgp/v15i09/45934",
    "abstracts":"Abstract Complex functionality of the ...",
    "acronym":"EPSILON",
    "code":"277749",
    "funder":"EC",
    "fundingProgram":"FP7",
    "jurisdiction":"EU",
    "title":"Elliptic Pdes and Symmetry of Interfaces and Layers for Odd Nonlinearities"
  }
}
```
 
