# Memory and CPU usage (classic)

## Overview

Learn about the fields and aggregate values Nexthink uses to measure memory usage and processing power. With these values, you can determine how much memory is allocated to a particular device and which applications consume the most resources.

To assess both devices' efficiency and resource consumption's impact on employee experience, your organization must measure the use of hardware resources on each device. When devices are perceived as slow, it is often due to scarcity or misuse of two fundamental system resources: main memory and central processing unit (CPU) power.

## Platform

Applies to Windows

## How it works

### Memory usage

Collector takes samples of the amount of memory used by each running process over 30 seconds. Collector calculates the average value of these samples over 5-minute intervals to eventually send to the Engine. 

> 
> #### Note
>
> If a process allocates and frees memory very quickly, Collector may miss some peaks of memory consumption when taking its samples every 30 seconds. 
> Therefore, there is always some uncertainty in the values Collector offers, but it is usually negligible for well-behaved applications.
> Moreover, memory issues typically arise because of a sustained high consumption of memory rather than because of short-lived allocations.
> <br>

The table below lists the fields and aggregates available to measure memory usage.

|Name      | Type | Applies     |Description    |
| :---        |    :----   |          :--- | :---|
| Average memory usage      |field | execution    |   The average memory usage of the execution before being aggregated.  |
|Average memory usage per execution  | aggregate |  user <br>  device <br>  application <br> executable <br> binary  |  The average memory usage of all the underlying executions divided by their cardinality.     |
| Average memory usage (deprecated) | field | binary | The average memory usage of the underlying execution with a sampling rate of 5 minutes. |

CPU usage

Collector takes samples of the CPU load of all running processes every 1 minute, with 2 samples taken within each 30-second interval. This data is then aggregated into 5-minute intervals by the aggregation service and further aggregated into 15-minute time buckets.

For execution events, CPU time is reported every 5 minutes after a process is created, with 10 samples taken within each 30-second interval. Collector sends the CPU samples to Engine every 5 minutes.

>
> ### Note
>
> Since the data is collected at different intervals and processes may terminate during the monitoring period, there may be an overlap between CPU blocks and execution events. 
> 
> Therefore, the last reported information on process termination may only reflect the first 0-5 minutes of the process. <br>


The table below lists the fields and aggregates available to measure memory usage.


|Name      | Type | Applies     |Description    |
| :---        |    :----   |          :--- | :---|
| Total CPU time | field | execution | The effective utilization time of the CPU during the aggregated execution. Note that the total CPU time can exceed the total duration of the execution if the average CPU load is over 100%.|
| Total CPU time | aggregate |  user <br>  device <br>  application <br> executable <br> binary | The sum of the total CPU time of the within the scope of the selected object. |
| CPU usage | field | device | The average memory usage of the underlying execution with a sampling rate of 5 minutes. |

> ### Note
> These figures are based on the samples taken directly from running processes.
> Collector also takes samples of the total CPU load reported by a device (not broken down by processes), but these are just used to signal high CPU conditions in the device











