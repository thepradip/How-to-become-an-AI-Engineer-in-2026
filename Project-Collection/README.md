# 🛠️ Project Collection — Hands-On AI Engineering

A complete, **build-it-yourself** companion course to [*How to Become an AI Engineer in 2026*](../index.html).
Each of the 53 projects solves a **real-world problem** end-to-end — documented Python, a working UI,
automated tests, and a professional README. Together they form a portfolio you can show in interviews
and adapt for production work.

> Built for **working professionals, coders, and non-coders**. If you can follow a recipe and run a
> command, you can ship these. Start with [`00-getting-started`](00-getting-started/) to learn how to
> drive AI coding tools (Claude Code, Codex, Lovable) so the AI writes most of the code *with* you.

---

## How every project is structured

```
<track>/NN-project-slug/
  README.md          # the problem, the real dataset/model, the approach, how to run, results
  requirements.txt   # pinned dependencies
  src/               # documented Python (docstrings + type hints)
  app.py             # the UI — a thin shim over the shared chat interface
  tests/             # pytest (unit + a smoke test)
  data/              # download script only — real data is fetched on first run, never committed
```

### One UI for every app — the shared **chat interface**
We do **not** rebuild a UI per project. Every app uses one shared chat component
([`_shared/chat_ui.py`](_shared/chat_ui.py)), so all ~53 projects feel the same and you focus on the
*AI*, not on plumbing. A project's `app.py` is just a few lines:

```python
import sys, pathlib
sys.path.insert(0, str(pathlib.Path(__file__).resolve().parents[2]))   # add Project-Collection root
from _shared.chat_ui import run_chat_app
from src.handler import respond

run_chat_app(title="…", intro="…", respond=respond, examples=[...])
```

The chat UI renders **text, tables, charts, images, metrics and code** in the transcript, so a
churn model, a chest-X-ray classifier, a RAG bot and a multi-agent team all use the same surface.
A handful of flagship GenAI/agent apps also ship a **Next.js** showcase front-end.

### Levels
🟢 Beginner · 🟡 Intermediate · 🔴 Advanced — each track runs basic → advanced.

---

## Catalog (53 projects)

Every project below has the same shape — `README.md`, documented `src/`, `app.py` (shared chat UI),
`tests/`. Level: 🟢 Beginner · 🟡 Intermediate · 🔴 Advanced.

### `ml/` — Machine Learning · classic algorithms, training & tuning
| # | Project | What it does | Stack |
|---|---------|--------------|-------|
| 01 | **Customer Churn** 🟢 | Flags telco subscribers likely to cancel; compares LogReg / RF / XGBoost + a stacking ensemble, reports ROC-AUC and the top churn drivers. | scikit-learn, XGBoost |
| 02 | **House Prices** 🟢 | Price regression comparing Ridge / RF / Gradient Boosting + stacking; reports R²/MAE/RMSE and the features that drive price. | scikit-learn |
| 03 | **Fraud Detection** 🟡 | Imbalanced credit-card fraud with SMOTE oversampling + multi-algorithm stacking, tuned for recall. | scikit-learn, imbalanced-learn |
| 04 | **Credit Risk** 🟡 | Loan-default classifier (LogReg / RF / GBM + stacking) with feature-importance explanations. | scikit-learn |
| 05 | **Breast-Cancer Diagnosis** 🟢 | Explainable diagnosis on UCI Wisconsin; multi-algorithm + stacking with clinician-checkable importances. | scikit-learn |
| 06 | **Customer Segmentation** 🟡 | RFM features from raw transactions; KMeans vs Agglomerative vs DBSCAN scored by silhouette, labelled segments. | scikit-learn |
| 07 | **Demand Forecasting** 🟡 | Forecasting as supervised regression on lag + calendar features vs a seasonal-naive baseline; MAE/RMSE/MAPE. | scikit-learn |
| 08 | **Stock Movement** 🔴 | Technical features → chronological split (no look-ahead leakage) → honest backtest of long/flat vs buy-and-hold. | scikit-learn, yfinance |
| 09 | **Movie Recommender** 🟡 | SVD matrix factorization vs mean baselines on MovieLens, held-out RMSE + top-k recommendations. | scikit-learn |
| 10 | **AutoML + Optuna** 🔴 *capstone* | An Optuna study tuning a gradient-boosting model with a default-vs-tuned comparison and optimization-history chart. | Optuna, scikit-learn |

