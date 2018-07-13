InitializeFrom function allows you to create new records in the context of an existing record where a mapping exists between the entities to which the records belong. 

## Example

**Request**

```HTTP
GET [Organization URI]/api/data/v9.0/InitializeFrom(EntityMoniker=@p1,TargetEntityName=@p2,TargetFieldType=@p3)?@p1={'@odata.id':'accounts(c65127ed-2097-e711-80eb-00155db75426)'}&@p2='account'&@p3=Microsoft.Dynamics.CRM.TargetFieldType'ValidForCreate' HTTP/1.1
If-None-Match: null
OData-Version: 4.0
OData-MaxVersion: 4.0
Content-Type: application/json
Accept: application/json
```

**Response**

```JSON
{
        "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts/$entity",
        "@odata.type": "#Microsoft.Dynamics.CRM.account",
        "parentaccountid@odata.bind": "accounts(c65127ed-2097-e711-80eb-00155db75426)",
        "transactioncurrencyid@odata.bind": "transactioncurrencies(732e87e1-1d96-e711-80e4-00155db75426)",
        "address1_line1":"123 Maple St.",
        "address1_city":"Seattle",
        "address1_country":"United States of America"
}
```

The response received from InitializeFrom request consists of values of mapped attributes between the source entity and target entity and the GUID of parent record. The attribute mapping between entities that have an entity relationship is different for different entity sets and is customizable, so the response from InitializeFrom function request may vary for different entities and organizations. When this response is passed in the body of create request of the new record, these attribute values are replicated in the new record. The values of custom mapped attributes also get set in the new record during the process.

> NOTE
> To determine whether two entities can be mapped, use this query:  
> GET [Organization URI]/api/data/v9.0/entitymaps?$select=sourceentityname,targetentityname&$orderby=sourceentityname

Other attribute values can also be set and/or modified for the new record by adding them in the JSON request body, as shown in the example below.

```JSON
{
        "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts/$entity",
        "@odata.type": "#Microsoft.Dynamics.CRM.account",
        "parentaccountid@odata.bind": "accounts(c65127ed-2097-e711-80eb-00155db75426)",
        "transactioncurrencyid@odata.bind": "transactioncurrencies(732e87e1-1d96-e711-80e4-00155db75426)",
        "name":"Contoso Ltd",
        "numberofemployees":"200",
        "address1_line1":"100 Maple St.",
        "address1_city":"Seattle",
        "address1_country":"United States of America",
        "fax":"73737"
}
```
