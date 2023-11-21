package manager : npm

- index.js : `<App>`컴포넌트를 render
- App.js : Start 전인지 후인지 감시 (`onStartButtonClicked`를 넘김) 하고, 상태에 맞는 컴포넌트 리턴
	- 근데 왜 `setIsStarted`자체를 넘기지 않았지??
	- 또는 그냥 람다식으로 넘겨도 됐을 듯
- BeforeGameStart.js : 그냥 시작화면. 버튼 누르면 state변경
	- 여기다 추가할만한거 : ?
		- 몇 초 플레이할건지?
		- 난이도??
- AfterGameStart.js : 시간을 잰다, Game컴포넌트 호출 
	- (`setTimeout` : 이거 머라더라?비동기 어쩌구..라서 좀 손봐야하나 싶기도 하고)
- Game.js
	- `getRandom` : 랜덤으로 난수 생성, 리턴
	- `newPosition` : `getRandom` 두 개 불러서 랜덤한 위치좌표 생성
	- `isInTarget` : 타겟을 클릭했는지 확인 : 
		- 먼저 헤드(동그라미)로의 거리를 재고, 좌표가 내부인지 확인
		- 헤드 아니면 몸통 히트인지 확인 (몸통은 직사각형으로 간주)
	- `drawBody` : 어깨부분 둥글게 그린다
	- `drawEyes` : 눈 그려줌ㅋㅋ
	- `drawCross` : 현재 마우스 위치에 크로스헤어 추가
	- `Game` : 
		- `useEffect`로 `setInterval`감싸서 시간 재는데 잘 안나옴
		- 