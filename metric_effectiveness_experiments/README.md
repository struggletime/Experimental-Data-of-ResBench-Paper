# Metric Effectiveness

Results for Section V-C, "Effectiveness of the Eight-Dimensional Evaluation System," using the same six events as Section V-B.

- `cpu_saturation/`, `memory_saturation/`, `network_delay/`, `disk_full/`, `connection_exhaustion/` and `process_suspension/`: per-event metric results (`*.json`) and multi-round score plots (`multi_*.pdf`).
- `single_round_heatmap.pdf`: heatmap of the single-round metric scores across the six events.

The JSON files contain computed metric values and event/run timing information; the PDFs visualize the corresponding scores.

Source performance traces and injection records are provided in the sibling directory `event_injection_response_experiments/`.
