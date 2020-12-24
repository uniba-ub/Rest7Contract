# Box Metrics Configuration

[Back to the list of all defined box types](boxes-types.md)

## Main Endpoint

**/api/layout/boxmetricsconfigurations**

Not Implemented

## Single Box Metrics Configuration

**/api/layout/boxmetricsconfigurations/<:id>**

Provides detailed information about the metrics associated to the box

```json
{
  "id": 1,
  "numColumns": 2,
  "metrics": ["views", "downloads"]
}
```

It provides the configuration for a component that visualize a list of metrics.

## Patch operations

### Add metrics
It is possible to add metrics (overwriting the existent value)
`curl -X PATCH '{dspace7-url}/api/layout/boxmetricsconfigurations/1'
-H "Authorization: Bearer ..." -H 'Content-Type: application/json'
--data '[{"op":"add","path":"/metrics/", "value":["metric3", "metric4"]}]'

that will transform

 ```json
{
  "id": 1,
  "numColumns": 2,
  "metrics": [
    "metric1",
    "metric2"
  ],
  "type": "boxmetricsconfiguration"
}
```
in

```json
{
  "id": 1,
  "numColumns": 2,
  "metrics": [
    "metric3",
    "metric4"
  ],
  "type": "boxmetricsconfiguration"
}
```
Return codes:
* 200 OK if the path operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators can use the endpoint
* 404 Not found - if box doesn't exist (or was already deleted)

### Append metrics
It is possible to append metrics (to the existing ones)
`curl -X PATCH '{dspace7-url}/api/layout/boxmetricsconfigurations/1'
-H "Authorization: Bearer ..." -H 'Content-Type: application/json'
--data '[{"op":"add","path":"/metrics/-", "value":["metric3", "metric4"]}]'
 
that will transform

 ```json
{
  "id": 1,
  "metrics": [
    "metric1",
    "metric2"
  ],
  "type": "boxmetricsconfiguration"
}
```
in

```json
{
  "id": 1,
  "metrics": [
    "metric1",
    "metric2",
    "metric3",
    "metric4"
  ],
  "type": "boxmetricsconfiguration"
}
```

Return codes:
* 200 OK if the path operation succeed
* 401 Unauthorized - if you are not authenticated
* 403 Forbidden - if you are not logged in with sufficient permissions. Only system administrators can use the endpoint
* 404 Not found - if box doesn't exist (or was already deleted)
