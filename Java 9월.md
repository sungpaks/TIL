## 9월 11일 (월)
JRE : Java Runtime Environment : 자바 실행에 필요한거
JDK : Java Development Kit : 자바 개발에 필요한거

클래스 :=: 프로그램, 어플리케이션으로 취급
함수 :=: 메서드
Java는 char의 크기가 2바이트 => 확장형 유니코드 등 때문에
숫자 : byte(1바이트) -> short (2바이트) -> int (4바이트) -> long. unsigned는 없다

## 9월 13일 (수)
System.in 대신에 => Scanner : `Scanner in = new Scanner(System.in)` 
- java.util.Scanner가 풀네임이고, java.util을 import하면 이 앞의 namespace를 생략가능
- System.in : 바이트 데이터로 키값을 넘겨준다. 따라서 이걸 사용하려면?
		바이트 데이터 -> 문자 정보로 바꾸는 작업이 필요함.
- Scanner : 바이트 데이터를 알맞은 타입으로 변환하고 리턴함
- next() 메서드로 다음 토큰을 가져옴. default delim: ' ', '\n' . nextLine() 메서드로 한 줄 전체
- 타입을 정할 경우 nextInt() nextFloat() 등으로 쓴다. 타입을 다르게 쓸 경우 Exception
- nextLine() 보다 앞서서 next를 호출한 경우 주의!! 
		next() (또는 뭐 nextInt() 등..)로 토큰을 가져가고 나면, \n앞에서 끝나있다. 
		따라서 바로 nextLine() 호출하면 빈 문자열을 가져옴
		해결 => `while(str.length()==0) str=in.nextLine()` 이후에 nextLine()을 부른다

Java는 연산자 오버로딩을 허용하지 않으며, 문자열 간의 결합인 **+** 연산자만 허용되어있다

비트 연산자들은 비교 연산자보다 순서가 낮음에 주의
	=> if((a&SWITCH) != 0) 이런거 할 때 괄호 빼먹으면 절대 안된다는 뜻임

Expression Tree : 연산자를 부모, 피연산자를 자식 노드로 하여 트리를 구성. 양 자식의 값이 정해졌다면 계산하고, 그게 아니라면 확인하러 들어간다(재귀적)


## 9월 18일 (월)
- 유클리드 호제법 : 최대공약수를 구하는 알고리즘. 
	두 자연수 a, b (a>b)에 대하여, a와 b의 최대공약수는 b와 r (r = a%b)의 최대공약수와 같다.
```java
Scanner in = new Scanner(System.in);
int x = in.nextInt();
int y = in.nextInt();
if (x < y) {
	int tmp = x;
	x = y;
	y = tmp;
} //x를 큰 값으로 한다
while (true) {
	int r = x%y; //큰 값을 작은 값으로 나눈 나머지
	if (r==0) break; //나누어 떨어지면 작은 쪽이 최대공약수
	x = y; //나누어 떨어지지 않았으면, y와 r로 다시 반복
	y = r;
}
System.out.println(y);
```
또는 do-while로 다시 써서
```java
Scanner in = new Scanner(System.in);
int x = in.nextInt();
int y = in.nextInt();
if (x < y) {
	int tmp = x;
	x = y;
	y = tmp;
}
int r = x&y;
do {
	r = x%y;
	x = y; //이번엔 끝나기 전에 먼저 x<-y, y<- r을 했으므로,
	y = r;
} while (r != 0) //끝나고 나면 y가 아닌 x가 최대공약수이다
System.out.println(x);
```

Java의 배열은 => int[] a 이렇게 쓰는게 정석임. int[] 자체로 데이터타입이라고 보는게 좋다
for-each : `for(int a : b)` b 배열에 있는 원소 하나씩 각각을 a로 둔다. 
	=> 항상 배열의 처음부터 끝까지 읽으며, read-only

**garbage collecting** Java는, 더이상 사용되지 않는 힙 공간의 할당을 자동으로 해제해준다
ex) 힙 공간을 선언하면, 해당 공간의 reference counter++. 나중에 이게 0이되면 -> garbage
따라서, **delete가 없다** => system call로 delete요청을 할 수 있지만, 즉각적으로 일어나지 않는다. 
어느정도 쌓인 뒤 JVM의 판단에 의해 어느 순간에 일어나는데, 이 순간이 잠시 느려지는 타이밍이 될 수 있음 => 이걸 피하려면, 처음부터 메모리를 (static 등으로) 쭉 선언한 후 돌려쓰는 등의 방법을 사용함(나중에 언급)

`int m[3][5]` 의 경우를 생각하면
- C : `[i][j]` 자리는, 메모리가 선형으로 이어져있기 때문에, `i*5+j`임.  사실상 15의 공간을 3개로 논리적으로 자른거
- Java : 5칸 배열을 3개 만드는 셈임. 
```java
int [][]m = new int[3][5] //이렇게랑

int [][]m = new int[3][]
for(int i=0;i<3;i++) m[i] = new int[5]; //이렇게랑 같음 
```
## 9월 20일 (수)
**객체지향** 이란... 프로그램을 "전체"로 보지 않고, "object의 조합"으로 보게되는 것
1. 캡슐화 : 부품 하나하나를 독립적으로 구성하고, 숨긴다 => 사용 안정성
	Java에서는 멤버 함수를 메서드. 멤버 변수를 필드. 라고 한다
	메서드 + 필드 => 캡슐화하여, CLASS. => 이를 실제로 생성, 메모리를 잡으면 객체(instance)
	편의성과 안정성을 제공
2. 상속
3. 다형성

primitive 변수는 선언하자마자 메모리가 잡히지만, 클래스는 선언하면 레퍼런스일 뿐이다. 
`MyClass a` <- instance 없음. `a = new MyClass();` <- intance 생성됨
생성자 : 오로지 new 다음에만 호출가능함.. (나중에 예외적으로, 상속의 super 등이 있긴하다. [[나중에추가하기]])
