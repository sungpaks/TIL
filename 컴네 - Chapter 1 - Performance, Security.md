## Performance
- packet loss : 라우터 큐에서, arrival rate to link >> output link capacity
	- 더 받을 공간이 없는데 패킷이 들어오는 경우 : loss로 이어진다.
- packet delay : 4개 원인
	- $d_{proc}$ : nodal processing. => bit error 체크, 어떤 link 통할지 결정, 등..
			보통 < msec
	- $d_{queue}$ : queueing delay => 전송을 위해 queue에서 대기하는 시간
			라우터의 혼잡도에 따라 상이
	- $d_{trans}$ : transmission delay => $L/R$ 
			$L$ : 패킷의 크기(bits) , $R$ : link transmission rate (bps)
	- $d_{prop}$ : propagation delay => $d/s$ 
			$d$ : physical link의 길이 , $s$ : propagation speed (링크 재질 등)
![[Pasted image 20231021211523.png]]
$R$ : link bandwidth(bps) , $L$ : packet length(bits), $a$ : average 패킷 도착률
queueing delay : 1에 가까워질수록 급상승. 
=> 1인 경우, 이상적(주기적)으로 들어오면 문제없겠지만, 한번이라도 어긋나면 queueing delay가 무한정 증가해버림

- traceroute : 각 지점마다 패킷(probe)를 하나씩 보내보고, 돌아오는 시간을 기록한다. 각 i번째 probe패킷은 i번째 라우터(또는 엔드시스템)에 도착한 뒤, time과 함께 돌아옴
		ex) 4개 라우터, 1개 엔드시스템(목적지) 인 경우, 5개 패킷
		사실 실제로는 지점당 3개 probe를 보낸다

- Throughput : bits/time으로 나타내는, 시간당 보내는 데이터 양 (rate)
			네트워크 퍼포먼스에서 매우매우 중요!