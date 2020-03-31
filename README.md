# webservices-statistics
A description and explanation for users on how the E-Series Web Services statistics API's work

## Overview

There are multiple API's in Web Services that allow you to retrieve statistics. The most common of these are the analysed-statistics API's. There are also API's that allow you to retrieve the raw statistics from which we generate the analysed statistics. Most will find the analysed statistics are what they're looking for, as they give throughput, IOps, and latency calculations rather than linear counters.

### Statistics Types

E-Series can provide new statistics every 5 seconds, but that places additional load on not only the E-Series device (which it's more than capable of handling, provided many clients aren't requesting), but it also generates huge amounts of statistics data. Therefore, most clients will only request statistics data once a minute or more. 

### Polling Interval
The analysed statistics are based on the raw counters that the E-Series system provides and we aggregate these values into a rolling window that updates every N seconds. By default, the Web Services Proxy will update statistics every 60 seconds, but this value can be set as low as 5s, or higher if desired. You can request statistics more often, but you'll only get duplicate values and the same timestamp, so you should set your polling interval accordingly.

## Integrations and Recommendations
Time-series databases are the most common way that metrics like this are tracked; examples include Graphite, InfluxDB, and Prometheus. E-Series has a project that is available on [GitHub](https://github.com/NetApp/eseries-perf-analyzer) that uses Grafana and InfluxDB to present many of the metrics we make available in pre-built dashboards.

## FAQ and Troubleshooting

### Why do I see fewer cores than I would expect for CPU statistics?
On some systems the E-Series will hide certain cores from the controller firmware for other uses. When this happens, the statistics that are generated in CFW will not show these cores in the statistics because they are unavailable. In this context, it can be assumed that load on this core will not impact performance.
