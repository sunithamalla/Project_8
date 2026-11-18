# Job Market Analysis & Recommendation System

An end-to-end starter implementation based on the supplied Upwork job-postings CSV.

## Dataset
`dataset/raw_jobs.csv` contains 244,828 rows and these fields:
`title, link, published_date, is_hourly, hourly_low, hourly_high, budget, country`.

Important limitations:
- This is a historical snapshot, not a live jobs feed.
- The dataset has no explicit remote-work flag; remote analysis uses title-keyword matches as a proxy only.
- Currency is not explicitly specified in the CSV. Do not label rates USD without external confirmation.
- The time span is short and unevenly distributed; forecasts are exploratory and should not be presented as reliable long-term predictions.
- Title-based categories are rule-based broad categories, not ground-truth industry labels.
- The recommender is content-based TF-IDF on title and country; it does not use user history or full job descriptions.

## Setup (Windows PowerShell)
```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python -m src.preprocessing
python -m src.analysis
python -m src.demand_model
streamlit run dashboard/app.py
```

## API
In another terminal:
```powershell
python api/main.py
```
Health check: `http://localhost:5000/health`

Example request:
```bash
curl -X POST http://localhost:5000/recommend -H "Content-Type: application/json" -d "{\"role\":\"Data Engineer\",\"skills\":\"Python SQL PySpark Azure\",\"country\":\"India\",\"top_n\":5}"
```

## Docker
```bash
docker compose up --build
```
Dashboard: http://localhost:8501
API: http://localhost:5000/health

## Analysis outputs
Running `python -m src.analysis` creates CSV summaries and PNG charts in `reports/`.

## Project task mapping
1. Salary vs title keywords: `reports/salary_by_keyword.csv`
2. Emerging categories: `reports/category_monthly_trends.csv` and `reports/category_frequency.csv`
3. Demand pattern baseline: `reports/weekly_demand.csv`; run `python -m src.demand_model`
4. Country hourly rates: `reports/country_hourly_rates.csv`
5. Recommendation prototype: Streamlit tab and `/recommend` API
6. Monthly dynamics: `reports/category_monthly_trends.csv`; rerun after adding monthly source files
7. Remote landscape: `reports/remote_keyword_proxy.csv` (proxy only)
8. Future trends: exploratory demand model; more history required for robust forecasts

## Suggested next improvements
- Add a repeatable monthly ingestion process and a database such as PostgreSQL.
- Add job descriptions and explicit remote, experience, contract, and currency fields.
- Replace rule-based categories with a validated taxonomy or supervised classifier.
- Use more months/years of data and time-based backtesting before forecasting.
- Add authentication, request validation, logging, and production WSGI serving before public deployment.
Outpus :
---------
- <img width="1600" height="673" alt="WhatsApp Image 2026-11-18 at 11 42 04 AM" src="https://github.com/user-attachments/assets/dec0f1aa-bceb-4f27-8bd8-790ed7317fde" />
-<img width="1600" height="488" alt="WhatsApp Image 2026-11-18 at 11 48 03 AM" src="https://github.com/user-attachments/assets/67ba9666-9724-4dd4-a9e1-05eb4c299eb3" />

