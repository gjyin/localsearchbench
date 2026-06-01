<p align="center">
  <img src="assets/xiaotuan.jpg" alt="问小团 logo" width="100" />
</p>

# LocalSearchBench

**Benchmarking Agentic Search in Real-World Local Life Services**

LocalSearchBench is a benchmark for evaluating LRM-based agentic search in local life services. This repository is aligned with the camera-ready paper and includes the benchmark data pointer, evaluation toolkit, and leaderboard snapshot.

## 🌐 Quick Links

- **Project Website**: [localsearchbench.github.io](https://localsearchbench.github.io)
- **Code Repository**: [github.com/localsearchbench/localsearchbench](https://github.com/localsearchbench/localsearchbench)
- **Artifact DOI**: [10.5281/zenodo.20416849](https://doi.org/10.5281/zenodo.20416849)
- **Paper DOI**: [10.1145/3770855.3817466](https://doi.org/10.1145/3770855.3817466)

## 📝 Abstract

Recent advances in large reasoning models (LRMs) have enabled agentic search systems to perform complex multi-step reasoning across multiple sources. However, most studies focus on general information retrieval and rarely explore vertical domains with unique challenges. In this work, we focus on local life services and introduce **LocalSearchBench**, which encompasses diverse and complex business scenarios. Real-world queries in this domain are often ambiguous and require multi-hop reasoning across merchants and products, remaining challenging and not fully addressed. As the first comprehensive benchmark for agentic search in local life services, LocalSearchBench comprises a database of over **1.3M** merchant entries across **6** service categories and **9** major cities, and **900** multi-hop QA tasks from real user queries that require multi-step reasoning. We also develop **LocalPlayground**, a unified environment integrating multiple tools for LRM interaction. Experiments show that even state-of-the-art LRMs struggle on LocalSearchBench: the best model (**DeepSeek-V3.2**) achieves only **35.60%** correctness, and most models have issues with completeness (average **60.32%**) and faithfulness (average **30.72%**). This highlights the need for specialized benchmarks and domain-specific agent training in local life services.

## ⭐ Key Features

- **Six service categories**: Dining, Lifestyle, Shopping, Accommodation, Healthcare, and Tourism.
- **Nine major Chinese cities**: Shanghai, Beijing, Guangzhou, Shenzhen, Hangzhou, Chengdu, Chongqing, Wuhan, and Suzhou.
- **Merchant-scale grounding**: **1,354,185** final merchant profiles constructed from over **1.6M** original seed records.
- **Real-world geographic coverage**: **10,741** landmarks, **145** districts, and **9,956,907** retrievals.
- **Multi-hop QA supervision**: **900** validated multi-hop QA tasks, with L3/L4 intelligence levels and 3–5 search hops.
- **LocalPlayground evaluation**: Integrated LocalRAG and web-search tools for measuring answer quality and trajectory quality.

## 📊 Benchmark At a Glance

| Item | Value |
| --- | ---: |
| Final merchant profiles | 1,354,185 |
| Original merchant seed records | 1.6M+ |
| Primary service categories | 6 |
| Major Chinese cities | 9 |
| Landmarks | 10,741 |
| Districts | 145 |
| Retrievals | 9,956,907 |
| Multi-hop QA tasks | 900 |
| Hop count distribution | 3-hop 60.0%, 4-hop 30.0%, 5-hop 10.0% |
| Intelligence-level distribution | L3 66.7%, L4 33.3% |

### Geographic Coverage

| City | Landmarks | Districts | Retrievals |
| --- | ---: | ---: | ---: |
| Shanghai | 1,556 | 16 | 1,442,412 |
| Beijing | 1,451 | 16 | 1,345,077 |
| Guangzhou | 1,026 | 11 | 951,102 |
| Shenzhen | 1,039 | 9 | 963,153 |
| Hangzhou | 1,129 | 13 | 1,046,583 |
| Chengdu | 1,073 | 20 | 994,671 |
| Chongqing | 1,008 | 38 | 934,416 |
| Wuhan | 1,040 | 13 | 964,080 |
| Suzhou | 1,149 | 9 | 1,065,123 |
| Total | 10,741 | 145 | 9,956,907 |


## 🧱 Data Fields

| Field | Type | Description |
| --- | --- | --- |
| `Hop Count` | `int64` | Number of chained search hops used to solve the query (3–5). |
| `Difficulty` | `string` | L3 (Intelligent) or L4 (Expert). |
| `City` | `string` | One of the nine supported Chinese cities. |
| `Question` | `string` | Natural-language request describing the user's goal. |
| `Multi-hop search path` | `string` | Serialized trace of each hop's query and retrieved evidence. |
| `Answer` | `string` | Final recommendation or answer grounded in retrieved evidence. |

The dataset file in `data/` is stored with Git LFS. Please make sure Git LFS is enabled before cloning or pulling the repository.

```bash
git lfs install
git clone https://github.com/localsearchbench/localsearchbench.git
```

## 🚀 Sample Usage

```python
from datasets import load_dataset

ds = load_dataset("localsearchbench/localsearchbench")
print(ds["train"][0]["Question"])
print(ds["train"][0]["Multi-hop search path"])
print(ds["train"][0]["Answer"])
```

## 🏅 Leaderboard Snapshot

The following numbers follow the camera-ready paper's Table 5, under **Max Round N = 5**.

### 📊 Answer Quality Metrics

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

### 🎯 Trajectory Effectiveness Metrics

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

## 📚 Citation

```bibtex
@inproceedings{he2026localsearchbench,
  title={LocalSearchBench: Benchmarking Agentic Search in Real-World Local Life Services},
  author={He, Hang and Yue, Chuhuai and Dong, Chengqi and Tian, Mingxue and Chen, Hao and Liu, Zhenfeng and Chai, Jiajun and Wang, Xiaohan and Zhang, Yufei and Liao, Qun and Yin, Guojun and Lin, Wei and Wan, Chengcheng and Sun, Haiying and Su, Ting},
  booktitle={Proceedings of the 32nd ACM SIGKDD Conference on Knowledge Discovery and Data Mining V.2},
  year={2026},
  doi={10.1145/3770855.3817466}
}
```

## ✅ License

MIT License. Commercial and research use permitted with attribution to LocalSearchBench.
