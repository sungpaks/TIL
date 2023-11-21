## 2020 JAVA 중간
#### 1. JDK와 JRE의 차이점
- JDK : Java Development Kit, 자바 개발 도구
	- JRE + 자바 프로그램의 **개발**에 필요한 컴파일러, 디버거 등
	- JRE보다 상위 집합의 개념으로 볼 수 있음. 실행+개발
- JRE : Java Runtime Environment, 자바 실행 환경
	- 자바 프로그램을 **실행**하기 위한 라이브러리, JVM 등

#### 2. c 소스코드를 java에 맞게 작성
![[Pasted image 20231018142437.png]]
```java
import java.util.Scanner;

public class Hello {
	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		float f;
		f = in.nextFloat();
		System.out.println("f="+f);
	}
}
```

#### 3. 자바의 변수 명으로 써서는 안되는 것은?
![[Pasted image 20231018142521.png]]
예약어가 아닌걸 찾으란 뜻임
default, goto 안됨
bool, constant, bite, prohibited 가능

***'_', '$', letter*** 만 가능.. 
안되는 키워드... const (constant는 된다) finally, goto, native, synchronized, transient, volatile 등... 또한 true, false, null도 안될거
#### 4. 다음 명령문의 실행 결과?
```java
int a = 5;
int b = a << 2;
int c = a >> 2;
int d = a & 0b0100;
System.out.println("a=" + a + ", b=" + b);
System.out.println("c=" + c + ", d=" + d);
```
a=5 / b=20 / c=1 / d = 4

#### 5. int 변수의 최솟값 및 최댓값?
-2147483648 ~ 2147483647

#### 6. var 데이터 타입?
C++의 `auto` 키워드와 동일하게, 변수 타입의 선언을 생략하여 컴파일러의 타입 추론을 강제함. :
- 지역 변수 선언에만 사용
- 변수 선언에 반드시 초기값 지정 : `var name` 안되며, `var name = "KIM"` 이렇게 해야함

#### 7. 다음과 같은 비정방형 2차원 int 배열 arr를 생성하는 코드를 작성
![[Pasted image 20231018143923.png]]
```java
int[][] arr = new int[4][];
for(int i=0;i<4;i++) {
	arr[i] = new int[i+1];
}
```

#### 8. 빈칸 채우세요
![[Pasted image 20231018144135.png]]
```java
//class Node
class Node {
	int data;
	Node next;
	Node(int in, Node prev) {
		data = in;
		next = ((1. null));
		if (prev != ((2. null))) prev.next = ((3. this));
	}
}
//Main
Node a = new Node(10, ((4. null)) );
Node b = new Node(20 ,a);
Node c = new Node(30, b);
Node cur = a;
while (cur != ((5. null))) {
	System.out.println(cur.data);
	cur = cur.next;
}
```

#### 9. JAVA의 Garbage Collection에 대해, 어떤 방식으로 이것이 자동으로 수행되는지 간략히 쓰시오 
힙 공간은 각기 **reference counter**를 갖고 있고, 레퍼런스 변수가 생성될 때마다 해당 주소의 reference counter가 1씩 올라간다. 이것이 reference counter=0인 힙 공간은 garbage collecting의 대상이 되며, JVM의 판단에 의해 자동적으로 collecting이 수행된다

#### 10. 
```java
class Counting {
	static int n = 0;
	Counting() {
		n++;
	}
}
```
static으로 선언하여 객체에 종속되지 않게 관리하며, 생성자가 불릴 때마다 n을 증가