### `deep-learning/` — PyTorch · training, transfer learning, fine-tuning
| # | Project | What it does | Stack |
|---|---------|--------------|-------|
| 01 | **CNN from Scratch** 🟢 | A `SimpleCNN` + training loop on Fashion-MNIST that classifies example images. | PyTorch, torchvision |
| 02 | **Transfer Learning** 🟡 | Swaps ResNet-18's head, freezes the backbone, fine-tunes on any `ImageFolder` dataset. | PyTorch, torchvision |
| 03 | **Pneumonia X-ray** 🔴 | Fine-tuned ResNet-18 (normal vs pneumonia) + a from-scratch Grad-CAM overlay for explainability. | PyTorch, Grad-CAM |
| 04 | **Object Detection** 🟡 | A YOLO11 detector — upload an image, get an annotated image + a table of detections. | Ultralytics YOLO11 |
| 05 | **U-Net Segmentation** 🔴 | A compact U-Net with skip connections, pixel-wise training loop, input-vs-mask viz. | PyTorch |
| 06 | **Traffic Signs** 🟡 | A colour-image CNN over GTSRB 32×32 crops, trained and evaluated in the chat UI. | PyTorch, torchvision |
| 07 | **LSTM Forecasting** 🟡 | An LSTM that predicts the next value from a window, then forecasts multiple steps recursively. | PyTorch |
| 08 | **Speech Emotion** 🟡 | Audio → MFCC features → MLP classifier (librosa, with a numpy spectral fallback so it runs offline). | PyTorch, librosa |
| 09 | **Face Verification** 🔴 | A CNN that maps a face to an L2-normalised embedding, then verifies pairs by cosine similarity. | PyTorch |
| 10 | **ViT Fine-Tune** 🔴 *capstone* | A Vision Transformer with a swapped head + fine-tune loop + optional Weights & Biases sweeps. | PyTorch, W&B |

### `nlp/` — classic NLP → transformers → LLM fine-tuning
| # | Project | What it does | Stack |
|---|---------|--------------|-------|
| 01 | **SMS Spam** 🟢 | TF-IDF comparing Naive Bayes / LogReg / Linear SVM; paste a message, get spam/ham + confidence. | scikit-learn |
| 02 | **Sentiment** 🟢 | TF-IDF classifier comparison that scores any review; documents the DistilBERT fine-tune path for SOTA. | scikit-learn, DistilBERT |
| 03 | **Fake News** 🟡 | TF-IDF NB / LogReg / SVM classifier that scores any headline. | scikit-learn |
| 04 | **Named Entity Recognition** 🟡 | A rule-based extractor in the chat UI; documents the fine-tuned BERT / spaCy production path. | spaCy, HF Transformers |
| 05 | **Summarization** 🟡 | A faithful extractive summarizer (frequency-scored sentences) + the documented BART abstractive path. | HF Transformers (BART) |
| 06 | **Topic Modeling** 🟡 | Compares NMF (on TF-IDF) and LDA (on counts), shows top words per topic, matches new docs to a topic. | scikit-learn |
| 07 | **Machine Translation** 🟡 | A chat translator — offline word-lookup demo + the real NLLB-200 path via Transformers. | HF Transformers (NLLB-200) |
| 08 | **Question Answering** 🟡 | A TF-IDF sentence-relevance baseline over your `context:` + the SQuAD BERT span-extraction path. | scikit-learn, BERT |
| 09 | **LLM Fine-Tune (LoRA/QLoRA)** 🔴 *16 GB GPU* | Alpaca-format instruction-data prep + a complete Unsloth QLoRA training script. | Unsloth, QLoRA, HF |
| 10 | **Semantic Search** 🟡 | A TF-IDF résumé ↔ job matcher + the sentence-transformer dense-embedding upgrade. | scikit-learn, sentence-transformers |

