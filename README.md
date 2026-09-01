# NOAA weather project on AWS

This project uses NOAA weather data from the Registry of Open Data on AWS to teach S3, pandas, Parquet, AWS Glue, Athena, matplotlib, and optional Amazon Bedrock.

Run the notebooks in order:

1. `01_build_pipeline.ipynb` creates the AWS resources and builds the data pipeline.
2. `02_query_and_visualize.ipynb` queries Athena, compares CSV with Parquet, and creates charts.
3. `03_bedrock_report.ipynb` is optional. It asks a Bedrock model to summarize calculated results.

This project creates AWS resources and may incur small charges. Run the cleanup cell in Notebook 2 and stop SageMaker compute when finished.

## Project files

```text
.
├── 01_build_pipeline.ipynb
├── 02_query_and_visualize.ipynb
├── 03_bedrock_report.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Run locally in your AWS account

You need Python 3.11 or newer and AWS CLI 2.32.0 or newer.

### Sign in with AWS Console credentials

For local development with an existing AWS Management Console identity, use the current `aws login` flow from a terminal:

```bash
aws --version
aws login
aws sts get-caller-identity
```

Install the notebook environment, then launch Jupyter or your IDE from the same terminal:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

## Run in SageMaker

Clone this repository into a SageMaker Jupyter environment, then work through the notebooks in the order listed above. The Bedrock notebook is optional.

## How it works

Notebook 1 copies NOAA CSV files from public S3 into a raw layer, cleans and validates them with pandas, and writes partitioned Parquet to a curated layer. AWS Glue catalogs both layers, Notebook 2 queries them with Athena and creates charts with matplotlib, and Notebook 3 can turn the calculated results into a Bedrock report.

## Data source

The project uses [NOAA Global Surface Summary of the Day](https://registry.opendata.aws/noaa-gsod/) from the Registry of Open Data on AWS. NOAA requests attribution when unaltered data is used or shared.