#### 11. 다음의 실행 결과는
![[Pasted image 20231018165505.png]]
`A
`B: 10`

#### 12. 틀린부분?
`LinkedList <int> list = new LinkedList<>()`
얘 인터페이스 아닌가??

#### 13. iterator는 .. 아직 안나감 패스

#### 14. Runtime Exception?
exception을 throw하는 함수를 사용하는 경우, 기본적으로 try-catch문을 통해 이 잠재적인 위험을 handling하거나, 이 위험한 함수를 사용하는 함수에서도 동일한 exception을 throw하여, 위험함을 알지만 미루도록 하거나, 둘 중 하나를 해야만 합니다. 
그러나 너무 자주 쓰이고 잘 알려진 경우에 대해 이 의무를 강제하지 않게 되어있는데, 이렇게 "예외 발생 가능성이 있는 함수임에도 예외 handling을 강제하지 않는" 예외들을 Runtime Exception이라고 합니다.
이 Runtime Exception를 갖는 경우 try-catch로 감싸거나 다시 throw하지 않아도 사용할 수 있으나, Runtime에서 예외가 발생하면 이 에러 정보를 출력하고 프로그램을 종료하게 됩니다.
Runtime Exception 예 : 
- 나눗셈(/)연산 : devideByZeroException 가능성
- Array 접근 : outOfIndex 가능성

#### 15. 람다식으로 바꾸삼
![[Pasted image 20231018173226.png]]
=> 람다식을 사용하여 새로 작성한 main 함수 :
`MyNumber myNum = (n)->n*2;`

-----
## 2021 JAVA 중간
#### 1. API는 무엇의 약자임? && JAVA API에 포함된 예
API는.. 머시기 interface인데
***API*** : Application Programming Interfaces : 프로그래밍 언어에 추가로 유용한 기능을 제공하는 라이브러리 
	Java는 광범위한 API 집약체임
JAVA API에 포함된 것들의 예
- java.lang 패키지 : 기본 클래스와 데이터 타입을 정의함. Object, String, Integer, 등..
- java.util 패키지 : Scanner, ArrayList 등..

##### JAVA의 특징 Main Features
- virtual machine의 사용을 통해 => "Write Once, Run Anywhere"
- Built-in GUI, networking, security, multi-threaded programming
- 단순, 객체지향, 고성능, 견고함, 안전성Secure, 컴퓨터 구조에 중립적 (Architecture-neutral), 이식 가능(portable), interpreted 방식. 멀티스레딩 지원. 동적, 분산처리 지원.
##### JAVA의 단점??
- bytecode로 컴파일된 코드를 실행하는 것이, 원시 기계 코드로 컴파일된 코드를 실행하는 것보다 좀 더 느리다
	=> 이를 해결하기 위해, JIT(Just-In-Time) 컴파일러 도입하여 이 갭을 채움
- standard Java APIs로는 모든 low-level 조작을 지원할 수 없음
	=> 따라서 native(non-Java) 확장의 형태로 지원됨

#### 2. Java 언어의 특징인 WORA에 대해 설명하고, 이것이 가능한 원리에 대해 간략히 설명하라
WORA : Write Once, Run Anywhere
플랫폼에 종속되지 않고, 어떤 환경에서도 호환되도록 한다
이것이 가능한 이유 : Java는, 코드를 컴파일하여 bytecode로 만들고, 이 bytecode를 JVM 위에서 실행시킨다. 따라서, 어떤 플랫폼이라 할지라도, JVM만 있다면 플랫폼에 관계없이 Java Byte Code를 실행할 수 있게 한다

#### 3. Java `boolean`과 C++의 `bool`타입의 차이점
C++에서 `bool` 타입은 `int`형과 혼용될 수 있었음. 0을 `false`로, 0이 아닌 모든 수를 `true`로 간주했다. 따라서 `bool isDone = 0;` 이렇게도 가능
그러나, Java에서는 `boolean`타입과 `int`타입 사이의 혼용을 허용하지 않는다. 따라서, `boolean isDone = 0;` 불가, 반드시 true or false만 가능
***정수값을 논리형으로 형변환할 수 없다***

#### 4. 이거 실행결과 ??
```java
int a = 3;
int b = 4;
int c = 5;

