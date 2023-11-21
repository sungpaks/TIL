### 트랙2 서버리스
#### 1세션 :
영어임 ㄷㄷㄷ 개요인듯
aws Lambda : 서버리스 함수
aws Fargate : 서버리스 컨테이너

#### 서버리스 ?
https://dev-coco.tistory.com/171
https://aws.amazon.com/ko/serverless/
백엔드 코드는 평소에 자고있고, 요청이 들어오면 서버가 코드를 깨워 처리하고 다시 재운다
- FaaS(Function as a Service) : 함수를 서비스로 제공함. AWS Lambda 등
- BaaS(Backend as a Service)
보통 FaaS

#### 2세션 : 모던 프론트엔드 개발자가 꼭 알아야 할 서버리스 서비스들
- Modern Web Application
	이전엔 CSR : static HTML?을 던져주는 정도였음 서버는
	요즘 SSR : HTML던져주는 것 뿐만아니라, 함수도 실행하고 등등 동적임
	Micro Architecture : 각 서비스를 기능, 팀별로 쪼갰다. 각 마이크로서비스를 여러 인프라 위에 세우게 되었다
- 서버리스란?
	
- AWS Amplify 
	간단하게 웹 앱 호스팅
	빠르게 풀스택 서비스를 구축하기 좋은듯
	서버리스 기반.. 
	amplify UI라는 라이브러리도 있고
	amplify studio - backend 머시기 
	docs.amplify.aws/console
	간단하게 (피그마 연동 등) 어느정도의 스케치를 따줄 수 있다는 것임
	
-  AWS lambda
	- cold start : 언어별 지연시간이 좀 상이하다
	=> 람다함수를 5분마다 호출하는 방법이 좀 대중적임
		물론 다 비용임ㅋㅋ
	람다 : 요청 발생 시점에 인스턴스를 로드하고
		코드 다운로드 -> 새 컨테이너 시작 -> runtime -> 코드 시작
		이 코드 시작 직전까지가 cold start임
	- snap start? 스냅샷에서부터 함수를 재개한다
		java 11 17전용임 ㅋㅋ 
- API Gateway
	- MSA => 각 마이크로 서비스를 독립적으로 컨테이너에 올려야하고, 공통동작의 API를 따로따로 개발하는 등.. 관리할 엔드포인트가 많아진다 이걸 API gateway로 해결??
	- Authentication / Authorization
	- Routing / Load Balancing
	- Service Discovery
	- 엔드포인트 하나로 모두 관리할 수 있게 됨 

#### SAM 도와주세요~~~
AWS lamdba를 로컬에서 테스트할수는 없을까?
어떻게하면 분산된 AWS lambda를 통합관리할 수 있을까?

AWS SAM으로 이벤트 트리거를 대체?? S3 bucket으로 가던 것을..
`template.yaml` 에 S3 bucket을 명시하는 것처럼 

SAM : 서버리스를 위한 머시기 IaC : infrastructure as code
template.yaml에서, `Type:AWS::Serverless::Function` 이런식

영상 업로드 : API gateway -> -> S3 버킷 가던것을
API gateway를 SAM으로 대체하고, LocalStackS3로 S3버킷을 대체함

Docker compose를 활용하여 로컬스택을 띄우겠습니다
image는 localstack의 공식 이미지를, environment에는 SERVICES=s3
엔드포인트를 LocalStackS3로 설정해서, 45포트로 내부통신하게끔

"그냥 직접 업로드하면 안됨??"
람다는 6메가바이트보다 페이로드가 작다
더 큰 경우 S3 서명된 URL 사용

사용자가 데이터를 전달 -> API gateway를 거쳐 전달되고, lambda 서비스를 통과하고, 함수 소스코드에 도달하게 됨.
이 때 lambda 서비스->함수에 Runtime API가 있는거고
AWS SAM이 API gateway를 대체하는것임

#### 4세션 : 서버리스에서 부하테스트 하는 이유
부하테스트란?? 특정 조건에서 시스템 또는 워크로드에 부하를 걸어 처리능력을 측정하고, 운용 가능성에 대해 릴리스 전에 검증하는 테스트임

근데 AWS의 매니지드 서비스를 이용하는 서버리스에서 굳이 부하테스트를?
1. 서버리스 비용 미리 파악 : 종량제라서 요금 계산이 복잡하니까 견적내기 어려워여
	=> 실제 비용을 "발생시켜서" 확인해보기 : 비용 할당 태그
2. 서비스 할당량 추가 요청을 위한 근거 수집.
	=> 병목 현상이 생기는 부분을 미연에 파악함
3. 최적화와 성능 튜닝
	=> 결과를 보고 대응수단 고려
Throttling : 버스트 동시성은 일반적 동시 실행 수와 다르다

툴? Apache JMeter, Serverless-artillery, 등.. 또는 AWS 분산로드테스터 등
주의 : 부하는 점진적 증가하기, 로그or트레이싱 등 요금 부분에 유의, 연계 시스템은 Mock으로 사전에 대체하는 등 준비하기

#### Amazon EventBridge를 활용한 Event-Driven 아키텍처
- Event-Driven 아키텍처 : 이벤트를 활용하여 분리된 서비스들을 연결하거나 실행(트리거)시킨다
- aws Lambda 자체도 **이벤트 중심**임.
- "이벤트"? 명령이 아닌, 관찰한 내용
- Event-Driven 아키텍처의 구성요소 : 이벤트 소스, 이벤트 라우터, 이벤트 대상
	이벤트가 발생하면, 이벤트 라우터가 적재적소의 대상으로 보낸다
- EventBridge? 머시기머시기..이벤트버스임
	- 이벤트 버스 ? 발생한 이벤트를 받고 전달하는 라우터. 규칙을 활용하여 이벤트를 선별하고, 알맞은 대상에 전달
- 파이프 : 이벤트소스와 대상을 포인트-포인트로 연결하는 서비스.
	이벤트를 '강화'할 수 있음. 예를들면, 주소를 입력하면 외부API를 통해 우편번호를 알아오고, 이걸 함께 이벤트대상으로 전달하는 등
- cron : 분단위로 스케줄처리, 예약, 등..
- 근데 cron은 분단위인데 , 초단위로 하고싶으면? SQS delay머시기가 있는데, 몇초 단위로 interval을 넣고 큐에 몰아넣는다



[[서버리스]]
