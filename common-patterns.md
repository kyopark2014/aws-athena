# Athena 사용 패턴

Athena를 활용하여 데이터를 분석하는 4가지 패턴에 대해 설명합니다.

## Ad-hoc use case

Amazon Redshift, S3에 저장되어 있는 데이터 뿐 아니라, Amazon RDS나 EC2의 Database의 데이터는 AWS Glue Data Catalog를 통해 Discovery될 수 있습니다. 이때 AWS Glue ETL을 통해 데이터를 전처리하거나 Athena, Redshift spectrom, EMR을 통해 분석할 수 있습니다. 분석된 데이터는 그래프와 같은 BI를 통해 비지니스에 활용됩니다. 



![image](https://user-images.githubusercontent.com/52392004/184464828-85ce517e-e2dd-4afa-b0d5-7a91d3d49fef.png)


## SaaS use case

API Gateway와 같이 외부에서 사용할 수 있는 API제공할때, warm 또는 cold data의 경우에 athena를 통해 S3의 데이터를 로드하는 방식으로 제공할 수 있습니다. 이때, S3의 데이터를 테이블화하기 위하여 AWS Glue data catalog가 활용됩니다. 

![image](https://user-images.githubusercontent.com/52392004/184464900-5b0a8cc8-0486-4e53-82b2-0161ee812f47.png)


## ETL and query use case

AWS 서비스나 사용자가 만든 Application에 대한 로그 및 외부 벤더들이 제공하는 로그들은 S3에 경제적으로 저장할 수 있습니다. S3의 데이터는 Athena CTAS와 INSERT INTO to ETL을 통해 다른 S3 bucket에 저장될수 있고, 이러한 데이터는 AWS Glue Data Catalog를 통해 Table화되어서 Athena로 SQL로 query를 할 수 있습니다. 


![image](https://user-images.githubusercontent.com/52392004/184464977-248d6331-6f61-4b72-9d0d-05e6340042e9.png)

## Data science exploration and feature engineering

대표적인 AI/ML분석툴인 SageMaker는 Athena를 통해 S3의 데이터를 조회하여 Machine Learnig 작업을 수행할 수 있습니다. 

![image](https://user-images.githubusercontent.com/52392004/184465005-ec1d1212-10d4-4eb6-94d2-57f95e1f9cb2.png)
