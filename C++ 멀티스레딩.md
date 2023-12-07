`#include <thread>`
`thread myThread(함수포인터, 객체, 인자, 인자, ... )`
예를들어, `pc.dig(targetPos.X, targetPos.Y)`를 스레드로 대체하려면
=> `thread digThread(&PC::dig, &pc, targetPos.X, targetPos.Y);`
이런 다음, 두 가지 선택지
- `myThread.join()` : 메인스레드는 저거 끝나기를 기다린다
- `myThread.detach()` : 메인스레드와 분리시켜 백그라운드 작업을 지속
나의 목적은 백그라운드에서 작업이 일어나고, 다른 동작들은 계속되게 하고싶으므로, `detach()`로 한다

주의 : `switch case`문 안에서 thread변수를 만들면 `thread 초기화가 case레이블에 의해 생략되었습니다.` 뭐 이런게 나온다 
=> case문 내부에서 변수를 선언할 때 발생하는데, case 다음 실행할 구문(변수 선언 포함해서)을 {}스코프로 묶으면 된다..

함수 인자가 있을 때, 없을 때, 어떤 객체에서 부르는 함수일 때, namespace 등등에 주의