System.out.println("a+b="+a+b*c);
```
a+b=320 (b * c 먼저 실행되고, 그 다음 a에 문자열형태로 붙게 됨)

#### 5. 이거 실행결과 쓰고, 이유도
```java
String s1 = "Sejong";
String s2 = "Sejong";
String s3 = new String("Sejong");
System.out.println("s1==s2 : " + (s1==s2));
System.out.println("s1==s3 : " + (s1==s3));
```
`s1==s2 : true` *아 false가 아니네*
`s1==s3 : false`
String끼리의 `==`연산을 진행하는 경우, 레퍼런스가 가리키는 주소가 같은지 아닌지를 보게 됨
근데 `s1==s2`인 이유는 리터럴을 같이 가리키는 셈이라서 인가??
ㅇㅇ `String s1 = "Sejong";` 이렇게 하면 최초로 "Sejong" 리터럴 인스턴스가 생성,저장되고, 이를 참조함. 그 다음 `String s2 = "Sejong";` 하면, 이전에 생성된 인스턴스를 그저 참조할 뿐임. 따라서 레퍼런스가 동일

#### 6. super() 메서드의 목적 및 사용 시 주의사항에 대해 간단설명
super() 메서드는 sub클래스에서 부모클래스의 생성자를 호출하는 메서드임. 슈퍼클래스의 여러 생성자들 중 명시적으로 원하는 생성자를 호출 가능
(*주의 : 메서드 오버라이딩에서 super는 슈퍼클래스의 객체를 가리키며, super.method()이렇게 하여 슈퍼클래스의 메서드를 호출함. 이 경우 정적바인딩*)
super() 메서드 사용 시 주의사항
- ***무조건*** 가장 첫 줄에서 호출
- 생성자에서만 호출 가능함. (부모클래스의 생성자)
- 명시적으로 호출하지 않으면 자동으로 슈퍼클래스의 default 생성자가 호출되며, 슈퍼클래스에 default 생성자가 없다면 에러

#### 7. Object 클래스에는 hashCode() 메서드가 있다. hash code는 무슨 뜻이며 어떤 용도임?
hash code : 객체 식별값이며, 객체가 참조하는 주소를 알기 위함??
hash code : 객체의 상태나 내용을 나타내는 정수 값으로, 객체를 메모리 내에서 고유하게 식별할 수 있는 값임
용도
- 해시 테이블 or 해시 맵
- 객체 간의 동등성 검사
- 해시 코드 기반 집합 및 집합 연산
- 객체 식별

#### 8. 다음은 사용자가 만든 Employee 클래스이며, 이를 main에서 배열로 만들어 사용하려 한다. 이 때 Arrays.sort 메서드를 이용하여 정렬을 수행하고 싶다. 정렬이 수행될 수 있도록 Employee 클래스를 고쳐서 다시 제시하시오

```java
// class Employee 내용 
public class Employee{
	String name;
	Employee(String in) { name = in; } 
} 
// Main 함수 내용: 
Employee [] arr = new Employee[3];
arr[0] = new Employee("Kim");
arr[1] = new Employee("Park");
arr[2] = new Employee("Lee");
Arrays.sort(arr);
for(Employee e : arr) System.out.println(e.name);
```
먼저 Employee클래스가 comparable 인터페이스를 구현하도록 해야함
- 일단 Arrays 클래스를 사용하기 위해 `import java.util.Arrays;`
- 그 다음 `class Employee implements Comparable` => Comparable 구현
- `@Override` 키워드와 함께 `public int compareTo(Object o)` 메서드 작성
```java
//Employee 클래스에 다음과 같이 작성
@Override
public int compareTo(Object o) {
	if (o instanceof Employee) {
		Employee in = (Employee) o;
		return this.name.compareTo(in.name);
	}
	else return 0;
}
```

#### 9. 다음 코드는 for-each 구문에서 오류 발생. 어떤 오류이며, 이를 제대로 돌아갈 수 있게 iterator를 이용...? 

for-each는 READONLY라서 remove불가

#### 10. 다음 main 실행결과가 다음과 같이 나오도록 빈칸 채우시오
```java
static void func(Object o) {
	if(/*빈칸 1*/) System.out.println("정수입력 : " + o);
	if(/*빈칸 2*/) System.out.println("문자열입력 : " + o);
}

public static void main(String args[]) {
	func(10);
	func("Sejong");
}
//출력 내용 :
//정수입력 : 10
//문자열입력 : Sejong
```
`o instanceof Integer`
`o instanceof String`

#### 11. 다음 코드의 잘못된 점을 찾고 이유 설명
```java
try {
	func(); //예외 생길 수 있는 함수로, 잘 구현되어 있다고 가정
	int x = 4;
	int y = 0;
	int z = x/y;
} catch (Exception E) {
	System.out.println("예외 발생");
} catch (ArithmeticException E) {
	System.out.println("나누기예외발생");
}
```
***상위 Exception클래스를 하위(sub)Exception클래스보다 먼저 catch하면 안됨***
구체적인 예외부터 처리하며, 일반적인 예외를 아래에 두어야 함
일반적인 예외를 먼저 처리하면 그 하단의 구체적인 예외 처리로 갈 수 없기 때문

#### 12. JAVA의 명령어 throw와 throws는 용도가 다른데, 각각 어떤 용도인지 짧게 설명
- **throw** : Exception을 발생시키고 함수를 종료한다. (개발자가 예외를 발생시킴)
- **throws** : 해당 메서드가 특정 Exception을 발생시킬 수 있음을 알린다. (선언)

#### 13-1. package와 module의 차이에 대해 간단히 설명
????? package는 ..
#### 13-2. Template을 사용한 Generic 클래스..
얘네는 안배움

#### 14. 아래 Child클래스의 생성 코드 수행 시 아래와 같이 출력되도록 빈 칸을 채우시오
```java
class Parent{
	Parent(int n) {
		System.out.println("parent: " + n);
	}
}
class Child extends Parent{
	Child(int n) {
		/*빈 칸*/
		System.out.println("child: " + n*2);
	}
}
//Child 생성 코드
Child a = new Child(10);

