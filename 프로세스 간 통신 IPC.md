Inter-Process Communication

> 리눅스 기반 운영체제의 모든 프로그램들은 파일로 존재

이 파일을 구분하기 위해 번호를 붙인게 **fd**

- fd 테이블 : 프로세스에서 필요로 하는 fd를 써놓는 테이블
	=> 프로세스가 파일에 접근(`open` 등?)하면 fd테이블에 올라간다

### PIPE ?
프로세스 간 통신의 방법 중 하나로, 프로세스들의 통신을 위해 개설하는 별도의 공간 이라고 봐야할 듯
사실상 버퍼임 : 통신을 위한 메모리 공간을 생성하고 이를 매개로 통신
- ***Anonymous*** PIPE : 부모-자식, 형제-형제 프로세스 간에 사용. 
	- `pipex`과제에서 사용하는 파이프이며, `pipe()`함수로 pipe 시스템콜을 호출할 수 있다
	- 파이프는 *단방향*으로 동작. 하나는 read만, 하나는 write만
- Named PIPE : `PIPE type`의 큐를 하나 생성하고, 어쩌구.. 하는데 

#### fork
`fork()` : 현재 프로세스로부터 자식 프로세스를 생성한다.
- 연관된 작업을 동시에 하고싶음 => 두 프로그램을 실행하는 것이 아닌, 자식프로세스를 생성하여 여기서 실행하도록 함
- 이렇게 만들어진 child process는 parent process와 다른 점은
	- 유일한 `pid`를 가지며, parent의 pid와 다르다
	- 개별 공간을 할당받음 : 내용은 그대로 복사되고 상속됨
	- 


pipe 만들고 -> fork로 자식프로세스 생성 -> pipe 세팅(한 쪽은 read를 닫고, 다른 한 쪽은 write를 닫는 등)

