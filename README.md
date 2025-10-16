# job-data-cleaning-pyspark
End-to-end job data cleaning and aggregation pipeline using PySpark on Databricks



Job Data Cleaning & Analytics Pipeline
📌 Project Overview

This project demonstrates a real-world end-to-end data cleaning and aggregation pipeline using PySpark on Databricks.
It handles multiple messy job datasets, cleans them, merges them, and produces aggregated insights across multiple layers:

## 📂 Datasets

The project merges multiple job posting datasets from different sources, including:

1. **Arshkons Data Engineer Postings**  
   - CSV containing job postings with columns like `job_id`, `company_name`, `title`, `description`, `normalized_salary`, etc.  
   - Source: [Arshkons Job Market Dataset](#) *(https://www.kaggle.com/datasets/arshkon/linkedin-job-postings)*

2. **Job Descriptions Data**  
   - CSV with detailed job descriptions, work types, and salary ranges.  
   - Source: [Job Descriptions Dataset](#)*(https://www.kaggle.com/datasets/ravindrasinghrana/job-description-dataset)

3. **JobStreet Dataset**  
   - Large dataset of job postings from JobStreet, including salaries, company info, skills, and job types.  
   - Source: [JobStreet All Job Dataset](#) *(https://www.kaggle.com/datasets/azraimohamad/jobstreet-all-job-dataset)

4. **dfall_clean.csv**  
   - Pre-cleaned CSV dataset with job listings, locations, and salaries.  
   - Source: Internal/aggregated dataset from previous cleaning efforts or public dataset compilation.

> ⚠️ Note: The actual CSV files are not included in this repository due to size restrictions and licensing. These sources are referenced for reproducibility and context.


Bronze Layer: Raw merged data from multiple sources

Silver Layer: Cleaned and normalized data (skills extraction, salaries, job types, years)

Gold Layer: Aggregated metrics for analytics (jobs per company, salary ranges, top skills, etc.)

⚠️ Note: Advanced country extraction is included as a method but not applied due to limited resources on the free Databricks serverless cluster.


🧰 Tools & Libraries

PySpark (DataFrame transformations, cleaning, and aggregations)

Databricks Free Edition (serverless cluster)

Python Libraries: pandas, geotext, country_converter (for optional country extraction)

CSV files as datasets



datasets

🚀 Workflow
1️⃣ Bronze Layer — Raw Data Merging

Multiple CSV datasets of job postings are loaded from different sources.

Columns are normalized (e.g., job_id, company_name, title, normalized_salary, etc.)

Missing or malformed data is handled:

Null numeric fields → 0

Null string fields → empty string

Timestamps are converted to human-readable dates.

All datasets are merged into a single bronze DataFrame.

2️⃣ Silver Layer — Cleaning & Transformation

Duplicate rows removed.

Skills extracted and split into arrays; exploded to have one skill per row.

Salary fields cleaned and normalized to numeric values.

Year extracted from listed time.

Optional country extraction method included (requires more compute).

3️⃣ Gold Layer — Aggregation & Analytics

Aggregations performed on the silver data to produce insights:

Jobs per company

Jobs per year

Average / min / max salaries per company

Top skills by job count

Jobs per pay period

💾 Sample Outputs

Bronze Layer Preview

job_id	company_name	title	normalized_salary	skills_desc	listed_time_readable
3906267224	ABC Corp	Data Engineer	120000	python, sql	2024-01-15

Silver Layer Preview

job_id	company_name	title	skill	normalized_salary	year
3906267224	ABC Corp	Data Engineer	python	120000	2024
3906267224	ABC Corp	Data Engineer	sql	120000	2024

Gold Layer Preview

company_name	job_count	avg_salary	min_salary	max_salary
ABC Corp	15	115000	95000	135000
⚙️ How to Run

Upload your datasets to Databricks Volumes (free edition) or S3.

Open the provided notebook: job_pipeline_databricks_notebook.ipynb.

Run all cells sequentially:

Load and merge datasets → Bronze layer

Clean and transform → Silver layer

Aggregate metrics → Gold layer

Optionally, explore skills_desc and other columns with display() for interactive inspection.

💡 Tip: For larger datasets or advanced country extraction, a larger cluster is recommended.

📊 Skills Demonstrated

PySpark DataFrames and transformations

Data cleaning, type casting, and null handling

Merging multiple datasets with different schemas

Skills extraction and normalization

Aggregations for business insights (jobs, salaries, skills)

Handling large real-world CSV datasets efficiently

🔗 Next Steps / Enhancements

Integrate with AWS S3 for automated ETL pipelines.

Implement dynamic country extraction using GeoText + country_converter for location standardization.

Extend analysis with salary trends, remote jobs, and skill demand visualization using Streamlit or Power BI.

🎯 Status

✅ Project fully functional on free Databricks cluster (Bronze → Silver → Gold).
⚠️ Advanced location-to-country mapping requires more resources and is included as a method for future enhancement.