/*
실행 결과 :
parent: 10
child: 20
*/
```
그냥 빈칸에 `super(n);` 추가하여 super클래스의 생성자를 호출하면 됨

#### 15. 람다식은 코드를 간략히 줄일 수 있게 해 준다. 어느 경우에 람다식을 사용할 수 있는가??
interface가 단일 추상 메서드를 갖는 경우 (이를 *functional interface*)

---
## 2022 Java 중간
### 1. 객체지향 관점에서 C++과 JAVA의 차이점에 대해 3가지 이상 쓰시오
1. C++의 클래스는 다중상속이 가능했지만, JAVA의 클래스는 다중상속이 불가능하다
2. C++은 연산자 오버로딩이 가능했지만, JAVA는 이를 허용하지 않는다.
3. C++은 클래스의 생성자와 함께 소멸자가 존재하지만, JAVA의 클래스는 소멸자가 존재하지 않는다. JAVA의 메모리공간은 garabage collector에 의해 관리됨.
4. 접근 지정자 : C++과 JAVA가 비슷하지만, JAVA에서는 *default*가 추가됨. 폐쇄적인 순서로
	1. private : 해당 클래스 내에서만 사용
	2. defualt : 해당 클래스, 그리고 패키지 내에서만 사용
	3. protected : 해당 클래스, 패키지, 그리고 상속된 자식 내에서만 사용
	4. public : 어디서든 사용 가능
5. 인터페이스 : C++에는 없는 interface가 추가되어있음. 이를 통해 *어떤 기능을 갖는 클래스들 간에 집합 관계*를 만들고 다형성을 부여할 수 있음

#### 2. 다음 main 함수를 정의하는 빈 칸에 들어갈 키워드 두 개를 각각 쓰고, 그 의미를 설명하시오
```java
public class MidTest{
	/*빈칸 1*/ /*빈칸 2*/ void main(String[] arg) {
	}
}
```
1. public : 접근지정자 중 하나로, 어떤 scope에서도 접근할 수 있도록 공개되어있음을 뜻함
2. static : 함수를 정적으로 선언하겠다는 뜻으로, 정적으로 함수를 선언하면 클래스가 로딩될 때 함께 static의 메모리가 잡히며 객체에 종속적이지 않게 된다

#### 3. Java와 C++의 char 데이터타입의 차이점에 대해 간략히 쓰시오
C++에서는 char 데이터타입이 1byte크기인 반면,
Java에서는 char 데이터타입이 2byte크기이다
이는 C++과 달리 JAVA는 charset(문자집합)으로 unicode를 사용하며, 유니코드의 표현에는 16비트가 필요하기 때문이다

#### 4. 다음 명령문의 실행 결과를 예상해보시오
```java
int a = 7;
int b = a << 2;
int c = a >> 1;
int d = a & 0b1100;
System.out.println("a="+a+", b="+b);
System.out.println("c="+c+", d="+d);
```
7 = 0111 / 0111<<2 = 0001 1100 = 4+8+16 = 28 / 0111 >> 1 = 0011 = 3
0111 & 1100 = 0100 = 4
`a=7, b=28`
`c=3, d=4`

#### 5. 다음 코드의 실행 결과를 쓰고 그 이유를 간단히 설명하라
```java
String a="가나다라";
System.out.println(a=="가나다라");
String b=new String(a);
System.out.println(a==b);
```
결과 : `true false`
이유 : 처음에는 "가나다라"에 해당하는 리터럴이 생성되고 이를 참조하는 변수 a를 만들었다. 따라서 "가나다라"리터럴과 a의 참조 메모리는 동일하므로, `true`
그런데 `String b = new String(a)` 와 같이 a와 같은 값을 갖는 *새로운 객체*를 생성하였으므로, 다른 메모리가 잡혔다. 따라서 두 번째는 `false`

#### 6. this() 메서드의 목적 및 사용 시 주의사항
생성자 내에서 동일 클래스의 다른 생성자를 호출하기 위해 this() 메서드가 사용됩니다. 이 메서드를 호출할 때는 생성자 코드블록의 첫 줄에서 호출해야만 함을 주의해야합니다.

#### 7. Object 클래스의 존재 이유 (또는 활용법)에 대해
Object클래스는 JAVA의 모든 클래스의 최상위 클래스로, 모든 클래스는 Object클래스를 상속한 자식클래스입니다. 이렇게 최상위 클래스 Object를 둠으로써 다음의 활용을 기대할 수 있습니다
- 모든 객체를 Object 타입으로 다룰 수 있어 **다형성**을 지원할 수 있습니다
- 메서드 : Object 클래스는 기본적으로 `equals`, `hashCode`, `toString` 등의 메서드를 정의하고 있으며, 이를 상황에 맞게 사용 또는 오버라이딩하여 필요한 동작을 구현할 수 있습니다.
- 제네릭한 객체 연산 : 객체 비교, 해시코드 생성, 등..

#### 8. 다음 MyMath 클래스에 원주율 pi값을 상수로 지정하려 하는데, 두 빈칸에 들어갈 키워드를 쓰시오
```java
class MyMath{
	/*빈칸 1*/ /*빈칸 2*/ double PI = 3.1415926535;
}
```
- `static` : 정적으로 생성하여, 객체가 아닌 클래스 자체에 종속되도록 합니다.
- `final` : 이 키워드를 사용하여 불변값으로 선언합니다

#### 9. 다음은 MyString을 상속, MyColorString 클래스를 만든 코드이다. 두 빈칸을 채우시오
```java
class MyString{
	String str;
	MyString(String in){str=in;}
}
class MyColorString /*빈칸 1*/ MyString{
	String color;
	MyColorString(String in, String c) {
		/*빈칸 2*/
		color = c;
	}
}
```
1. `extends`
2. `super(in);`

#### 10. 다음 2차원 배열 n을 주어진 것과 같이 출력되도록 2중 for문을 이용하여 작성하시오 (if, switch 사용 X)
```java
int n[][] = {{1}, {2,10,5}, {3,5}};
//여기부터 작성

