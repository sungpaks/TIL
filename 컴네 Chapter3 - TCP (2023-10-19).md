오늘 내용까지만 시험범위
### review 
#### rdt3.0 : 손실 고려. 
	손실 : sender가 보낸걸 receiver가 못 받거나, receiver가 보낸 ACK응답을 sender가 못 받거나 등. 
	손실이 발생하면, 이전에 2.x에서 에러 상황에 대해 했듯이 재전송
	근데 detection이 추가 되어야 함.. ***reasonable amount of time***을 기다려보고, timeout을 감지한다
- fdm : 기본적으로, `rdt_send` 이후 `start_timer` => ACK받으면 `end_timer`
	- ACK가 안오면 timeout : 재전송하고 `start_timer`
	- 알맞은 seq#의 ACK가 오면 `stop_timer`, wait for call from above로 상태 변경
	- 뭐 이런식..
- ***stop-and-wait*** : pkt을 보내고, ack올 때까지 기다린다
- pkt의 loss와 ack의 loss를 sender는 구분하지 못함. 사실 딱히 구분할 필요는 없고 일단 retransmission하면 끝임
- 또는 이미 timeout으로 인해 pkt을 재전송한 경우, 
	- receiver는 이미 받았으나 이에 대한 ack를 또 보낸다. 
	- sender는 ack를 두 번 받으므로, 이 상황을 알고 있고, 두 번째 받은 ack를 무시하면 됨
- stop-and-wait performance
	- $U_{sender}$ = (실제 비트를 전송하는데 쓰는 시간 $L/R$) / (전체 한 사이클 소요 시간 $RTT + L/R$) 
#### pipelining
이렇게 마냥 기다리는 방식은 너무 비효율적이라, ***pipelining*** 도입
여러개 pkt을 보내고, ack를 기다린다
- seq# 범위가 넓어야 함 : 여러 패킷에 대해 구분할 수 있어야 함
- 송신자는 buffer를 유지해야 한다(여러 패킷을 동시에 보내기 위해), and/or receiver는 buffer를 유지해야 한다(순서가 어긋나면 뒀다가 맞추기 위함)
- utilization : n개 패킷을 동시에 보내면, n배 증가
	*물론 무조건 n배 성능인건 아니지만 (go-back-n 또는 selective repeat 등의 방식으로 이를 유지하기 위한 overhead), 직관적으로는 n배*
- ***Go-Back-N***
	- sender : window size=N : ack를 받지 않고도 N개의 패킷을 보낸다
		- `nextseqnum` : application layer에서 다음 패킷이 넘어오면 이에 대해 사용할 seq#
		- `send_base` : window 시작지점. 여기에서 timer 돌아감
		- cumulative ACK : n번 ACK가 뜻하는 바는, **"n번까지의 패킷을 전부 잘 받았다"**
	- receiver : 항상 highest in-order seq#로 ACK를 보낸다 
		- 순서에 맞지 않게 들어와도, 
	- pkt n timeout => n, 그리고 그 이후로 보낸 pkt들을 전부 재전송
- Selective repeat
	- pkt n 각각에 대해 timer를 설정한다
	- sender : 
	- receiver : 받은 seq# n에 해당하는 ACK(n)을 보낸다
		순서가 맞지 않은 경우, 받은 pkt들을 buffer에 넣어둔다
	- pkt n timeout : pkt n만 재전송, 이걸 받은 receiver는 순서에 맞는 부분까지 deliver(socket으로 올려준다)
	- **dilemma**? seq#와 window size를 어떻게 설정하느냐에 따라 문제 가능성
		- window size만큼 보냈는데, 이에 대한 ACK가 전부 loss인 경우?
			receiver는 4,5,6을 기다리는데, sender는 1,2,3을 다시 보낸다
			sender가 receiver의 상황을 전혀 알 수 없기 때문임
		따라서 seq# < window size 의 관계가 되게끔 설정해야함(? 추정)
		***2 X window size <= seq# 범위*** 되게 설정하면 되는듯
---
## TCP
RFCs : 버전임.
이 여러 버전의 TCP가 공통적으로 가지는 특징들?
- point-to-point 1대1 통신
- reliable, in-order *byte stream* (stream이라고 함은.. message를 packet으로 잘게 나누어 연속으로 보낸다 뭐시기)
- full duplex data : 양방향에서, data의 전송과 수신을 
	- MSS : maximum segment size. 이걸 기준으로 message를 자른다
- cumulative ACK : 위에서 언급한 내용
- pipelining : window size만큼 동시에. 한번에
	- window size : congestion, flow control에 의해 정해진다
- connection-oriented : 데이터를 보내기 전에, 먼저 연결을 수행한다
	- three-handshaking
