# Airflow Slack Operator

This provides a module and example usage for an Airflow Slack alert operator. It uses the code shown in Kaxil Naik's 
[Integrating Slack Alerts in Airflow](https://medium.com/datareply/integrating-slack-alerts-in-airflow-c9dcd155105) 
Medium article, with some minor additions and example code. 

# Usage

This assumes you already have Airflow running. 

## Install Slack Webhooks
Follow the article [Integrating Slack Alerts in Airflow](https://medium.com/datareply/integrating-slack-alerts-in-airflow-c9dcd155105) and install the necessary Webhooks and API key into your Airflow connections. Perform this on your deployed Airflow configuration.

## (Optional) Initial Local Tests
These are optional, but helps ensure a healthy DAG before launching it. Run these on a local airflow instance before saving them to a final deployed one.

1. Install airflow locally: `pip install -r requirements.txt`. This gives you access to `airflow` commands in later steps.
2. Copy the contents of `dags` into your local airflow `dags` directory
3. Confirm DAG compiles with: `python dags/dag_coin_flip.py`
4. Confirm it can be bagged: `airflow initdb`.
5. Confirm the task can be run: `airflow test hourly_coin_flip coin_flip 2019-01-01`
   - Run this a couple times. Sometimes it should raise a ValueError (forced fail), i.e. "flipping tails". Sometimes it will raise `airflow.exceptions.AirflowException: The conn_id `slack` isn't defined`, because this is a local Airflow without Slack hooked in.


## Installation
Similar to other Airflow DAGs, just copy the contents of `dags` into your deployed Airflow `dags` directory.