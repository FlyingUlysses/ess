# ModifyScalingRule {#concept_25949_zh .concept}

This topic describes how to modify a scaling rule using the API.

## Description {#section_xrd_hjk_sfb .section}

Modifies the attributes of a scaling rule.

## Request parameters {#section_xbk_3jk_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface, required. The parameter value is ModifyScalingRule.|
|ScalingRuleId|String|Yes|ID of a scaling rule.|
|AdjustmentType|String|No|Adjustment mode of a scaling rule. Optional values:-   QuantityChangeInCapacity: It is used to increase or decrease a specified number of ECS instances.
-   PercentChangeInCapacity: It is used to increase or decrease a specified proportion of ECS instances.
-   TotalCapacity: It is used to adjust the quantity of ECS instances in the current scaling group to a specified value.

|
|AdjustmentValue|Integer|No|Adjusted value of a scaling rule. The number of ECS instances that are increased or decreased at a time cannot exceed 500. Value range:-   QuantityChangeInCapacity: \[-500, 500\]
-   PercentChangeInCapacity: \[-100, 10000\]
-   TotalCapacity: \[0, 1000\]

|
|ScalingRuleName|String|No|Name shown for the scaling group, which is a string containing 2 to 40 English or Chinese characters. It must begin with a number, a letter \(case-insensitive\) or a Chinese character and can contain numbers, “\_“, “-“ or “.”.The account name in the same scaling group is unique in the same region. If this parameter value is not specified, the default value is ScalingRuleId.

|
|Cooldown|Integer|No|Cool-down time of a scaling rule. Value range: \[0, 86,400\], in seconds. The default value is empty.|

## Response parameters {#section_s1t_4jk_sfb .section}

|Name|Type|Description|
|:---|:---|:----------|
|ScalingRuleId|String|ID of a scaling rule, generated by the system and globally unique.|
|ScalingRuleAri|String|Unique identifier of a scaling rule.|

## Examples {#section_ymk_qjk_sfb .section}

Request example

```
Http://ess.aliyuncs.com /? Action = fig
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<Common Request Parameters>
```

Response example

`XML` format

```
<ModifyScalingRuleResponse>
    <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
    <ScalingRuleId>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleId>
    <RequestId>570C84F4-A434-488A-AFA1-1E3213682B33</RequestId>
</ModifyScalingRuleResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "ScalingRuleId": "eMKWG8SRNb9dBLAjweNI1Ik",
    "ScalingRuleAri":"ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik"
}
```

## Error codes { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error code|Error message|HttpCode|Description|
|:---------|:------------|:-------|:----------|
|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|The specified scaling group does not exist in this account.|
|InvalidScalingRuleName.Duplicate|The specified value of parameter <parameter name\> is duplicated.|400|The scaling rule name already exists.|
|QuotaExceeded.ScalingRule|Scaling rule quota exceeded in the specified scaling group.|400|The user's action quota has been reached.|

