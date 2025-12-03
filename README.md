# SerialED stream post-processing workflow

This repository contains a small set of custom scripts used in SerialED/CrystFEL-style stream-file post-processing:
1) (Optional) orientation-based frame exclusion (Jupyter notebook).
2) Stream-file filtering by an indexing quality metric (IQM-like composite score) to retain the best solution per event.
3) Helper scripts to convert filtered stream files into `.sol` and generate integration bash commands.

## Contents

### IQM stream filtering (`src/iqm_stream_filtering/`)
- `gen_lowest_iqm_stream.py`: ranks indexed chunks within `.stream` files using a weighted multiplicative composite score of normalized metrics, and writes:
  - `combined_metrics_IQM_<weights>.csv`
  - `best_results_IQM_<weights>.stream`
- `extract_chunk_data.py`: parses chunks and extracts per-chunk metrics; calls:
  - `calculate_weighted_rmsd.py`
  - `calculate_cell_deviation.py`

### Integration helpers (`src/integration_helpers/`)
- `read_stream_write_sol_gen_bash.py`: reads a stream file, writes a `.sol`, and triggers bash generation.
- `generate_bash_script.py`: generates an `indexamajig` integration command file.

### Orientation filtering (`src/orientation_filtering/`)
- `extract-missindexed-orientation.ipynb`: optional notebook used to remove frames with specified (problematic) refined crystal orientations prior to IQM filtering.

## Dependencies
- Python 3.x
- `tqdm` (see `requirements.txt`)

Install:
```bash
pip install -r requirements.txt
