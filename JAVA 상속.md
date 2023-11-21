### 상속

상속받으면 최소 같거나 보통 커진다 => 축소되는 경우는 없다
확장 or 구체화
1. 유지보수가 편하다
2. 클래스 간의 관계가 형성됨
3. 다형성으로 연결
4. 코드 간결 (코드 중복 피하는 등)
상속을 받으면, 필드와 메서드를 그대로 받게 된다.
- 자식 클래스의 생성자는 부모 클래스의 데이터를 만들지 않는다.
- 부모 클래스의 데이터는 ? 자식 클래스의 생성자에서 부모의 생성자 호출
	- 생략하면 default를 부르고, 또는 `super()`
- 부모 = parent, super, base / 자식 = child, sub, derived
- 메모리 구조 : 실제로 부모 클래스에 덧붙인다. 뚝 자르면 그대로 부모
- 다중상속을 지원하지 않는다(C++과 다름) 상속 횟수는 제한없다
	다중 상속 비슷한 걸 지원하는게 ***interfrace*** (implements)
- 모든 클래스의 최상위 조상 : `Object` .. 사실상 `extends object`가 생략

### Type Casting
`int i = 10` => `float f = i` : 항상 가능 : 정수 -> 실수 : 개념 확장
`float f = 10.5f` => `int i = f` : 그냥은 불가 : 실수 -> 정수 : 개념 축소
	그만큼의 손실이 있을 수 있음을 알고 명시하면 가능 : `int i = (int)f`

클래스 간의 형변환도 마찬가지다
- 자식->부모 : 항상 가능 - 확장되었던 부분만 도려낸다
	_실제로 메모리를 도려내진 않고, 레퍼런스가 부모만큼만 보도록 수정_
	**Up-casting** : 상속도의 화살표를 따라 부모로 올라가므로
- 부모->자식 : 원래는 안된다
	**Down-casting** : 부모를 자식변수로 내리므로
- **Down-casting 가능한 경우** : 자식->부모->자식
	`MyStudent d = (MyStudent) c` 이 때, c는 원래 `MyStudent`였고, 업캐스팅으로 인해 부모클래스인 `MyPerson`로 레퍼런스가 바뀌어있었음
	그러나 원래는 부모였던 `MyPerson a`가 있다면, 얘는 다운캐스팅 시 런타임에러
```java
public static void func(MyPerson in) {
	in.name += "*";
	in.print();
	if (in instanceof MyStudent) {
		MyStudent s = (MyStudent) in;
		s.school += "!";
		s.printStudent();
	}
}
```
- instanceof 연산자 : left가 right에 해당하는 type인지 판단, boolean반환
	`if (in instanceof MyStudent) MyStudent s = (MyStudent) in;
	=> 다운캐스팅 가능 여부 확인 : 원래 MyStudent instance인지 판단
	- 추천하는 방식은 아니다 : 클래스에 의존적임. 새로 클래스를 만들거나 하면 이쪽을 고쳐줘야함 => "외부 함수에서 클래스 내부를 건드림"
- 함수 overriding 이용 : 부모에 func 만들고, 자식에 또 func을 만든다
	확장, 교체.. 동적바인딩을 발생시키며, 이로 인해 다형성 실현
	- 동적 바인딩 : 런타임에 무슨 타입의 함수를 부르는건지 확인한다
		업캐스팅으로 레퍼런스 바꾼 경우 : 오버라이딩 된 함수를 호출하면, 현재 레퍼런스가 나타내는(부모)의 함수가 아닌, 실제 원본 타입을 동적으로 찾아서 실행
	- 오버라이딩된 함수는 동적으로 바인딩한다 => 동적바인딩이 쪼금 더 느리긴 함(판단하는 오버헤드가 추가되어서)
	- 기본적으로 전부 처음부터 다시 작성하는게 된다
	- 확장하고 싶으면? `super.func();` 이렇게 하여 부모의 동작을 호출
		생성자때 했던 `super()`와 달리 맨 처음에 부르지 않아도 됨
	- `@Override` annotation으로 "오버라이딩하는 함수"임을 명시하면 실수를 막을 수 있다
- 함수 overloading : 인자가 다른, 같은 이름의 함수를 작성 (함수 중복)