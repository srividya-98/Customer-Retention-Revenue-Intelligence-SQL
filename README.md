# DuckDB SQL Analytics

Run pure SQL on a CSV using DuckDB (no pandas).

## Setup

```bash
pip install -r requirements.txt
```

## Usage

1. Put your Kaggle CSV path in `analytics.py` (variable `CSV_PATH`).
2. Run:

```bash
python analytics.py
```

Or open `analytics.ipynb` in Cursor/VS Code and run the cells.

## What the script does

- Connects to an in-memory DuckDB database
- Loads the CSV into a table named `data`
- Prints schema (`DESCRIBE`), preview (first 5 rows), and example SQL patterns (SELECT, WHERE, GROUP BY)

Adjust column names in the commented examples to match your dataset after inspecting the schema.
