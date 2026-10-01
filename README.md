# 📊 LLM-Powered Sales Analytics Agent (LangChain + OpenAI)

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-ReAct%20Agent-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--3.5-412991?style=flat-square&logo=openai&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Forecasting-EB5E28?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

> Ask business questions about sales data **in plain English** — *"Forecast sales for Motorcycles"*, *"Detect anomalies"*, *"Which product line is most profitable?"* — and an LLM agent decides which analytics tool to run and explains the result.

---

## 📌 Why

Business users often need quick answers from data but depend on analysts to write queries. This project combines an **LLM's reasoning** with **reliable, pre-built analytics functions**, so the LLM doesn't guess numbers — it **calls tools** that compute them.

## 🏗️ Architecture

```mermaid
flowchart LR
    U[User question] --> A[LangChain pandas-DataFrame agent<br/>ReAct · GPT-3.5 · temp 0]
    A -->|chooses tool| T1[📈 XGBoost sales forecast]
    A --> T2[🚨 Z-score anomaly detection]
    A --> T3[🌍 Region / territory breakdown]
    A --> T4[💰 Profitability analysis]
    A --> T5[🔁 Time-series decomposition]
    A --> T6[📝 Summary report]
    A --> T7[🐍 Python REPL on the DataFrame]
    T1 & T2 & T3 & T4 & T5 & T6 & T7 --> A
    A --> R[Natural-language answer + table]
```

**Stage 1 – Data engineering** (Kaggle *Sample Sales Data*, 2,823 order lines):
merged address fields, built `location`, filled missing `territory` from a country → region map, parsed dates, normalised column names and removed duplicates, then explored trends with Seaborn/Plotly.

**Stage 2 – Agent:** a `create_pandas_dataframe_agent` (zero-shot ReAct) with **six custom tools**, each wrapped with input validation and error handling, plus file-backed conversation memory.

## 🧪 Example Interactions (from the notebook)

| Question | Tool used | Answer (abridged) |
|---|---|---|
| *Forecast sales for the Motorcycles product line* | XGBoost forecaster | 6-month forecast table |
| *Detect any anomalies in the sales data* | Z-score detector | 1 anomaly — 2005-03-03, $10,066.6, z = 3.83 |
| *Show me the sales breakdown for NA* | Region breakdown | Total / mean / median sales by city |
| *Generate a summary report* | Report generator | $10.03 M total sales · 92 customers · 7 product lines · top territory EMEA |
| *Least selling product?* | Python REPL | **Trains** ($226 K) |

## 💡 Lessons Learned (honest notes)

- **Tool descriptions are the real prompt.** The agent once answered *"top selling product"* using the *profitability* tool — tighter tool descriptions are needed to route correctly.
- Tools must **fail gracefully**: the forecaster reports when there is too little history to compute error metrics; the decomposition tool surfaced a file-path error instead of crashing the agent.
- Deterministic Python tools + LLM orchestration is far more trustworthy than asking an LLM to do arithmetic.

## 🔭 Next Steps

- Add a Streamlit chat UI and deploy it.
- Evaluate tool-selection accuracy on a fixed question set.
- Migrate to LangGraph / tool-calling models for more reliable routing.

## 🚀 How to Run

```bash
git clone https://github.com/AnishRane-cox/LLM-AI-Analytic-Project.git
cd LLM-AI-Analytic-Project
pip install openai langchain langchain-experimental langchain-openai langchain-community xgboost statsmodels pandas seaborn plotly kaggle tabulate
export OPENAI_API_KEY="your-openai-key"
jupyter notebook "LLM_–_Powered_Data_Analytics_Agent.ipynb"
```

Download the dataset with `kaggle datasets download -d kyanyoga/sample-sales-data` (needs a Kaggle API key), or place `sales_data_sample.csv` next to the notebook. The notebook was built in Colab — adjust the Drive paths if running locally.

> ⚠️ The pandas agent executes model-generated Python (`allow_dangerous_code=True`). Run it only in a sandboxed environment.

## 📁 Repository Structure

```
├── LLM_–_Powered_Data_Analytics_Agent.ipynb      # Data prep + agent + tests
├── LLM_–_Powered_Data_Analytics_Agent_DOC.pdf    # Project documentation
├── LICENSE
└── README.md
```

---

## 👤 Author

**Anish Rane** — Data & AI Engineer · MSc Machine Learning & AI (LJMU) · Mechanical Engineer

[![Portfolio](https://img.shields.io/badge/Portfolio-1D9E75?style=flat-square&logo=githubpages&logoColor=white)](https://anishrane-cox.github.io/Portfolio/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/anish-rane/)
[![GitHub](https://img.shields.io/badge/GitHub-AnishRane--cox-181717?style=flat-square&logo=github)](https://github.com/AnishRane-cox)

⭐ If you found this useful, consider starring the repo.
