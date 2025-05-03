# Enhanced ETL Pipeline with AWS S3 and MySQL RDS

## 📌 Overview

This project implements an **Enhanced ETL (Extract, Transform, Load)** pipeline using **Python**, **AWS S3**, and **MySQL RDS**. It extracts data from multiple file formats (CSV, JSON, XML), transforms the data (e.g., unit conversions), loads the transformed data into both a **CSV file** and a **MySQL RDS database**, and utilizes **AWS S3 buckets** for source and result storage.

---

## ⚙️ Technologies Used

- Python 3.x
- AWS S3 (boto3)
- MySQL RDS (mysql-connector-python, SQLAlchemy, PyMySQL)
- pandas
- Jupyter Notebook / Python Script

---

## 🔧 Setup & Installation

### 🐍 Python Dependencies

Install the required Python libraries:

```bash
pip install boto3
pip install mysql-connector-python
pip install pymysql
```
☁️ AWS Setup
Create two S3 buckets:

my-etl-project-source (for source files)

my-etl-project-transformed (for transformed outputs)

Provide valid AWS credentials:
AWS_ACCESS_KEY = "YOUR_ACCESS_KEY"
AWS_SECRET_KEY = "YOUR_SECRET_KEY"


🛢️ MySQL RDS Setup
Create a MySQL RDS instance and update the following in your script:

RDS_ENDPOINT = 'your-rds-endpoint'
RDS_PORT = '3306'
RDS_USER = 'admin'
RDS_PASSWORD = 'your-password'
RDS_DB = 'etlproject3'

🔄 ETL Pipeline Workflow
Extract

Reads data from .csv, .json, and .xml formats using pandas and ElementTree.

Transform

Converts height from inches to meters and weight from pounds to kilograms.
```bash
def transform_data(df):
    #Transform the data (e.g., unit conversions, cleaning).
    log_message("Starting data transformation")
    # Convert heights to meters and weights to kilograms
    for col in df.columns:
        if col.lower() =='height':
            df['height_in_meters'] = (df[col].astype(float) * 0.0254).round(2)
            df.drop(columns=[col], inplace=True)
        if col.lower() =='weight':
            df['weight_in_kilograms'] = (df[col].astype(float) * 0.453592).round(2)
            df.drop(columns=[col], inplace=True)
    log_message("Data transformation completed")
    return df

```
Load

Saves the transformed data into a local CSV file.

Uploads the transformed file to an S3 bucket.

Loads data into a MySQL RDS database table (User_Data).

Logging

All actions and errors are logged in log_file.txt.

📒 Notes
* Ensure your AWS IAM user has appropriate S3 permissions.

* All logs are stored in log_file.txt.

* Replace hardcoded secrets with environment variables in production.

