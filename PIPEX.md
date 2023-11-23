- `check_init` : file 체크 후 init, 그 뒤 pipe init
	- `access` : `R_OK`인지 확인하고, R권한 없으면 -1반환됨
	- `creat` : `O_WRONLY | O_CREAT | O_TRUNC`플래그로 `open`하는 것과 동일
		- `open`또는 `creat`으로 파일 열면, `fd` 반환, 에러가 있으면 -1반환
	- `pipe` : 프로세스 간 통신을 위한 단방향 데이터 채널인 pipe 생성
		- 인자로 `int pipefd[2]`를 넘김 : 두 종단의 fd를 반환하기 위함
			- 0 : read용 종단
			- 1 : write용 종단
- `do_pipex` : 환경변수에 해당하는 path를 찾고, `fork`해서 자식프로세스 만들고, ...

[[프로세스 간 통신 IPC]]