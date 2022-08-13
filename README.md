# AWS Athena

Athena는 서버리스 환경에서 Data Lake를 위한 interative query를 제공합니다.

![image](https://user-images.githubusercontent.com/52392004/184464605-c71155b2-b466-42e1-86e7-a17358322b25.png)


## 특징

#### Simplicity

- serverless이므로 초기 설정이나 인프라 비용이 발생하지 않습니다.
- SQS를 이용해 S3와 저장된 데이터를 query할 수 있습니다.
- JDBC/ODBC driver들을 제공합니다. 

#### Pay per query

- 데이터를 scan할때에만 비용이 발생합니다.
- 압축을 통해 30-90%의 query비용을 절감할 수 있습니다. 

#### Decouple storage and compute

- 데이터저장소와 Query를 위한 인프라가 분리되어 있습니다.
- S3, Data warehouse와 database에 대한 Query를 제공합니다.
- 다양한 custom 데이터나 포맷에 호환가능합니다.

#### Security

- 전송(Transit)에서 암호화합니다.
- AWS IAM 및 SALv2에 대한 인증을 제공합니다.
- AWS PrivateLinke를 지원합니다. 

## 일반적인 사용 패턴

[Common Patterns](https://github.com/kyopark2014/aws-athena/blob/main/common-patterns.md)에서는 Athena를 사용하는 패턴에 대해 설명합니다. 


## Reference

[MakeMyTrip: Leveraging Athena Federated Query to break data silos], Reinvent 2021 ANA301
