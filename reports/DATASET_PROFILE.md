# Dataset profile

Source file: `all_upwork_jobs_2024-02-07-2024-03-24 (1).csv`

- Rows: 244,828
- Columns: 8
- Columns: title, link, published_date, is_hourly, hourly_low, hourly_high, budget, country

The supplied file is included as `dataset/raw_jobs.csv`. Run preprocessing to generate `dataset/cleaned_jobs.csv`.

Interpretation notes:
- Hourly low/high are only relevant to hourly postings.
- Fixed-price `budget` is a different measure and should not be combined with hourly rates.
- Country can be missing.
- The dataset does not contain job descriptions, explicit remote status, applicant counts, skills, or confirmed currency metadata.
