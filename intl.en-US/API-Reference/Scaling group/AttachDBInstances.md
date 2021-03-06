# AttachDBInstances {#concept_85379_zh .concept}

You can call this operation to add one or more RDS instances.

## Description {#section_upc_k2k_sfb .section}

Due to restrictions, the following conditions must be met when you add RDS instances to a scaling group.

-   The SLB instance and the scaling group must be in the same account.
-   The status of the RDS instance must be **Unlocked**. For more information, see [RDS usage instructions](../../../../../reseller.en-US/Product Introduction/RDS usage instructions.md#).
-   The status of the RDS instance must be **Running**.
-   After you add an RDS instance, the number of IP addresses included in the default group of the IP whitelist for an RDS instance cannot exceed 1,000. For more information about an IP whitelist, see [Set the whitelist](../../../../../reseller.en-US/User Guide/Security/Set the whitelist.md#).

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to `AttachDBInstances`.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|
|DBInstance.N|String|Yes|The ID of the RDS instance. You can add up to five RDS instances at one time.|
|ForceAttach|Boolean|No|Indicates whether to add all private IP addresses of instances in the scaling group to the IP whitelist of the RDS instance. -    `true`: adds all private IP addresses.
-    `false`: does not add all private IP addresses.

Default value: `false`.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The GUID generated by Alibaba Cloud for the request.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=AttachDBInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&DBInstance. 1=rm-bp12cy39261
& <Common request parameters>
```

Successful response examples

`XML` format

```
<AttachDBInstancesResponse>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId>
</AttachDBInstancesResponse>
```

`JSON` format

```
{
    "RequestId": "DD0309B7-2613-4792-9B86-275906695253"
}
```

## Error codes { .section}

For more information about common errors, see [Client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [Server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|HttpCode|Error code|Error message|Description|
|--------|:---------|:------------|:----------|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist in your account.|
|400|QuotaExceeded.RDS|"RDS" quota exceeded.|The error message returned when the number of RDS instances in the scaling group exceeds the quota.|
|400|InvalidDBInstanceId.NotFound|The specified value of parameter "%s" is not valid.|The error message returned when the specified RDS instance does not exist.|
|400|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|The specified action failed due to the current status of the instance.|
|400|QuotaExceeded.DBInstanceSecurityIP|Security IP quota exceeded in DB instance “XXX”.|The error message returned when the number of backend IP addresses in the whitelist of the RDS instance exceeds the quota.|
|400|InvalidInstanceIds.PrivateIpNotFound|Can not find all private ips of instances in specific scaling group.|The error message returned when failing to obtain the private IP address of the RDS instance in the scaling group.|

