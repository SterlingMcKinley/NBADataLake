# NBADataLake
This repository contains the setup_nba_data_lake.py script, which automates the creation of a data lake for NBA analytics using AWS services. The script integrates Amazon S3, AWS Glue, and Amazon Athena, and sets up the infrastructure needed to store and query NBA-related data.

# Overview
The setup_nba_data_lake.py script performs the following actions:

Creates an Amazon S3 bucket to store raw and processed data.
Uploads sample NBA data (JSON format) to the S3 bucket.
Creates an AWS Glue database and an external table for querying the data.
Configures Amazon Athena for querying data stored in the S3 bucket.

<p>In this project, I made an attempt to utilize AWS CloudShell but I ran into issues with code syntax/indentation of code. I tried to fix the syntax of the entire python file but I would have wasted time reviewing vi editor. I also tried to upload the code file and I faced the same syntax indentation errors. To complete this project, I utilzed AWS CLI.</p>

# Prerequisites
Free account with subscription and API Key at sportsdata.io
Personal AWS account
Python understanding

## **Technologies**
- **Cloud Provider**: AWS
- **Core Services**: S3, Amazon Glue, Amazon Athena
- **External API**: NBA Game API (SportsData.io)
- **Programming Language**: Python 3.x
- **IAM Security**:
  - Least privilege policies for S3, Glue, and Athena.

### **Setup Instructions**
# 1. Clone NBADataLake repo

git clone https://github.com/alahl1/NBADataLake.git

# 2. Create .env file for the below variables

SPORTS_DATA_API_KEY=your_sportsdata_api_key
NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players

# 3. Modify Python script
Find API key references and add your SportsDataIO api key
Change to a unique S3 bucket name

# 4. Execute the script 
python3 setup_nba_data_lake.py

Script results:

![script_results](https://github.com/user-attachments/assets/936a77c3-a316-4366-be28-d4363af00a9c)

![s3bucket](https://github.com/user-attachments/assets/84616d7e-047d-4c61-a019-837418a9e5df)

![aws_glue](https://github.com/user-attachments/assets/146bf3f3-2ae7-4b20-924f-4163fd96b9c3)

# 5. Manually check resources

-Query the Data w/ AWS CLI and/or AWS Athena

```
aws athena start-query-execution --query-string "SELECT FirstName, LastName, Position, Team FROM nba_players WHERE Position = 'PG';" --query-execution-context Database="
glue_nba_data_lake" --result-configuration OutputLocation="s3://sterling-sports-analytics-data-lake/"
```
The command/query will produce an QueryExecutionId
![query_executioners_id](https://github.com/user-attachments/assets/7e3322fe-bf81-4fe5-80cc-e26ff2824d58)


![athena_queries](https://github.com/user-attachments/assets/44a78de4-caec-42c7-be4f-3b5da4a9c428)

Copied query data from s3 bucket vi aws cli

```
aws s3 cp s3://sterling-sports-analytics-data-lake/ . --recursive
```

![download_query_files](https://github.com/user-attachments/assets/d09d0855-c851-4873-b380-cc7e6ae23803)


![Athena_query_resutls](https://github.com/user-attachments/assets/0d89b622-4d43-43fd-aa57-f6c634014727)


Query via Amazon Athena

```
SELECT FirstName, LastName, Position, Team FROM nba_players WHERE Position = 'PG'
```

![Athena_query_results](https://github.com/user-attachments/assets/f53c3ac6-7b61-44c9-bde3-795a349bc915)

### **Project Reaction**
<p>I enjoyed this project. I learn more about my favorite AWS CLI (hahaha) and querying athena/s3 using aws cli. I truly love to complete tasks via CLI. I spent time reviewing Python code and understanding different methods of getting creating services (boto3), api calls, as well as delimiting data.</p>
