# Setup and dependencies

1. Use Zabbix 7.0 and a Grafana installation supporting the supplied dashboard API v2 format.
2. Configure the Grafana Zabbix plugin and a datasource using your own endpoint and credentials. No credentials are included.
3. Import the Zabbix JSON template and link it to a Linux test host with the base items listed below. The export contains calculated items only; it does not install an agent or link a base template automatically.
4. Confirm calculated items are supported and receiving values.
5. Import the dashboard JSON files into a separate test folder. Choose your datasource in the Zabbix Server selector, then choose hosts.
6. Confirm panels resolve the expected item names, units and values. Import behavior has not been tested here; if the export format is rejected, re-export the original dashboard in a format supported by the destination version.

## Required base keys

- `system.cpu.util`
- `vm.memory.utilization`
- `vfs.fs.size[/,used]`
- `vfs.fs.size[/,pused]`

These exact keys must exist on each host using the capacity template. Dependent filesystem keys from another base template are not interchangeable without editing formulas. The capacity template has no discovery rules and only forecasts the root filesystem.

The dashboards also query base items by their displayed English names, including Number of CPUs, Total memory and filesystem utilization/total space. Match names and component tags to your templates. Keep sufficient raw history for the 30-day forecast/timeleft calculations and trend data for both weekly comparison windows.

Grafana alert rules are separate from Zabbix triggers and must be configured independently for the overview alert list.

Do not import into production as part of portfolio preparation. Validate in a test environment first.
