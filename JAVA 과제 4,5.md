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
- `isMoving`을 boolean으로 하는 방법도, int로 하는 방법도 아님
- 왼쪽 눌렸는지에 대한 `boolean`과 오른쪽 눌렸는지에 대한 `boolean`을 유지한다. 
- 왼쪽만 눌려있으면 왼쪽으로 방향을 설정하고 업데이트
- 오른쪽만 눌려있으면 오른쪽으로 방향 설정하고 업데이트
- 둘 다 눌려있으면 vx=0으로 업데이트
- press하면 왼쪽or오른쪽인지 봐서 플래그 turn on
- release하면 왼쪽or오른쪽인지 봐소 플래그 turn off


`plate`상속해서 `brick`되게했는데, 반대로 하는게 좋으려나?? 바꿔보자
지금 공이 한번 튀기고나면 벽을 한번 통과하는 버그가 있음


폭은 750으로 하자.. 처음 250,250,250일거고, 그다음 


스테이지의 레벨에 따라, 
1레벨 = 벽돌 3x3
2레벨 = 벽돌 6x6
3레벨 = 벽돌 9x9
4레벨 = 벽돌 12x12 ..

이미지 늑대와 아기돼지 써서 늑대가 벽돌깨는 컨셉 ㄱㄱ? ㅋㅋ

헉ㅋㅋㅋ iterator순회할때도 "iterator"에 add해야함!! 
직접 linkedList에 add하거나 remove하면 바로 concurrentException
아 근데 iterator에 add메서드가 없다
- 벽돌과 공을 resolve할 때, 새로 생기는 ball들은 newBalls에 담는다, foreach문이 전부 끝나고나서 balls에 newBalls를 추가한다.

공의 속도는 점점 높아짐

start는 마지막에 하도록 변경

fadeOut을 어떻게 하는게 가장 좋을까?
- fade상태를 따로 유지하고, 깨지면 setDead가 아니라 `isFade=true`로 하고, 점차fade하기
- 스레드를 빼서 잔상남기기
***근데 필드 선언에서 `boolean isDead = false` 이렇게 하는거랑, 그냥 두고 생성자에서 `isDead = false`하는거랑 머가다름?***






지금 게임오버가 안됨!!!