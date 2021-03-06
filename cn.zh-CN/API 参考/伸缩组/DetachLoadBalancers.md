# DetachLoadBalancers {#concept_85141_zh .concept}

移除一个或多个负载均衡实例。

## 请求参数 {#section_y5n_5dk_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：`DetachLoadBalancers`。|
|ScalingGroupId|String|是|伸缩组 Id。|
|LoadBalancer.N|String|是|负载均衡实例 Id，单次最多支持移除 5 个负载均衡实例。|
|ForceDetach|Boolean|否|是否移除负载均衡实例后端服务器中属于伸缩组的实例： -    `true`：移除
-    `false`：不移除

默认值：`false`。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 Id，由系统生成。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DetachLoadBalancers
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&LoadBalancer.1=lb-2zeur05gfsge6n
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DetachLoadBalancersResponse>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId>
</DetachLoadBalancersResponse>
```

`JSON` 格式

```
{
    "RequestId": "DD0309B7-2613-4792-9B86-275906695253"
}
```

## 错误码 { .section}

对于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|您并未授予弹性伸缩完整的 Open API 调用权限。|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|账号下不存在指定的伸缩组。|
|404|InvalidLoadBalancerId.NotFound|The Load Balancer "%s" does not exist.|伸缩组中不存在指定的负载均衡实例。|