### `genai/` — LLM apps, RAG, image/video, local inference, guardrails
| # | Project | What it does | Stack |
|---|---------|--------------|-------|
| 01 | **Prompt Playground** 🟢 | Multi-provider chat (OpenAI / Anthropic / Ollama / offline mock) that shows which model answered + a chain-of-thought transform. | shared LLM client |
| 02 | **RAG — Chat with Docs** 🟡 | Chunk → retrieve → answer **with citations** over your text or PDFs. | TF-IDF / embeddings, pypdf |
| 03 | **GraphRAG** 🔴 | Entity extraction → a networkx co-occurrence graph → neighbourhood retrieval → grounded answer. | networkx |
| 04 | **Local LLM Chat** 🟡 | Chats against a local model via Ollama or a vLLM OpenAI-compatible server, with history. | Ollama, vLLM |
| 05 | **1-bit LLMs (BitNet)** 🔴 | From-scratch ternary (absmean) quantization — converts weights to {−1,0,1}, reports compression + error. | numpy (BitNet) |
| 06 | **Image Generation** 🟡 | Text-to-image — a procedural offline demo + the real `diffusers` path (SD 3.5 / FLUX). | diffusers |
| 07 | **Video Generation** 🔴 | Text-to-video — a procedural GIF offline demo + the `diffusers` LTX-Video / hosted-API path. | diffusers (LTX-Video) |
| 08 | **Document Intelligence / OCR** 🟡 | scan/PDF → OCR → field extraction; extraction tested offline, modern OCR engines documented. | Docling / olmOCR / Qwen2.5-VL |
| 09 | **Structured Extraction** 🟡 | A Pydantic schema validated on the way in — regex offline, PydanticAI (LLM fills the schema) in production. | Pydantic, PydanticAI |
| 10 | **Evals + Guardrails** 🔴 *LLMOps capstone* | Quality metrics (exact-match, faithfulness recall) + guardrails (PII, banned-content) aggregated into a report. | Ragas / DeepEval patterns |

### `agents/` — frameworks & real agent types
| # | Project | What it does | Stack |
|---|---------|--------------|-------|
| 01 | **ReAct from Scratch** 🟢 | A ReAct executor with a safe calculator + lookup tool and a transparent Thought/Action/Observation trace. | pure Python |
| 02 | **SQL Agent** 🟡 | Natural language → SQL over a real SQLite DB; LangGraph + a schema-aware LLM in production. | SQLite, LangGraph |
| 03 | **Web / Browser Agent** 🟡 | Navigates a site and extracts answers with a visible trace; browser-use / Playwright on a live browser in production. | browser-use, Playwright |
| 04 | **Research Agent** 🟡 | Searches a corpus, ranks sources, writes a **cited** synthesis; CrewAI + a web-search tool in production. | CrewAI |
| 05 | **Multi-Agent Content Team** 🟡 | A researcher → writer → editor pipeline that turns a topic into an article, showing each role's output. | CrewAI |
| 06 | **Conversational Multi-Agent** 🟡 | A Solver ↔ Critic dialogue that refines an answer over rounds, with the full transcript. | AutoGen / AG2 |
| 07 | **Type-safe Tool Agent** 🟡 | Tools with Pydantic arg models + validators and a router that validates before executing. | PydanticAI, Pydantic |
| 08 | **A2A — Across Frameworks** 🔴 | An A2A message schema + agent cards; two cross-framework agents collaborate on one task. | A2A protocol |
| 09 | **Healthcare Agent** 🔴 | Guideline-RAG wrapped in safety rails: emergency escalation, refusal to diagnose/prescribe, disclaimer on every answer. | RAG + guardrails |
| 10 | **Finance Agent** 🟡 | A finance analyst over a financials table (SQLite) with a no-advice guardrail; RAG over 10-Ks in production. | SQLite, RAG |
| 11 | **Voice Agent** 🔴 | An STT → LLM → TTS pipeline; the text orchestration is tested offline, the audio edges are documented. | Whisper, TTS |
| 12 | **Guardrails / Safety** 🟡 | An input rail (jailbreak / disallowed-request blocking) + an output rail (PII masking) wrapping a model. | NeMo Guardrails, Guardrails AI |
| 13 | **Agent Harness** 🔴 *capstone* | Routes a task to the right skill, retries, returns a full trace + metrics; Claude Agent SDK / LangGraph + a tracer in production. | Claude Agent SDK, Langfuse |

---

## Quick start

```bash
cd Project-Collection
python -m venv .venv && source .venv/bin/activate    # or: uv venv && source .venv/bin/activate
cd ml/01-customer-churn
pip install -r requirements.txt
python src/download_data.py          # fetches the real dataset into ./data
pytest -q                            # tests should pass
streamlit run app.py                 # open the chat UI in your browser
```

See [`00-getting-started/environment-setup.md`](00-getting-started/environment-setup.md) for GPU
notes (T4 / Apple M-series 16 GB), Ollama, vLLM, and the recommended 2026 local-model list.

## Conventions
- **Real, current datasets & models** — loaded via open registries/APIs (OpenML, UCI, Hugging Face,
  yfinance, Kaggle) on first run.
- **Never commit data, model weights, or secrets** — `.gitignore` enforces it.
- Each README has an honest **“Tested on”** line stating exactly what was run (CPU vs. GPU-required).

## Progress
This collection is built in reviewable batches. See [`PROGRESS.md`](PROGRESS.md) for what's shipped.