/*---------------------------------------*/
/*
출력 결과 :
1
2 10 5
3 5
*/
```
답 : 이렇게 작성
```java
for(int i=0;i<3;i++) {
	for(int j=0;j<n[i].length;j++) {
		System.out.print(n[i][j] + " ");
	}
	System.out.println();
}
```

#### 11. 자바의 레퍼런스 변수형은 C의 포인터와 유사하지만, 더 안전하다고 한다. 어떤 면에서 자바의 레퍼런스 변수가 더 안전할 수 있는지 간략히 쓰시오
C의 포인터는 주솟값에 직접 접근하며 따라서 포인터 연산이 가능하지만, Java의 레퍼런스 변수는 주솟값을 간접적으로 "참조"할 뿐이며 이에 대한 연산이 불가하다.
또한 C의 포인터와 달리 Java의 레퍼런스는 반드시 type을 가진다.
C의 포인터는 전적으로 개발자에 의해 관리되며, 메모리 할당 / 해제, 타입, 예외, 등에 대한 책임이 개발자에게 있는 반면, Java의 레퍼런스는 위와 같은 잠재적 위험요소들이 시스템에 의해 관리됩니다. (가비지컬렉팅 등)

#### 12. 동적바인딩?
레퍼런스 변수가 참조하는 객체타입, 그에 따른 호출할 메서드를 런타임에 결정하는 것을 동적바인딩이라고 합니다.
부모클래스의 메서드를 자식클래스가 오버라이딩한 경우, 이 메서드를 호출 시 동적바인딩이 일어난다
동적바인딩이 일어나는 예 : 
	최초에 자식 클래스 객체를 가리켰던 레퍼런스를 업캐스팅 -> 부모클래스에 대한 레퍼런스로 변경한 경우 :
		현재 참조하는 부모 클래스가 아닌, 실제 원본인 자식 클래스 타입의 메서드를 찾아 호출함

#### 13. a,b,c 세 값 중 가장 작은 값을 계산하는 함수이다. 다음 빈 칸에 "3항 연산자"를 사용하여 한 문장으로 완성하시오
```java
int getMin(int a, int b, int c) {
	return a < b ? (a < c ? a : c) : (b < c ? b : c);
}
```
`return a < b ? (a < c ? a : c) : (b < c ? b : c);`

#### 14.
![[Pasted image 20231020182632.png]]
```java
//Node 클래스 ----
class Node {
	int data;
	Node next;
	Node (int in) {
		data = in;
		next = {빈칸 1};
	}
}

