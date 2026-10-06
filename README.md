# Infrastructure Monitoring and Capacity Planning

Monitoring combining Zabbix metrics with Grafana dashboards for infrastructure visibility and capacity planning.

## Included

- Infrastructure overview: CPU, memory, root filesystem / Windows C: utilization, agent and alert panels.
- Linux capacity dashboard: 30-day forecasts, weekly changes, CPU peaks and estimated time to 90% utilization.
- Zabbix 7.0 template with 13 calculated items, updated hourly.
- Configurable Zabbix datasource and host selectors.

## Files

- `dashboards/infrastructure-overview.json`
- `dashboards/capacity-forecast-linux.json`
- `zabbix/templates/capacity-forecast-linux.json`
- [Setup and dependencies](docs/setup.md)
- [Calculated metrics](docs/metrics.md)
- [Changes and validation](docs/changes.md)

## Architecture

Linux / Windows agents provide infrastructure metrics to Zabbix. Grafana queries Zabbix through the `alexanderzobnin-zabbix-datasource` plugin. Capacity calculations run in Zabbix; Grafana presents their results.

## Status

Prepared from dashboard and template exports. JSON parsing and dependency inspection completed; import and runtime validation in a separate environment are still pending. Exports use Grafana dashboard API v2 and reference Grafana 13.0.1 visualization versions; compatibility with older releases is not established.

Windows capacity templates, UptimeRobot integration and sanitized screenshots will be added when their files are available. The overview alert-list panel requires Grafana alert rules, which are not included in dashboard exports.

Forecasts are estimates based on historical behavior, not guarantees. Weekly utilization differences represent percentage points. Missing history, workload changes and unreachable thresholds require interpretation.
