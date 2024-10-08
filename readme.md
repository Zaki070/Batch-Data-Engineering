# Batch-Data-Engineering
The goal is to construct a data pipeline that populates the user_behavior_metric table. This table is an OLAP table designed for use by analysts, dashboard applications, and similar tools. The data for this table is derived from the user_purchase table, which is an OLTP table containing user purchase information, and from movie_review.csv, a daily data file provided by an external vendor.
![Project Table](https://github.com/Alero-Awani/Batch-data-engineering-project/blob/master/images/de_proj_obj.png?raw=true)

# Table of contents
1. [Pipeline Workflow](#Pipeline)
2. [Terraform setup](#Terraform)
3. [Airflow/Airflow Configurations](#Airflow)


## Pipeline Workflow <a name="Pipeline"></a>
### User Purchase Data
* The user purchase data is extracted from an OLTP database and ingested into the Redshift data warehouse. AWS S3 serves as the storage solution, enabling integration with AWS Redshift Spectrum for a data lakehouse approach. By utilizing Redshift Spectrum, data can be queried directly from S3 on Redshift through the creation of an external schema, facilitated by AWS Glue.

### Movie Review Data
* The movie review data is initially loaded into a staging area within an S3 bucket, where it becomes accessible to AWS EMR. Alongside this data, a Spark script is executed to perform basic text classification. After processing, the classified data is stored back into the S3 bucket.

### User Behaviour Metric Table
* In Redshift, the processed movie review data is combined with the user purchase data to generate the user_behavior_metric table. This table provides valuable insights by merging these two data sources.

## Terraform setup <a name="Terraform"></a>
![Terraform Plan](https://github.com/Alero-Awani/Batch-data-engineering-project/blob/master/images/terraform_visual.png?raw=true)

### overview
* This pipeline requires us to setup Apache Airflow, AWS EMR,AWS Redshift, AWS Spectrum, and AWS S3, AWS EC2.
* The EC2 instance and has docker and docker-compose installed on it through the use of user-data.tpl, This helps in setting up the Airflow with the docker-compose yaml file
* The yaml file also contains a Postgres container and a metabase container for visualization

### Setting up Infrastructure
Generate a key pair
```
ssh-keygen -t ed25519
```
Prepare the working directory
```
terraform init
```
To Preview the changes terraform plans to make to your infrastructure.
```
terraform plan
```
To execute the actions proposed in the terraform plan and create the resources.
```
terraform apply
```
To terminate the resources.
```
terraform destroy
```




## Airflow/Airflow Configurations <a name="Airflow"></a>
![Airflow Dag](https://github.com/Alero-Awani/Batch-data-engineering-project/blob/master/images/Airflow%20dag.png?raw=true)











