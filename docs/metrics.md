# Calculated metrics

Formulas preserved from the supplied Zabbix export.

## CPU - 7 days average

`capacity.cpu.avg.7d` — exported unit: `%`

```text
avg(//system.cpu.util,7d)
```

## CPU - Forecast 30 days

`capacity.cpu.forecast.30d` — exported unit: `%`

```text
forecast(//system.cpu.util,30d,30d)
```

## CPU - Weekly peak change

`capacity.cpu.peak.weekly.change` — exported unit: `%`

```text
trendmax(//system.cpu.util,7d:now/d)
-
trendmax(//system.cpu.util,7d:now/d-7d)
```

## CPU - Peak 7d

`capacity.cpu.peak7d` — exported unit: `%`

```text
max(//system.cpu.util,7d)
```

## CPU - Peak 24h

`capacity.cpu.peak24h` — exported unit: `%`

```text
max(//system.cpu.util,1d)
```

## CPU - Weekly change

`capacity.cpu.weekly.change` — exported unit: `%`

```text
trendavg(//system.cpu.util,7d:now/d)
-
trendavg(//system.cpu.util,7d:now/d-7d)
```

## / - Growth daily

`capacity.fs.growth.c` — exported unit: `B`

```text
(
trendavg(//vfs.fs.size[/,used],1d:now/d)
-
trendavg(//vfs.fs.size[/,used],1d:now/d-7d)
)
/7
```

## Memory - Forecast 30 days

`capacity.memory.forecast.30d` — exported unit: `%`

```text
forecast(//vm.memory.utilization,30d,30d)
```

## Memory - Time until 90%

`capacity.memory.timeleft.90` — exported unit: `s`

```text
timeleft(//vm.memory.utilization,30d,90)
```

## Memory - Weekly change

`capacity.memory.weekly.change` — exported unit: `%`

```text
trendavg(//vm.memory.utilization,7d:now/d)
-
trendavg(//vm.memory.utilization,7d:now/d-7d)
```

## / - Forecast 30 days

`capacity.root.forecast.30d` — exported unit: `%`

```text
forecast(//vfs.fs.size[/,pused],30d,30d)
```

## / - Time until 90%

`capacity.root.timeleft.90` — exported unit: `s`

```text
timeleft(//vfs.fs.size[/,pused],30d,90)
```

## / - Weekly change

`capacity.root.weekly.change` — exported unit: `%`

```text
trendavg(//vfs.fs.size[/,pused],7d:now/d)
-
trendavg(//vfs.fs.size[/,pused],7d:now/d-7d)
```

## Interpretation

Weekly utilization changes are differences in percentage points, not relative percentage growth. Disk daily growth compares daily averages seven days apart and divides their difference by seven; interpret it as average bytes per day. Forecast and timeleft use 30 days of raw item history. Timeleft returns seconds; special/error results must not be treated as ordinary countdowns.

Reference: https://www.zabbix.com/documentation/7.0/en/manual/appendix/functions/prediction
