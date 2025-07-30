
# 📊 LLM–Powered Data Analytics Agent

A Streamlit-ready, LangChain-powered agent that enables natural language analytics on structured sales data using large language models (LLMs), machine learning, and statistical tooling.

---

## 🚀 Project Features

- 💬 Ask natural language questions about your sales data
- 📈 Forecast future sales using XGBoost
- ⚠️ Detect anomalies using Z-score method
- 🌍 Breakdown regional sales performance
- 💰 Analyze profitability across product lines
- 📊 Decompose time series into trend/seasonality
- 📝 Generate natural language sales reports

---

## 🗂️ Project Structure

```
llm_data_analytics_agent/
├── llm_powered_data_analytics_agent.py   # Main logic (LangChain + Streamlit + Tools)
├── cleaned_sales_data.csv                # Cleaned dataset used by the agent
├── memory.json                           # Memory file for conversation history
├── README.md                             # Project documentation
```

---

## 📦 Requirements

Install all dependencies in a virtual environment or Google Colab:

```bash
pip install -U openai langchain streamlit pandas numpy matplotlib seaborn plotly
pip install -U langchain-community langchain-openai langchain-experimental
pip install -U kaggle kagglehub pyngrok xgboost statsmodels mlxtend
```

---

## 🔑 Setup

1. **Obtain Required Keys:**
   - OpenAI API Key
   - Kaggle API Key (`kaggle.json`)

2. **Environment Setup:**
```bash
export OPENAI_API_KEY=your_openai_key
export KAGGLE_USERNAME=your_kaggle_username
export KAGGLE_KEY=your_kaggle_key
```

3. **Kaggle Dataset Download (Optional):**
```bash
kaggle datasets download -d kyanyoga/sample-sales-data
unzip sample-sales-data.zip
```

---

## 🧠 How It Works

The system uses the LangChain `create_pandas_dataframe_agent` with extra tools:

- `SalesForecastingToolXGBoost`
- `AnomalyDetectionTool`
- `RegionSalesBreakdownTool`
- `ProfitabilityAnalysisTool`
- `TimeSeriesDecompositionTool`
- `ReportGeneratorTool`

Each tool is wrapped with `wrap_tool()` to make it compatible with single-string input passed by the LangChain agent.

---

## ▶️ Running the Agent

### ✅ Option 1: Run in Google Colab

- Open `llm_powered_data_analytics_agent.py` in Colab
- Make sure the required `userdata.get()` entries are present
- Run cells sequentially
- Use `dc_agent.run("Your question")` to interact

### ✅ Option 2: Run with Streamlit

You can convert the script into a Streamlit app with a UI:

```bash
streamlit run llm_powered_data_analytics_agent.py
```

Update the script to support Streamlit input/output rendering.

---

## 💡 Example Queries

- "Forecast sales for the Motorcycles product line."
- "Detect any anomalies in the sales data."
- "What is the sales breakdown for APAC?"
- "Generate a summary report of performance."

---

## 🧩 Challenges Solved

- Handling single string input with `wrap_tool()`
- LLM tool selection using `ZERO_SHOT_REACT_DESCRIPTION`
- Formatting mixed outputs (tables, plots, markdown)
- Integrating memory (`ConversationBufferMemory`) across runs

---

## 📎 License

MIT License © 2025 — Anish Nilesh Rane

---
