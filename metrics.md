# Metrics Endpoint
[Back to the list of all defined endpoints](endpoints.md)

## Single Metric
**/api/cris/metrics/<:id>**

Provide detailed information about a specific metrics. The JSON response document is as follow
```json
{
    "id":1,
    "metricType":"view",
    "metricCount":2312.0,
    "acquisitionDate": "2020-12-1",
    "startDate":null,
    "endDate":null,
    "last":true,
    "remark":null,
    "deltaPeriod1":null,
    "deltaPeriod2":null,
    "rank":null,
    "type":"metric",
    "_links":{
        "self":{
            "href":"http://localhost/api/cris/metrics/1"
        }
    }
}
```
Return codes:
* 200 OK - if the operation succeed
* 401 Unauthorized - if you are not authenticated.
* 403 Forbidden - if you are not logged in with sufficient permissions. Only users with ADMIN right and users tha has READ policy on item related to the metric
* 404 Not found - if the metric doesn't exist (or was already deleted)