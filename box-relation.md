# Box Metadata Configuration

[Back to the list of all defined box types](boxes-types.md)

## Main Endpoint

**/api/layout/boxrelationconfigurations**

Not Implemented

## Single Box Relation Configuration

**/api/layout/boxrelationonfigurations/<:id>**

Provides detailed information about the relation included in the box

```json
{
  "id": 1,
  "discovery-configuration": "the-name-of-the-discovery-configuration"
}
```

the-name-of-the-discovery-configuration will match a discovery configuration where a facet named "cluster" 
will be eventually defined  to group the result by arbitrary defined criteria (facet query)