- flow control : receiver의 상황에 따라 sender의 전송 속도를 조절한다

###### TCP segment structure
- src port #, dest port #
- sequence number
- ACK number
- length + flag + receive window(flow control에서 사용)
	- C, E : congestion notification
	- A : ack정보 갖고있는지 여부. 
	- R,S,F : connection management
- checksum(error detection) 등

###### ACK, sequence#
- 내가 보낼 데이터의 시작 바이트 = seq#
	0~999: seq#=0 / 1000~1999: seq#=1 등..
- ACK : 반대편에서 보내야 할 seq# ?? 다음에 보내줘야 할, 기다리는 중인  seq#
- ![[Pasted image 20231019140730.png]]
	data 1byte이므로, seq=42 받고나면 그 다음은 43 받아야함. => ACK=43

###### timeout
timer 시간 어케 정함 ? => ***RTT***(ack보내고 ack받는데 걸리는 시간)이랑 맞춘다
근데 이게 RTT는 일정하지 않은게 문제임
따라서 RTT의 평균값을 구하고, 여기에 $+a$ (이를 safety-margin time)
- 먼저 평균값을 구하기 위해, **moving average**를 이용:
	EWMA : exponential weighted moving average
	- 이전의 평균과, 이번 RTT를 사용하여 계산. 이 때 사용하는 $alpha$값은 보통 0.125 사용
	- $(1-alpha)*EstimatedRTT+alpha*SampleRTT$
- 이제 safety margin값을 정해야함 : DevRTT
	$TimeoutInterval = EstimatedRTT + 4*DevRTT$ 
	- 변동이 크면 크게 정하고, 변동이 작으면 이 값은 작아야
	- safety margin = 편차값 $DevRTT$에 4를 곱해서 이만큼 더해준다
	- 이 편차값도 moving average로 구한다. 
$DevRTT = (1-beta)*DevRTT + beta*|SampleRTT - EstimatedRTT|$ 
이 때 $beta$값은 0.25로 쓴다

TCP는 기본적으로 Go-Back-N 방식에 + selective repeat 방법의 특징을 조금 넣는다
- timer 한 개만 사용 : `sender_base`에 대해
- timeout(n) : Go-Back-N과 달리, **timeout 패킷에 대해서만 재전송** 수행
	이 부분이 selective repeat방법의 특징을 가져온 것

![[Pasted image 20231019174112.png]]
receiver단에서 어떤 event에 대해 취하는 action의  종류 4가지
- 순서와 seq#를 제대로 받았고, 이전까지도 모두 expected data들인 경우
	=> delayed ACK : 500ms 기다렸다가 ACK보낸다
	다음 segment가 연이어 들어오는지 기다려본다. 만약 500ms 내에 다른 패킷이 또 도착하면, 이것을 받고 ACK를 한번만 보내도 됨 
	이렇게 하여 ACK 전송 횟수를 줄일 수 있음
- 순서와 seq#를 제대로 받았고, ACK 전송을 기다리는 다른 in-order 세그먼트가 있는 경우
	=> 2개의 in-order 세그먼트들을 ACK하기 위해, 즉시 cumulative ACK 전송
- 기다리던 것보다 높은 순서(순서 바뀜)가 도착, 격차 발견 : 
	=> duplicate ACK 즉각 보내기 : 기다리던 원래 순서를 가리키는 ACK
- 격차를 부분적으로or모두 채우는 세그먼트 도착
	=> 해당 세그먼트가 gap의 최솟값에서 시작하면, 즉시 ACK 전송

###### TCP fast retransmit
타이머를 사용하여 손실 판단하는데, 이 경우 timeout까지 계속 기다리는거
따라서 TCP는 여기에 추가적으로 cumulative ACK의 특징을 이용한다
**triple duplicated ACK** : 중복 ACK를 세 개 이상 받게 되면, 손실로 간주한다
![[Pasted image 20231019142449.png]]
이 경우처럼

###### flow control
sender가 보내는 속도가 너무 빨라서 receiver의 buffer가 overflow되는 경우
**receiver의 buffer사이즈를 봐야함** (비어있는 buffer 공간)
따라서 이것을 format 내에 *receive window* 필드로 넣는다
이에 맞춰서 sender의 window를 조절한다
- *rwnd* : receivew window 필드에 들어갈 값을 계산해야함
	- receive buffer 중에서도 비어있는 만큼
	- application layer는 필요할 때마다 buffer에서 데이터를 가져간다
- sender는, 노란 부분(보냈는데 ack 대기중)을 rwnd에 맞춰야 하고, 이를 위해 widnow size 조절
결국 receiver의 비어있는 buffer 사이즈를 보면서 sender의 window 조절

---
여기까지 시험범위입니다


