
![](https://i.imgur.com/bbA3V3Y.png)
![](https://i.imgur.com/XTiIemy.png)
https://game.alienattack.ninja/ 게임링크

### 간단한 설명
서버리스로 위의 아키텍처 다이어그램을 만들게 될거임
EC2안쓰면 서버리스?ㅋㅋㅋ EC2는 설정, 관리해야함..
관리를 AWS에 떠넘기는게 서버리스임 (Container를 사용해도, Fargate같은걸 쓰면 서버리스로 사용 할 수 있음)

### Getting Started
Alient Attack : 게이머의 점수와 상태 데이터 포인트를 생성하는 이벤트 소스 역할을 합니다.
새 IAM 사용자 : Sungho :  콘솔 로그인 URL https://727502603431.signin.aws.amazon.com/console


- **AWS Cloud Development Kit (CDK)** : AWS Alien Attack은 인프라 배포를 위해 AWS CDK를 사용하여 구축되었습니다. CDK에 대한 자세한 내용은 다음을 참조하십시오.["What is CDK"](https://docs.aws.amazon.com/CDK/latest/userguide/what-is.html) , 그외에 [github repository](https://github.com/awslabs/aws-cdk) 참고하시고 [AWS CDK Workshop](https://cdkworkshop.com/) 도 참고하십시요.
- **AWS Cloud9** : Cloud9는 "개발 환경"이 될 것입니다. 가격을 포함하여 Cloud9에 대해 자세히 알아 보려면[here](https://aws.amazon.com/cloud9/) 참고하세요. Cloud9는 프리 티어를 제공합니다.
- **Amazon Cognito** : Cognito를 사용하여 AWS Alien Attack에 식별 및 인증 서비스를 제공합니다. 가격을 포함하여 Cognito에 대해 자세히 알아 보려면 [here](https://aws.amazon.com/cognito/)  참고하세요. Cognito는 프리 티어를 제공합니다.
- **AWS Identity and Access Management (IAM)** : AWS IAM을 사용하면 AWS 리소스에 대한 액세스를 생성하고 관리 할 수 ​​있습니다. Alien Attack의 경우 Cognito와 함께 역할 및 정책을 사용하여 사용자에게 적절한 권한을 제공합니다. Cognito 및 IAM을 사용하면 RBAC (Role-Based Access Control)를 사용하여 식별, 인증 및 권한 부여를 처리 할 수 ​​있습니다. IAM에 대한 자세한 내용은 [here](https://aws.amazon.com/iam/) 참고하세요. IAM은 무료로 사용할 수 있습니다.
- **Amazon Simple Storage Service (S3)** : S3는 웹 사이트를 호스팅하고 분석 목적으로 들어오는 원시 데이터를 저장하는 데 사용됩니다. 그것에 대해 더 읽어보기 [here](https://aws.amazon.com/s3/) . S3는 프리 티어를 제공합니다.
- **Amazon API Gateway** : API Gateway는 게이머와 백엔드 간의 인터페이스 역할을 할 REST API를 구축 할 수있는 기능을 제공합니다. 자세한 내용은 [here](https://aws.amazon.com/api-gateway/)  참고하세요. API Gateway는 프리 티어를 제공합니다.
- **AWS Lambda** : Lambda는 처리 계층의 기반입니다. 이를 통해 서버를 프로비저닝하지 않고도 코드를 실행할 수 있습니다. 자세한 내용은 [here](https://aws.amazon.com/lambda/)  참고하세요. Lambda는 프리 티어를 제공합니다.
- **Amazon Kinesis Data Streams (KDS)** : KDS는 스트리밍 데이터를 수집하는 데 사용됩니다. 요금을 포함하여 Kinesis Data Stream에 대한 자세한 내용은 다음을 참조하십시오.[here](https://aws.amazon.com/kinesis/data-streams/) . Kinesis Data Streams에는 프리 티어가 없지만 이 애플리케이션에 대한 비용 (사용자 1 명)의 경우 Kinesis Data Streams와 관련된 비용은 대략 시간당 1 센트입니다.
- **Amazon Kinesis Data Firehose** : Amazon Kinesis Data Firehose는 스트리밍 데이터를 데이터 스토어 및 분석 도구에 로드하는 가장 쉬운 방법입니다. 스트리밍 데이터를 캡처, 변환 및 Amazon S3, Amazon Redshift, Amazon Elasticsearch Service 및 Splunk로로드 할 수 있으므로 현재 이미 사용중인 기존 비즈니스 인텔리전스 도구 및 대시 보드를 통해 거의 실시간 분석이 가능합니다. Kinesis Data Streams에서 데이터를 삭제하는 데 사용하고 있습니다. 가격을 포함하여 Kinesis Data Firehose에 대해 자세히 알아 보려면 [here](https://aws.amazon.com/kinesis/data-firehose/) . Kinesis Data Firehose 에는 프리 티어 가 없지만이 애플리케이션을 테스트하는 비용은 무시할 수 있습니다. 자세한 내용은 가격 모델을 확인하십시오.
- **Amazon DynamoDB** : DynamoDB를 사용하여 게임 세션의 점수 판 데이터를 저장합니다. Amazon DynamoDB는 모든 규모에서 한 자릿수 밀리 초의 성능을 제공하는 키-값 및 도큐먼트 데이터베이스입니다. 보안, 백업 및 복원, 인터넷 규모 애플리케이션을 위한 인 메모리 캐싱이 내장 된 완전 관리 형 멀티리전 멀티 마스터 데이터베이스입니다. DynamoDB는 하루에 10조 개 이상의 요청을 처리 할 수 ​​있으며 초당 2천만 개 이상의 최대 요청을 지원할 수 있습니다. DynamoDB는 프리 티어를 제공하며 Alien Attack을 위해 그 하에서 실행될 것입니다. 자세한 내용은 [this link](https://aws.amazon.com/dynamodb/) .
- **AWS Systems Manager** : Systems Manager는 통합 사용자 인터페이스를 제공하므로 여러 AWS 서비스의 운영 데이터를보고 AWS 리소스 전체에서 운영 작업을 자동화 할 수 있습니다. 우리는매개 변수 저장소데이터베이스 문자열과 같은 일반 텍스트 데이터 또는 암호와 같은 비밀 여부에 관계없이 구성 데이터를 관리 할 수있는 중앙 저장소를 제공하는 Systems Manager의 기능입니다. 가격을 포함하여 Systems Manager에 대한 자세한 내용은 다음을 참조하십시오.[here](https://aws.amazon.com/systems-manager/) . Parameter Store는 무료입니다.
- 프로그래밍 관점에서, 우리는 [AWS SDK for Javascript in the Browser](https://aws.amazon.com/sdk-for-browser/)  와 [AWS SDK for Node.js](https://aws.amazon.com/sdk-for-node-js/) 를 사용합니다.

### 환경세팅
Cloud9 콘솔 - 환경 생성 - AlienAttackWorkshop으로 이름설정
이제 Cloud9 콘솔 열어서 밑에 수행

```
git clone https://github.com/aws-samples/aws-alien-attack
```
하면 , application은 프론트엔드 , infrastructure는 백엔드임

CHOAAA635853

- 지속적인 컴파일 방식 : 파일 변경마다 환경이 자동으로 컴파일됨. 따로 새 터미널 띄워서, infrastructure/cdk 폴더에서 `npm run watch`로 감시하는거인듯
- 환경을 synthesize하고, deploy (S3버킷 어쩌구)
- Outputs :
```bash
CHOAAA635853.apigtw = https://tvys65m4v2.execute-api.ap-northeast-2.amazonaws.com/prod/v1/
CHOAAA635853.envname = CHOAAA635853
CHOAAA635853.region = ap-northeast-2
CHOAAA635853.resetpassurl = https://choaaa635853.auth.ap-northeast-2.amazoncognito.com/forgotPassword?client_id=6ae3h8idgcf5a51bbvr2bvilmc&response_type=code&redirect_uri=https%3A%2F%2Fexample.com
```
> synthesize 명령은 _YOUR_ENVIRONMENT_NAME.app_ 및 _YOUR_ENVIRONMENT_NAME.raw_라는 두 개의 S3 버킷도 생성합니다. 확인하려면 Amazon S3 콘솔을 방문하십시오.

3 AM Coding Session - Lofi Hiphop mix

nickname은 username1 
password는 Password!123

user pool ID : ap-northeast-2_MTYuWrdHr
```
aws cognito-idp admin-add-user-to-group --user-pool-id ap-northeast-2_MTYuWrdHr --username username1 --group-name Managers --region ap-northeast-2
```

S3 버킷 - 접미사 `raw` 가진 버킷의 ARN 복사 : arn:aws:s3:::choaaa635853.raw



LEVEL 2 : 리더보드 추가하기. Websocket
CHOAAA635853API ARN : arn:aws:iam::138037825876:role/CHOAAA635853API

websocket URL : wss://my2hjixnv1.execute-api.ap-northeast-2.amazonaws.com/prod/```
cdk delpoy -c envname=$envname -c sessionparameter=true
```