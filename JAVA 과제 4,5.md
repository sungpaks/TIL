일단 패널을 조건에 따라 갈아끼워야하는데
Game Start와 Game Over는 키 리스너로 SPACE입력이 들어오면 갈아끼운다
Game Play는 게임 종료 조건이 되면 갈아끼운다
그래서 이걸 어떻게 하냐

- 일단 Frame에서도 Runnable을 구현해서 스레드를 만들 수 있게 한다
- 이 Frame객체에서 메인스레드는 새 Thread를 생성하고, 이 Thread에게 지금 차례의 패널을 생성하고 Frame에 끼운다
- Main스레드는 이 Thread와 join하여 계속 기다린다. 사실상 프로그램 닫을 때까지 기다림이 끝나지 않음
- 패널을 꽂고 갈아끼우는 Thread는 현재 차례의 패널을 생성 -> 끼운다 -> 포커스 넘긴다 -> `setVisible` -> 해당 패널 안쪽의 스레드를 기다린다.
- 패널 내부의 스레드의 run : 
	- GameStart와 Over는 KeyEvent로 Space가 눌릴 때까지 wait(), 눌리면 notify => 스레드가 끝난다
	- GamePlay는 게임종료까지 계속 Game Loop를 돈다
- 패널의 스레드가 끝나면 다음 패널을 갈아끼울 차례이므로, 현재 Scene을 넘기고 run을 재귀호출한다


plate가 방향 바꿀 때, 움직이기 시작할 때 멈춤 없이 바로 부드럽게 움직이게 하는 법?
- `isMoving`을 유지하고, 움직이는 중이면 계속 update한다. 
- 그런데 `isMoving`을 press때 켜고 release때 끄면 한쪽을 누르면서 떼기 전에 반대쪽을 눌러버리는 등의 상황에서 잠깐 멈춰버린다.. 따라서, 
- `isMoving`을 boolean이 아닌 int로 유지하고, 키보드 왼쪽이나 오른쪽이 press되면 1씩 늘리고, release되면 1씩 감소시킨다. 이렇게하면 멈추지 않는다
- 그런데 이렇게 하면 가끔, 키보드를 모두 release했을 때에도 isMoving이 0이 아닌 경우가 생긴다.. 스레드에 의한 읽기쓰기 타이밍 때문으로 생각되므로, `synchronized`블록으로 이 부분을 동기화한다
이러면 문제없이 스무스한 방향전환과 이동시작이 구현된다~
- 이 때 벽에 막히는 경우를 `resolve`하려고 할 때, 그냥 쓰면 안되고, 얘도 `isMoving`일 때 같이 `update`와 묶어서 하도록 한다. 왜냐면.. `isMoving`이 0이면서 `run`루프가 동작하는 타이밍은 아직 `plate`객체가 생성되지 않은 타이밍일 수 있음. 실제로 그렇다 : 따라서 어차피 `isMoving`일 때 plate를 업데이트하고 충돌처리할거니까.. 같이 묶어버려야함

