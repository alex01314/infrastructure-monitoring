# Preparation changes and validation

- Removed original Grafana resource metadata, user identifiers, selected host names and selected datasource values.
- Replaced fixed Zabbix datasource references with `${zabbix}` and added a datasource selector to the Linux dashboard.
- Renamed the overview and capacity dashboards for the portfolio.
- Corrected the panel querying Total memory from Memory - Weekly change to Total Memory.
- Corrected `capacity.memory.timeleft.90` units from `d` to `s`; the formula returns seconds. This change is only in the portfolio copy.
- Preserved template/item UUIDs, keys and formulas for compatibility. The root growth key retains its original `.c` suffix.

Validation: all generated JSON files parse successfully; calculated-item names used by the Linux dashboard are present in the supplied template. Base items require an additional host template. No import or live datasource tests were performed.

Review timeleft table thresholds before operational use: inherited coloring is not a validated capacity warning policy.
