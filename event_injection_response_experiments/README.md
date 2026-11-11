# Event Injection and Service Response

Data and plots for Section V-B, "Adverse-Event Injection and Service Response," using MySQL with TPC-C. Each event folder includes:

- `faultInject.json`: injection and recovery commands, execution results, timing, and verification records.
- `monitor.csv`: timestamped workload throughput and transaction-latency measurements.
- `run-meta.json`: database, workload, run, and configuration metadata.
- `series.json`: time-series measurements collected from the database environment.
- `triangle_*.pdf`: the throughput plot for the corresponding event.

Event folders: `connection_exhaustion`, `cpu_saturation`, `disk_full`, `memory_saturation`, `network_delay`, and `process_suspension`.
