# Layout Box Types
[Layout Box Endpoints](boxes.md)

The following table summarize for each boxType available out-of-box in DSpace-CRIS 7 the data representation returned in the configuration attribute

boxType | data representation
------------ | -------------
metadata | [example](box-metadata.md)
relation | ```json { discovery-configuration: 'the-name-of-the-discovery-configuration'}``` the-name-of-the-discovery-configuration will match a discovery configuration where a facet named "cluster" will be eventually defined  to group the result by arbitrary defined criteria (facet query)
