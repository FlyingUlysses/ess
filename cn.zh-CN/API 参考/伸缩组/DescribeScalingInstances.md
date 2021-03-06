# DescribeScalingInstances {#concept_25942_zh .concept}

本文介绍查询伸缩组内ECS实例列表API操作。

## 描述 {#section_try_jbk_sfb .section}

查询伸缩组内ECS实例列表。查询时可以指定伸缩组ID、伸缩配置ID、健康状态、生命周期状态、创建类型进行过滤。

-   加入伸缩组的ECS实例有两种类型：自动创建的ECS实例、手工添加的ECS实例。
    -   “自动创建的ECS实例”是指根据用户的伸缩配置和伸缩规则，由弹性伸缩服务自动创建的ECS实例。
    -   “手工添加的ECS实例”是指不是由弹性伸缩服务创建，而是由用户手工添加到伸缩组中的ECS实例。
-   ECS实例在伸缩组中的生命周期，通过以下几种状态描述：
    -   Pending：表示ECS实例正在加入伸缩组，包括创建实例、加入负载均衡、添加RDS访问名单等过程。
    -   InService：表示ECS实例已成功加入伸缩组，并正常提供服务。
    -   Removing：表示ECS实例正在移出伸缩组。
-   ECS实例在伸缩组中的健康状态为：
    -   Healthy：健康
    -   Unhealthy：不健康，本期仅通过ECS实例为非 **运行中**（`Running`）状态来判断该实例不健康
-   弹性伸缩会自动移出伸缩组中不健康的ECS实例。
    -   对于自动创建的ECS实例，弹性伸缩会停止和释放该ECS实例。
    -   对于手工添加的ECS实例，弹性伸缩不会停止和释放该ECS实例。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DescribeScalingInstances。|
|RegionId|String|是|伸缩组所属的地域ID。|
|ScalingGroupId|String|否|伸缩组的ID。|
|ScalingConfigurationId|String|否|关联的伸缩配置ID。|
|InstanceId.N|String|否|ECS实例的ID。最多可以输入20个。返回查询结果时忽略失效的InstanceId，并且不报错。|
|HealthStatus|String|否|ECS实例在伸缩中的健康状态。可选值：-   Healthy：健康的ECS实例。
-   Unhealthy：不健康的ECS实例。

|
|LifecycleState|String|否|ECS实例在伸缩组中的生命周期状态。可选值：-   InService：已成功加入伸缩组并正常运行。
-   Pending：正在加入伸缩组但还未完成相关配置。
-   Removing：正在移出伸缩组。

|
|CreationType|String|否|ECS实例的创建类型。可选值：-   AutoCreated：由弹性伸缩自动在伸缩组中创建。
-   Attached：在弹性伸缩之外创建，并由用户手工加入伸缩组。

|
|PageNumber|Integer|否|ECS实例列表的页码，起始值为1，默认值为1。|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值50行，默认值为10。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|ECS实例总数。|
|PageNumber|Integer|当前页码。|
|PageSize|Integer|每页行数。|
|ScalingInstances|ScalingInstanceSetType|ECS实例信息组成的集合。|

ScalingInstanceSetType是由ScalingInstanceItemType类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|ScalingInstance|ScalingInstanceItemType|ECS实例信息。|

ScalingInstanceItemType类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|ECS实例的ID。|
|ScalingGroupId|String|所属的伸缩组的ID。|
|ScalingConfigurationId|String|关联的伸缩配置ID。|
|HealthStatus|String|在伸缩组中的健康状态。|
|LifecycleState|String|在伸缩组中的生命周期状态。|
|CreationTime|String|加入伸缩组的时间。|
|CreationType|String|ECS实例的创建类型。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DescribeScalingInstances 
&RegionId=cn-qingdao
&ScalingGroupId=dBCYxE26IHKcGq1xPcTNBwV
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeScalingInstancesResponse>
    <RequestId>DFF8797F-5B73-4BD7-A7D0-03479C458F7A</RequestId>
<TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <ScalingInstances>
        <ScalingInstance>
            <CreationTime>2014-08-15T17:37Z</CreationTime>
            <CreationType>AutoCreated</CreationType>
            <HealthStatus>Healthy</HealthStatus>
            <InstanceId>i-283vvyytn</InstanceId>
            <LifecycleState>InService</LifecycleState>         <ScalingConfigurationId>
cGsGHrdMBa3DcDrrBVcc4k2H
</ScalingConfigurationId>
            <ScalingGroupId>dBCYxE26IHKcGq1xPcTNBwV</ScalingGroupId>
        </ScalingInstance>
    </ScalingInstances>
</DescribeScalingInstancesResponse>
```

`JSON` 格式

```
{
  "RequestId": "13305F2D-A4C2-4E6B-B7C7-0F2150842EA3",
"TotalCount": 1,
"PageNumber": 1,
"PageSize": 50,
  "ScalingInstances": {
    "ScalingInstance": [
      {
        "ScalingConfigurationId": "bU5uZHcAgtzwcL4IeDeavqTS",
        "CreationType": "AutoCreated",
        "InstanceId": "i-28sov3exk",
        "CreationTime": "2014-08-14T10:59Z",
        "HealthStatus": "Healthy",
        "LifecycleState": "InService",
        "ScalingGroupId": "dE9YbOdCHqaFdFZHXVdDjQCB"
      }
    ]
  }
}
```

## 错误码 {#section_rk5_pkb_kgb .section}

关于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

