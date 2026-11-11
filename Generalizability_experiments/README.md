# Generalizability

Data for Section V-E, "Generalizability": three databases, two workloads, and 16 adverse events, with three injection rounds per event and database-workload combination.

## Folders

- `mysql-tpcc/`, `mysql-smallbank/`: MySQL with TPC-C and SmallBank.
- `pg-tpcc/`, `pg-smallbank/`: PostgreSQL with TPC-C and SmallBank.
- `DB-X-tpcc/`, `DB-X-smallbank/`: DB-X with TPC-C and SmallBank.

Each combination contains these event folders; the numeric prefixes preserve the original event identifiers:

```text
01_cpu_saturation                 02_memory_saturation
03_network_packet_loss            04_network_delay
05_packet_reordering              06_packet_duplication
07_packet_corruption              08_disk_full
09_file_move                      10_file_permission_changes
11_process_suspension              12_connection_storm
13_connection_thread_saturation    14_massive_transaction_rollbacks
15_connection_exhaustion           16_process_termination
```

## Files Within Each Event Folder

- `monitor.csv`: timestamped throughput and transaction-latency measurements.
- `faultInject.json`: injection and recovery commands, timing, execution results, and verification records.
- `run-meta.json`: run identifiers and database/workload configuration metadata.
- `metric.json`: computed resilience scores, lifecycle key points, and per-round measurements; `metric.csv`, where present, provides a CSV export.
- `series.json`: environmental monitoring time series.

## Root-Level Score Tables

- `scores_per_round.csv`: individual-round scores and source-record information.
- `scores_per_sequence.csv`: final adaptability, disturbance-period, and deviation scores for each three-round sequence.
- `scores_summary.csv`: per-event eight-dimensional summaries, using round means for the five single-round metrics and final-round values for the three multi-round metrics.
- `scores_by_category.csv`: scores aggregated by event category and database-workload combination, used for the paper's radar charts.
