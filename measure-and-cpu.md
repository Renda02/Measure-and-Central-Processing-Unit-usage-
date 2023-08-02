# Memory and [CPU](## "Central Processing unit") usage (classic)

## Overview

Learn about the fields and aggregate values Nexthink uses to measure memory usage and processing power. With these values, you can determine how much memory is allocated to a particular device and which applications consume the most resources.

To assess both devices' efficiency and resource consumption's impact on employee experience, your organization must measure the use of hardware resources on each device. When devices are perceived as slow, it is often due to scarcity or misuse of two fundamental system resources: main memory and [CPU](## "Central Processing unit").

## Platform

> Applies to Windows   

## How it works

### Memory usage

[Collector](## "Nexthink Collector is a lightweight software agent designed to gather hardware and software information, monitor system activity, engage with employees for feedback surveys, and act on the device when instructed.") takes samples of the amount of memory used by each running process over 30 seconds. [Collector](## "Nexthink Collector is a lightweight software agent designed to gather hardware and software information, monitor system activity, engage with employees for feedback surveys, and act on the device when instructed.") calculates the average value of these samples over 5-minute intervals to eventually send to the [Engine](## "Nexthink Engine is a server-side application developed for the Nexthink V6 platform, the on-premises Nexhtink solution."). 

<br>

> ####  :information_source: Note
>
> If a process allocates and frees memory very quickly, [Collector](## "Nexthink Collector is a lightweight software agent designed to gather hardware and software information, monitor system activity, engage with employees for feedback surveys, and act on the device when instructed.") may miss some peaks of memory consumption when taking its samples every 30 seconds. 
> Therefore, there is always some uncertainty in the values [Collector](## "Nexthink Collector is a lightweight software agent designed to gather hardware and software information, monitor system activity, engage with employees for feedback surveys, and act on the device when instructed.") offers, but it is usually negligible for well-behaved applications.
> Moreover, memory issues typically arise because of a sustained high consumption of memory rather than because of short-lived allocations.
> 
<br>

The table below lists the fields and aggregates available to measure memory usage.

|Name      | Type | Applies     |Description    |
| :---        |    :----   |          :--- | :---|
| Average memory usage      |field | execution    |   The average memory usage of the execution before being aggregated.  |
|Average memory usage per execution  | aggregate |  user <br>  device <br>  application <br> executable <br> binary  |  The average memory usage of all the underlying executions divided by their cardinality.     |
| Average memory usage (deprecated) | field | binary | The average memory usage of the underlying execution with a sampling rate of 5 minutes. |

### CPU usage

[Collector](## "Nexthink Collector is a lightweight software agent designed to gather hardware and software information, monitor system activity, engage with employees for feedback surveys, and act on the device when instructed.") takes samples of the CPU load of all running processes every 1 minute, with 2 samples taken within each 30-second interval. This data is then aggregated into 5-minute intervals by the aggregation service and further aggregated into 15-minute time buckets.

For execution events, [CPU](## "Central Processing unit") time is reported every 5 minutes after a process is created, with 10 samples taken within each 30-second interval. Collector sends the [CPU](## "Central Processing unit") samples to [Engine](## "Nexthink Engine is a server-side application developed for the Nexthink V6 platform, the on-premises Nexhtink solution.") every 5 minutes.

<br>

> ### :information_source: Note
>
> Since the data is collected at different intervals and processes may terminate during the monitoring period, there may be an overlap between [CPU](## "Central Processing unit") blocks and execution events. 
> 
> Therefore, the last reported information on process termination may only reflect the first 0-5 minutes of the process. <br>


The table below lists the fields and aggregates available to measure memory usage.


|Name      | Type | Applies     |Description    |
| :---        |    :---   |  :--- | :---|
| Total [CPU](## "Central Processing unit") time | field | execution | The effective utilization time of the [CPU](## "Central Processing unit") during the aggregated execution. Note that the total CPU time can exceed the total duration of the execution if the average [CPU](## "Central Processing unit") load is over 100%.|
| Total [CPU](## "Central Processing unit") time | aggregate |  user <br>  device <br>  application <br> executable <br> binary | The sum of the total CPU time of the within the scope of the selected object. |
| CPU usage | field | device | The average memory usage of the underlying execution with a sampling rate of 5 minutes. |
| CPU usage | aggregate | user <br> device <br> application <br> binary | The sum of the total CPU time of the user/device/application/executable/binary divided by their duration. |
| Normalised CPU usage | aggregate | user <br> device <br> application <br> binary | The sum of the total CPU time of the user/device/application/executable/binary divided by their duration and number of logical processors. |

<br>

> ### :information_source: Note
> These figures are based on the samples taken directly from running processes.
> [Collector](## "Nexthink Collector is a lightweight software agent designed to gather hardware and software information, monitor system activity, engage with employees for feedback surveys, and act on the device when instructed.") also takes samples of the total CPU load reported by a device (not broken down by processes), but these are just used to signal [high CPU conditions](https://docs.nexthink.com/platform/latest/errors-and-warnings-for-devices-and-executions) in the device.











