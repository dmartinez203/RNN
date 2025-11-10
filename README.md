# Next-Word Prediction with LSTM

This project trains a next-word predictor (many-to-one) using Keras/TensorFlow and provides a Streamlit app for interactive completions.

## Contents
- `next_word_lstm.ipynb` — end-to-end notebook: data, model, training, evaluation, and analysis
- `models/best_next_word_lstm.keras` — best checkpoint (created by the notebook)
- `artifacts/` — tokenizer/config/metrics written by the notebook
- `streamlit_app.py` — Streamlit UI to try the trained model interactively

## Quick start

1) Create a Python environment and install deps:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

2) Run the notebook to prepare artifacts (dataset, train, evaluate):
- Open `next_word_lstm.ipynb` and run cells top-to-bottom.
- Fast-run is enabled by default for quick iteration. To train longer, set `CFG['FAST_EPOCHS']` and re-run.
- Artifacts produced:
  - `models/best_next_word_lstm.keras`
  - `artifacts/tokenizer.json`
  - `artifacts/config.json`
  - `artifacts/train_history.json`
  - `artifacts/eval_metrics.json`
  - `artifacts/cost_metrics_report.json` (optional; run final metrics cell)

3) Launch the Streamlit app:

```bash
streamlit run streamlit_app.py
```

Open the URL Streamlit prints (typically http://localhost:8501). Enter a prompt, adjust temperature and length, and generate completions.

## Results report
After training, you can generate an updated Markdown report with metrics by running:

```bash
python scripts/generate_results_md.py
```

This will write `docs/RESULTS.md` with training/eval and cost metrics.

## Troubleshooting
- Missing artifacts: Run the notebook first so `models/` and `artifacts/` are populated.
- Slow training: leave fast-run on (skips GloVe, caps samples/epochs), or reduce `MAX_SAMPLES` further.
- Crashes on dataset prep: the notebook uses a memory-safe `tf.data` pipeline; ensure you’ve re-run the updated data cell.
