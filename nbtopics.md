## Main Endpoint
**GET /api/integration/nbtopics**
​
Provide access to the OpenAIRE Broker topics. It returns the list of the OpenAIRE Broker topics.
​
```json
[
  {
    id: "ENRICH!MORE!PID",
    type: "openaireBrokerTopic",
    name: "ENRICH/MORE/PID",
    lastEvent: "2020/10/09 10:11 UTC",
    totalSuggestions: 33
  },
  {
    id: "ENRICH!MISSING!ABSTRACT",
    type: "openaireBrokerTopic",
    name: "ENRICH/MISSING/ABSTRACT",
    lastEvent: "2020/10/09 10:11 UTC",
    totalSuggestions: 21
  },
  ...
]
```
Attributes:
* name: the name of the topic to display on the frontend user interface
* lastEvent: the date of the last udate from OpenAIRE
* totalSuggestions: the total number of suggestions provided by OpenAIRE for this topic
* id: is the idenfier to use in GET Single Topic

Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions, only system administrators can access
​

## GET Single Topic
**GET /api/integration/nbtopics/<:id_topic>**
​
Provide detailed information about a specific OpenAIRE Broker topic. The JSON response document is as follow
​
```json
{
  id: "ENRICH!MORE!PID",
  type: "openaireBrokerTopic",
  name: "ENRICH/MORE/PID",
  lastEvent: "2020/10/09 10:11 UTC",
  totalSuggestions: 33
}
```
​
Attributes:
* name: the name of the topic to display on the frontend user interface
* lastEvent: the date of the last udate from OpenAIRE
* totalSuggestions: the total number of suggestions provided by OpenAIRE for this topic
​
Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions, only system administrators can access
* 404 Not found - if the topic doesn't exist
