# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a Jupyter notebook analysis titled "Beyond the AI Hype: Measuring Real Developer Productivity Gains from Coding Assistants". The project uses GitHub events analytics via BigQuery to quantify genuine productivity improvements from AI coding assistants, distinguishing them from AI-generated code bloat.

**Main notebook**: `beyond-the-ai-hype-measure-developer-productivity.ipynb`

## Environment Setup

This project is designed to run on **Kaggle** with the following dependencies:

```bash
%pip install --upgrade bigframes google-cloud-automl google-cloud-translate google-ai-generativelanguage tensorflow
```

### Required Credentials

The notebook uses Kaggle Secrets for GCP authentication:
- Google Cloud credentials are accessed via `kaggle_secrets.UserSecretsClient()`
- BigQuery project ID: `big-query-project-472510`

### BigFrames Configuration

The project uses BigFrames (BigQuery DataFrames) with these settings:
- **Ordering mode**: `partial` (for performance optimization)
- **Blob display width**: 300
- **Progress bar**: Disabled
- **Warning suppression**: `AmbiguousWindowWarning` is ignored

## Architecture

### Data Sources
- **GitHub Events Data**: Accessed via BigQuery public datasets
- Analysis focuses on commit patterns, code changes, and developer activity metrics

### Analysis Framework
The notebook uses BigFrames (BigQuery DataFrames API) as the primary data processing framework:
- `bigframes.pandas` provides a pandas-like interface for BigQuery
- Queries run directly on BigQuery, enabling large-scale data analysis
- Results are lazy-evaluated for efficiency

### Key Components
1. **Data Ingestion**: GitHub events data from BigQuery public datasets
2. **Metric Calculation**: Developer productivity metrics derived from event patterns
3. **AI Impact Analysis**: Statistical methods to separate AI-assisted productivity from code bloat
4. **Visualization**: Results presented within the notebook

## Running the Analysis

### On Kaggle (Recommended)
1. Upload the notebook to Kaggle
2. Enable internet access in notebook settings
3. Add Google Cloud credentials to Kaggle Secrets
4. Run all cells sequentially

### Local Development
Note: This notebook is optimized for Kaggle. Local execution requires:
- Valid GCP credentials with BigQuery access
- Modify authentication code to use local credentials instead of `kaggle_secrets`
- Ensure BigQuery API is enabled in your GCP project

## Data Processing Notes

- The analysis uses **partial ordering mode** in BigFrames to accelerate query execution and reduce costs
- Warning suppression is enabled for `AmbiguousWindowWarning` - these are expected in the analysis workflow
- BigQuery project must have access to GitHub Archive public datasets

## Project Structure

```
Github-Analysis/
├── beyond-the-ai-hype-measure-developer-productivity.ipynb  # Main analysis notebook
└── Screenshot/                                               # Supporting images/screenshots
```

## Important Considerations

- **BigQuery Costs**: Queries run against BigQuery will incur costs based on data processed
- **GitHub Archive Dataset**: The analysis likely uses the `githubarchive` public dataset which contains billions of events
- **Kaggle Environment**: The notebook is specifically designed for Kaggle's infrastructure and secret management