//----main----
Node a = new Node(10);
Node b = new Node(20); a.next = b;
Node c = new Node(30); b.next = c;

Node head = a;
while (head != {빈칸 2}) {
	System.out.println(head.data);
	{ 빈칸 3 }
}

/*
출력 결과 :
10
20
30
*/
```
1. null
2. null
3. head = head.next;

#### 15. 다음과 같이 인터페이스가 주어졌을 때 아래 왼쪽 코드의 밑줄 부분을 람다식으로 바꾸려한다. 빈칸을 채우시오

```java
interface MyNumber {
	public int getValue(int n);
}

//main
MyNumber myNum = new MyNumber() {
	public int getValue(int n) {
		return n*2;
	}
}
```
답 : 이렇게 바꾼다 `MyNumber myNum = (n)->2*n;`



----
- API : Application programming interfaces : `java.lang` `java.io` `java.math`  `java.util.Scanner` 등
- Java Source -> (Java Compiler) -> Java ByteCode로 변환 !!
	-> Java Virtual Machine 위에서 이 Java Byte Code를 실행 :
	- 장점 : 어디서든 수정 없이 JVM만 있다면 실행 가능 
		Write Once, Run Anywhere (WORA)
	- 단점 : 
		- 바이트코드의 실행은 기존에 기계어를 실행하던 것보다 조금 더 느리다..
		=> JIT(Just In-Time) compiler 도입으로 이 차이를 메운다
		- 저수준 시스템에 대한 조작을 표준 Java API로는 다 할 수 없다
			JVM위에서 돌아가기 때문??
- Java 프로그램 
	- 개발 : 바이트코드(.class)를 하나의 실행파일로 만드는 *링크 과정*이 없다.
	- 실행 : main()메서드를 가진 클래스부터 실행 시작. 
		JVM은 필요할 때만 클래스 파일을 로딩(JVM의 클래스 로더에 의한 동적 로딩)하며, 따라서 적은 메모리로 실행 가능
	- 반면 C/C++은, 소스를 컴파일하여 목적코드, 목적코드와 라이브러리를 링크하여 최종 실행 파일 생성. 정적 라이브러리는 실행파일에 포함시켜버린다.
- 자바 특징 : 단순/객체지향/고성능/견고/안전/architecture-중립적/이식가능/interpreted/멀티스레드/동적/분산처리
- 배포판 종류 : Standard Edition SE, Micro Edition ME, Enterprise Edition EE
	JDK > JRE > JAVA SE API 이렇게 포함관계
	JDK는 JRE + Java Language, Tool&Tool APIs
 - java는 charset으로 unicode를 사용함 => 2byte(16bit)써서 65536가지 구분
 - `var` == C++의 `auto` : 지역변수 선언에만 가능!!! 컴파일러가 변수 타입을 추론함. 또한 반드시 초기값 지정
 - 같은 우선순위의 연산자는 왼쪽에서 오른쪽으로 처리하는데, 
	 예외적으로, 대입연산자, --,++,+,-,!,형변환은 오른쪽에서 왼쪽으로 간다 
	 주의!! 비트연산자는 !=, == 연산자보다 우선순위가 낮다
- Scanner 객체 in에 대해, `in.nextLine()` 앞에 `in.next()`를 호출한경우 주의 : 개행 직전까지만 잘려있어서 빈 문자열을 받게될 수 있다
	=> `while(str.length()==0)str=in.nextLine()` 한 줄 추가하고, 이후에 `str=in.nextLine()`으로 가져온다
- 비트 시프트 연산자
	- a>>b : 산술적 오른쪽 시프트 : 최상위 비트의 빈 자리는 시프트 직전 최상위 비트로 채운다
	- a>>>b : 논리적 오른쪽 시프트 : 최상위 비트의 빈 자리는 항상 0으로 채운다.
	- a<< b : 산술적 왼쪽 시프트 : 최하위 비트의 빈 자리는 항상 0으로 채운다
- `this()` : 클래스 내 다른 생성자 호출. 
	- 생성자 내에서만 가능 / 반드시 코드의 가장 처음에 수행
- 기본 타입 변수인 인자는 : call by value / 배열, 객체는 call by reference
- 가비지 : 가리키는 레퍼런스가 하나도 없는 객체 : 누구도 사용할 수 없게 됨. 
	힙 공간을 선언하면 공간의 reference counter가 ++
	- 가비지 컬렉션 : JVM의 가비지 컬렉터가 자동으로 가비지들을 반환
	- 개발자는 `System.gc();` 메서드를 호출하여 JVM에 gc요청을 보낼 수 있지만, 곧바로 무조건 해주는건 아님
- 패키지 : 관련 클래스 파일(.class)을 저장하는 directory. 자바 응용프로그램은 하나 이상의 패키지로 구성됨
- 접근지정자
	- private : 나만
	- default : 나, 그리고 동일 패키지까지
	- protected : 나, 동일 패키지, 그리고 상속된 자식클래스까지
	- public : 전부
- static, non-static
	- non-static : 객체 종속적(instance멤버), 객체 생성 후 사용 가능, 비공유되며 배타적
	- static : 클래스에 종속적이며 클래스 당 하나만.(class 멤버) , 객체 생성하지 않아도 사용 가능, 공유되며 동일 클래스의 모든 객체에 대해 공유됨
		- 전역변수 전역함수 만들 때. / 공유 멤버를 작성할 때.
		- static 메서드는 non-static에 접근 불가. 객체가 없으니까~
		- static 메서드는 this 불가. this는 객체니까~
- 상속 : 클래스 간결화/유지보수/생산성/재사용과 확장/새 클래스 작성속도 빠름
- 오버라이딩 : 슈퍼 클래스에 선언된 메서드를 서브 클래스에서 다시 구현
	- 같은 이름에서 서로 다른 내용이 나오게 구현되는거임 : 다형성
	- 동적 바인딩을 통해 실행 중 다형성 실현
		*오버로딩은 컴파일 타임에 다형성이 실현되는 예*
	- **동적 바인딩** : 실행할 메서드를 run time에 결정. 오버라이딩 메서드를 찾아 호출하는거임
	- `super.method()` : 서브 클래스에서, 슈퍼 클래스의 메서드를 호출하고자 할 때. => super로의 접근은 정적 바인딩으로 처리됨
- 추상 메서드 : 선언되었으나 구현되지 않은 메서드로, `abstract` 키워드
- 추상 클래스 : 상속하고 추상메서드 구현하지 않으면 자식도 추상클래스임. 이 경우도 `abstract`로 선언. 
	1. 추상 메서드를 하나라도 가진 클래스 : 반드시 `abstract` 선언
	2. 추상 메서드가 없어도 `abstract`로 선언된 클래스
	- 추상클래스 용도 : 
		- 설계구현 분리 : 슈퍼 클래스는 개념을 정의하고, 서브 클래스에서는 구체적인 행위를 구현함. 
		- 계층적 상속 관계
- 인터페이스 : 객체와 객체 사이의 상호작용을 나타냄. 클래스의 다형성을 실현하는 도구임 => 클래스들의 기능을 다르게 구현하도록 함
	=> 클래스가 구현해야 할 메서드들이 선언되는 추상형임
	- 상수, 추상메서드, default 메서드, private 메서드, static 메서드 포함.
	- 그러나 여전히 필드 선언 불가
	- 인터페이스 객체 생성 불가, 레퍼런스 변수 선언 가능
- inner class : `private`지정을 유지하면서도 자유롭게 갖다 쓸 수 있음
	하나의 장소에서만 사용되는 클래스를 안쪽에 모은다 : 가독성,유지보수
- exception :
	- Error
	- RuntimeException(Unchecked) : 처리가 강제되지 않으며, 이는 자주 일어나는 에러인 경우에 해당. 처리를 강제하지 않지만 에러나면 런타임 종료
		`ArithmeticException, NullPointerException, ClassCastException, NegativeArraySizeException, OutOfMemoryException, NoClassDefFoundException, ArrayIndexOutOfBoundsException` 등
	- Checked Exception : Error, RuntimeException 제외한 나머지. 반드시 처리되어야 함(try-catch 등)