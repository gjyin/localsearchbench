# LocalSearchBench Evaluation Toolkit

Evaluation toolkit for [LocalSearchBench](https://github.com/localsearchbench/localsearchbench), aligned with the KDD 2026 camera-ready benchmark and leaderboard.

## 📝 Overview

LocalSearchBench evaluates LRM-based agentic search in local life services. The benchmark contains **1,354,185** merchant profiles and **900** validated multi-hop QA tasks across **9** major Chinese cities and **6** service categories. LocalPlayground combines LocalRAG and web-search tools to measure both answer quality and trajectory quality.

## 🧱 Data Fields

| Field | Type | Description |
| --- | --- | --- |
| `Hop Count` | `int64` | Number of chained search hops used to solve the query (3–5). |
| `Difficulty` | `string` | L3 (Intelligent) or L4 (Expert). |
| `City` | `string` | One of the nine supported Chinese cities. |
| `Question` | `string` | Natural-language request describing the user's goal. |
| `Multi-hop search path` | `string` | Serialized trace of each hop's query and retrieved evidence. |
| `Answer` | `string` | Final recommendation or answer grounded in retrieved evidence. |

## 🚀 Usage

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the scripts in this folder according to the desired evaluation mode:

- `run_rag_llm_baseline.py`: RAG + LLM baseline.
- `run_api_only_baseline.py`: API-only baseline.
- `evaluation_pipeline_agent.py`: agent-based evaluation pipeline.
- `evaluate_trajectories.py`: trajectory-quality evaluation.
- `summarize_answer_scores.py`: answer-metric aggregation.
- `summarize_trajectory_scores.py`: trajectory-metric aggregation.

## 🏅 Leaderboard Snapshot

The following numbers follow the camera-ready paper's Table 5, under **Max Round N = 5**.

### Answer Quality Metrics

| Model | Avg. tool calls | Avg. rounds | Correctness (%) | Completeness (%) | Fluency (%) | Faithfulness (%) | Safety (%) |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Qwen3-235B-A22B (w/o thinking) | 2.00 | 2.93 | 21.18 | 50.94 | 69.16 | 25.28 | 79.72 |
| Qwen3-235B-A22B (w/ thinking) | 2.31 | 3.17 | 30.24 | 71.20 | 71.58 | 26.90 | 81.76 |
| Qwen3-32B (w/o thinking) | 2.78 | 3.11 | 19.76 | 40.96 | 68.50 | 21.38 | 80.76 |
| Qwen3-32B (w/ thinking) | 2.80 | 3.12 | 25.63 | 40.66 | 68.44 | 22.40 | 79.54 |
| Qwen3-14B (w/o thinking) | 2.53 | 2.07 | 24.21 | 40.60 | 69.62 | 27.44 | 80.78 |
| Qwen3-14B (w/ thinking) | 2.57 | 2.12 | 25.17 | 40.98 | 69.32 | 28.40 | 80.44 |
| GPT-4.1 | 1.73 | 2.42 | 18.47 | 45.37 | 65.93 | 28.76 | 77.38 |
| o3(high) | 2.91 | 3.38 | 31.53 | 69.64 | 70.72 | 33.89 | 81.87 |
| Gemini-2.5-Flash | 1.84 | 2.51 | 20.97 | 58.44 | 68.04 | 35.72 | 79.70 |
| Gemini-2.5-Pro | 2.75 | 3.10 | 32.34 | 71.03 | 71.12 | 34.93 | 82.32 |
| LongCat-Flash-Chat | 2.34 | 3.07 | 25.28 | 52.98 | 69.45 | 27.49 | 83.61 |
| LongCat-Flash-Thinking | 3.04 | 3.20 | 30.68 | 68.83 | 69.07 | 31.47 | 80.10 |
| GLM-4.6 (w/o thinking) | 2.86 | 3.86 | 28.97 | 76.45 | 70.37 | 35.40 | 81.40 |
| GLM-4.6 (w/ thinking) | 3.08 | 4.06 | 32.83 | 76.83 | 70.27 | 37.48 | 81.30 |
| DeepSeek-V3.2 (w/o thinking) | 3.12 | 4.11 | 32.74 | 77.08 | 70.12 | 35.96 | 81.52 |
| DeepSeek-V3.2 (w/ thinking) | 3.21 | 4.20 | 35.60 | 77.56 | 70.92 | 39.78 | 81.13 |

### Trajectory Effectiveness Metrics

| Model | Action Relevance (%) | Evidence Sufficiency (%) | Causal Coherence (%) | Search Efficiency (%) |
| --- | ---: | ---: | ---: | ---: |
| Qwen3-235B-A22B (w/o thinking) | 75.22 | 43.61 | 50.68 | 45.99 |
| Qwen3-235B-A22B (w/ thinking) | 80.42 | 45.75 | 52.04 | 48.63 |
| Qwen3-32B (w/o thinking) | 74.67 | 46.52 | 48.82 | 49.84 |
| Qwen3-32B (w/ thinking) | 75.06 | 46.99 | 48.87 | 49.13 |
| Qwen3-14B (w/o thinking) | 80.46 | 46.44 | 50.96 | 50.02 |
| Qwen3-14B (w/ thinking) | 81.19 | 47.24 | 52.52 | 51.65 |
| GPT-4.1 | 68.47 | 38.62 | 45.83 | 42.29 |
| o3(high) | 75.93 | 44.71 | 51.78 | 42.96 |
| Gemini-2.5-Flash | 70.58 | 41.61 | 48.94 | 46.91 |
| Gemini-2.5-Pro | 77.31 | 45.73 | 52.87 | 41.78 |
| LongCat-Flash-Chat | 77.78 | 47.33 | 50.86 | 52.29 |
| LongCat-Flash-Thinking | 78.50 | 47.37 | 53.18 | 53.27 |
| GLM-4.6 (w/o thinking) | 74.28 | 48.44 | 50.79 | 52.76 |
| GLM-4.6 (w/ thinking) | 77.66 | 48.90 | 52.67 | 54.43 |
| DeepSeek-V3.2 (w/o thinking) | 75.51 | 48.49 | 52.23 | 54.33 |
| DeepSeek-V3.2 (w/ thinking) | 75.58 | 48.86 | 52.62 | 54.83 |

## 📜 License

MIT License.
