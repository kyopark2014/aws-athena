# Athena Federated Query

Atehna의 Federated Query를 이용하면 RDB, No-SQL, Object 스토리지나 사용자 정의 데이터 소스에 대한 Query를 수행할 수 있습니다. 이를 이용해 On-Premise나 다른 Cloud 데이터 소스에 대해서도 Query 할 있어서, 데이터분석이나 복잡합 파링프라인이나 어플리케이션을 분석하는데 이용할 수 있습니다. 

<img width="523" alt="image" src="https://user-images.githubusercontent.com/52392004/184465331-c312859f-9f9d-4272-acdb-7d86955a123b.png">

Federated query는 AWS Lambda를 통해 Federated data souce를 조회하게 됩니다. 


![image](https://user-images.githubusercontent.com/52392004/184465501-eeed9436-6e48-4e9e-a607-22d4a8d34cab.png)


## Use case: Join transactional data with logs

아래와 같이 RDB에 있는데 데이터와 CloudWatch의 로그를 아래처럼 Query 할 수 있습니다. 

![image](https://user-images.githubusercontent.com/52392004/184466443-6e7edcf4-6fc6-4af7-8db2-bfc0289f651b.png)

```sql
WITH order_logging AS (
  SELECT
    REGEXP_EXTRACT(…) AS order_id,
    REGEXP_EXTRACT(…) AS log_level
  FROM cwl."/var/lambda/order-processor"
)
SELECT orders.order_id, logs.message
FROM active_orders orders
  LEFT JOIN order_logging logs
  USING (order_id)
WHERE logs.log_level = 'ERROR’
  AND FROM_UNIXTIME(logs.time / 1000) >
      NOW() – INTERVAL '1' DAY
  AND orders.order_status = 'aborted'
  AND orders.order_date >
      NOW() – INTERVAL '1' DAY 
```

## Data Souce 연결 방법

1) Discover: data source connector를 deploy 합니다.

<img width="307" alt="image" src="https://user-images.githubusercontent.com/52392004/184465579-62e4503d-62ed-4b32-a87a-712424fd8ba5.png">


2) Select: data socue connector를 athena에 등록합니다. 이때 catalog name을 입력합니다.

<img width="333" alt="image" src="https://user-images.githubusercontent.com/52392004/184465584-7e2c6a24-9662-4a27-aed5-ff20bbc8e614.png">

3) Query: <CatalogName>.Database.Table로 SQL Query를 수행합니다. 

<img width="374" alt="image" src="https://user-images.githubusercontent.com/52392004/184465589-c5013299-48a9-475b-a79d-74b6b049252e.png">

## 사용가능한 Data Socue의 종류

최신 소스는 [Amazon Athena Query Federation](https://github.com/awslabs/aws-athena-query-federation)을 참조합니다. 
  
- AWS CMDB
- Amazon Timestream
- Amazon Neptune
- Hbase
- Amazon DocumentDB
- Amazon DynamoDB
- JDBC
- Amazon Elasticsearch
- CloudWatch Logs
- CloudWatch Metrics 
- TPDS Data Generator
- Vertica
- Redis


## Reference   

[Amazon Athena Query Federation](https://github.com/awslabs/aws-athena-query-federation)
