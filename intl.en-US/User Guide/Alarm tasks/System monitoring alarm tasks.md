# System monitoring alarm tasks {#concept_74854_zh .concept}

This topic introduces system monitoring alarm tasks.

Metrics in system monitoring alarm tasks are monitoring data collected from ECS instances by CloudMonitor. ECS instances are monitored at the scaling group level, meaning that the measurement of a certain metric in a scaling group is the average value of the metric measurements for all ECS instances in a scaling group. When the number of ECS instances in the scaling group changes, the metrics are also updated accordingly.

## Supported metrics {#section_vmc_dbd_sfb .section}

The following table lists the metrics supported by system monitoring alarm tasks.

|Metric|Unit|Applicable network|
|:-----|:---|:-----------------|
|CPU|%|Classic network and VPC|
|Memory|%|Classic network and VPC|
|Average system load|None|Classic network and VPC|
|Internal network outbound traffic|KB/min|Classic network and VPC|
|Internal network inbound traffic|KB/min|Classic network and VPC|
|Total TCP connections|N/A|Classic network and VPC|
|Established TCP connections|N/A|Classic network and VPC|
|System disk reads measured in bit/s|Bit/s|Classic network and VPC|
|System disk writes measured in bit/s|Bit/s|Classic network and VPC|
|System disk read IOPS|Times/s|Classic network and VPC|
|System disk write IOPS|Times/s|Classic network and VPC|
|Packets sent by internal network NICs|Packets/s|Classic network and VPC|
|Packets received by internal network NICs|Packets/s|Classic network and VPC|
|External network outbound traffic|KB/min|Classic network and VPC|
|External network inbound traffic|KB/min|Classic network and VPC|
|Packets sent by external network NICs|Packets/s|Classic network|
|Packets received by external network NICs|Packets/s|Classic network|

## Notes { .section}

-   A scaling group can only execute one scaling activity at a time. When a scaling activity is being executed, the scaling group rejects all other scaling activities generated by scaling rules triggered by alarm tasks.
-   The cooldown period of a scaling rule affects how the rule is triggered by Auto Scaling alarm tasks. When the cooldown period of a rule has not yet expired, Auto Scaling will not execute that rule. After ECS instances have been added to a scaling group, the systems of the instances are started, configured, and have businesses deployed on them. This process takes several minutes, during which monitoring data for the instances is not recorded. Because of this, you must set an appropriate cooldown period based on your specific business to prevent scaling rules from being triggered repeatedly.
-   Each Auto Scaling alarm task has a default cooldown period of one minute and scaling rules cannot be re-triggered during this period.
-   You must install the CloudMonitor client to collect system metrics such as memory, load, the number of packets sent by NICs, and the number of TCP connections. When you need to set an alarm task for metrics collected by the CloudMonitor client, the client is automatically installed on all instances belonging to the scaling group associated with the alarm task. At the same time, `CloudMonitor auto installation for newly purchased ECS instances` is automatically enabled on the CloudMonitor console so that the client will also be installed on newly purchased ECS instances.
