# Knowledge-Graph Experiment Data

Data for Section V-D, "Contributions of the Adverse-Event Knowledge Graph"

## Directory Layout

- input_plans_n300/
  - plan_000001/ through plan_000300/
    - config.xml
    - schedule.xml
- offline_kg_ablation/
  - constraint_feasibility_n300/
    - full_kg/
    - without_dependency/
    - without_mutual_exclusion/
  - interaction_detection_on_admitted_plans_n184/
    - full_kg/
    - without_enhancement/
    - without_masking/
- online_validation/
  - kg_admitted_runs_n184/
    - injection_completed_n175/
    - injection_failed_n9/
  - interaction_candidates_n64/
    - confirmed_enhancement_n35/
    - confirmed_masking_n13/
    - no_clear_interaction_effect_n15/
    - injection_failed_n1/
- interaction_case_studies/
  - plan_000037/
  - plan_000108/

## Input Plans

Each input plan folder, plan_XXXXXX, contains exactly two files:

| File | Contents |
|---|---|
| config.xml | Database and workload configuration: DBMS type and driver, connection URL, nodes, username/password fields, isolation, batch size, scale factor, terminals, fault-case declarations, and transaction types. |
| schedule.xml | Test-suite schedule, including adverse-event injection ordering and timing. |

## Offline KG Ablation

Each configuration directory contains summary.csv, check_details.csv, and per_plan_reports/. Each per-plan directory contains result.json and console.log. The interaction-detection configurations also contain potential_interaction_plans.csv.

### Constraint Feasibility

Each variant checks 300 plans. The paper-level admitted count is PASS_CHECKED_CONSTRAINTS plus NO_APPLICABLE_RULES. VIOLATION plans are rejected.

| Configuration | PASS_CHECKED_CONSTRAINTS | NO_APPLICABLE_RULES | Admitted | VIOLATION |
|---|---:|---:|---:|---:|
| full_kg | 118 | 66 | 184 | 116 |
| without_dependency | 139 | 94 | 233 | 67 |
| without_mutual_exclusion | 156 | 85 | 241 | 59 |

### Interaction Detection

Each variant evaluates the same 184 KG-admitted plan IDs.

| Configuration | Evaluated plans | Enhancement matched / confirmed | Masking matched / confirmed |
|---|---:|---:|---:|
| full_kg | 184 | 51 / 35 | 28 / 13 |
| without_enhancement | 184 | 0 / 0 | 28 / 13 |
| without_masking | 184 | 51 / 35 | 0 / 0 |

Potential-enhancement and potential-masking candidates can overlap.

### Offline Files

| File | Contents |
|---|---|
| summary.csv | Per-configuration aggregate counts in the paper-facing schema. |
| check_details.csv | One row per plan: sample ID, status, event count, errors, warnings, pending checks, interaction count, unknown count, and report path. |
| potential_interaction_plans.csv | Plan ID, status, potential-enhancement/masking flags, corresponding pair counts, and report path. Present only in interaction-detection variants. |
| per_plan_reports/plan_XXXXXX/result.json | Machine-readable plan-level check result: graph version, relation mode, status, cases, diagnostics, active interactions, coverage, summary counts, and input provenance. |
| per_plan_reports/plan_XXXXXX/console.log | Text output for the corresponding plan check, including progress and diagnostics. |

## Online Validation

kg_admitted_runs_n184 contains 184 plan folders: 175 injection-completed runs and 9 injection failures.

interaction_candidates_n64 contains 64 categorized folders: 35 online-confirmed enhancement cases, 13 online-confirmed masking cases, 15 with no clear interaction effect, and 1 injection failure. They are organized by outcome and are not 64 additional independent executions.

Every online plan folder contains the following five top-level files and two files under monitoring/:

| File | Contents |
|---|---|
| config.xml | Effective database, workload, and fault-test configuration saved for the run. |
| monitor.csv | Time-series TPS and latency summaries: timestamp, TPS, average/max/min latency, and 5th/95th-percentile latency. |
| raw.csv | Transaction-level measurements: transaction type/name, start time, latency, worker, phase, and success flag. |
| run-meta.json | Run identity and metadata, workload/database settings, fault declarations, run options, and timestamps. |
| summary.json | Aggregate benchmark metadata/results, including DBMS/test suite, final state, measured requests, transaction settings, latency distribution, throughput, and goodput. |
| monitoring/series.json | Archived resource/database monitoring series with metric/target labels, units, timestamps and values, and collection warnings. |
| monitoring/session.json | Monitoring session status, targets/metrics, sampling interval, test window, data completeness, and warnings. |

## Case Studies

interaction_case_studies/plan_000037/ contains the mutual-exclusion case. It has the online run file set above plus plan37_mutex_figure.pdf.

interaction_case_studies/plan_000108/ contains the masking case. It has the online run file set above plus plan108_masking_figure.pdf.

The PDFs are the rendered figures. The CSV and monitoring files in the same folder retain the corresponding performance and resource observations.
