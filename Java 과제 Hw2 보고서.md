
<div style="text-align: right"> 19010418 조성훈 </div>

## Hw2_1
문제에서 요구하는 콘서트 좌석 예약 시스템을 구현하기 위해서는 여러 클래스들이 필요할 것 같습니다.
- `seat` class : 먼저, 좌석에 대한 부모클래스인 seat클래스를 작성하였습니다. 이 클래스는 크기가 10인 String 배열을 멤버변수로 가지며, 생성자에 의해 이 배열의 모든 이름이 “---“로 초기화됩니다. 또한 name 멤버변수는 `private`으로 지정하고 `getName`과 `setName` 메소드를 통해 접근하도록 하였습니다. 모든 좌석 정보를 조회하는 경우를 위해, name 배열을 모두 for-each문으로 순회하고 출력하는 `showSeatInfo` 메소드 또한 작성하였습니다.
- `seatA`, `seatB`, `seatC` class : 좌석은 S, A, B로 나뉘므로, `seat`클래스를 상속하여 각 등급 좌석 클래스를 작성하였습니다. 각 클래스는 부모클래스의 `showSeatInfo` 메소드를 오버라이드하여, 각각의 등급 정보를 출력한 뒤 `super` 객체의 메소드를 호출하여 부모클래스에서 구현한 동작을 수행하도록 하였습니다. 이렇게 하여 동적바인딩을 유발함으로써, 좌석 정보를 부모클래스인 `seat`으로 업캐스팅하여 묶어서 관리하면서도 각각의 좌석등급에 따라 다른 동작을 수행할 수 있도록 하고자 하였습니다.
- `ConcertReservation` class : 실제로 좌석 정보를 유지, 관리하고 예약 시스템을 수행하는 클래스입니다. 이 클래스는 멤버변수로 S, A, B 세 좌석등급에 해당하는 객체를 가지며, 이 각기 다른 등급의 좌석 객체는 부모클래스인 `seat`클래스로 업캐스팅되어 크기가 3인 배열로 유지됩니다. 생성자가 호출되면 객체들의 인스턴스가 생성되어 각 등급에 해당하는 좌석의 객체에 접근할 수 있으며, 이렇게 생성된 `ConcertReservation` 객체의 `menuInput()`메소드를 호출하여 해당 콘서트의 예약을 진행할 수 있습니다. 공연 예약 클래스를 이렇게 객체종속적으로 작성한 것은, 문제에서 "*공연은 하루에 한 번 있다*"라고 하였으므로, 공연은 여러 개 있으며 이에 따라 공연 예약 또한 각각의 객체가 존재할 필요가 있다고 생각했기 때문입니다.
	- `menuInput(Scanner in)` 메소드 : 정수를 입력받고, `switch` 문으로 이에 적절한 메뉴를 실행합니다. *끝내기*메뉴를 선택하지 않는 한, 함수를 재귀호출하여 새로운 메뉴 입력 사이클을 진행합니다.
	- `reservation(Scanner in)` 메소드 : 좌석등급을 입력받고, 해당 등급의 좌석 정보를 출력한 뒤, 예약자의 이름과 번호를 입력받고 이를 저장합니다.
	- `showInfo()` 메소드 : S, A, B 각 등급 좌석의 정보를 모두 출력합니다. 
	- `cancel(Scanner in)` 메소드 : 좌석 등급을 입력받고, 해당 등급의 좌석 정보를 출력한 뒤, 삭제할 이름을 입력받고 이와 일치하는 좌석을 찾아 해당 좌석의 이름을 삭제하고 "---"로 대체합니다.
- 유효하지 않은 범위의 입력(좌석 등급, 좌석 번호, 메뉴 등), 입력된 이름이 없는 경우, 또는 `Scanner`의 메소드 호출에서 예외가 발생하는 경우(`nextInt()`에 정수가 아닌 입력이 들어오는 경우 등) 등의 오류 발생 시 오류메시지를 출력하고 해당 입력을 다시 받도록 구현하였습니다.
		- 이 때 `Scanner`의 예외를 `catch`하는 경우, 다음 토큰은 여전히 invalid한 토큰을 가리키므로, `in.next();`로 토큰을 건너뛰지 않으면 무한루프에 빠져버리는 문제를 조심해야 하였습니다.
		- 예약 취소 시, 일치하는 이름이 없으면 이름을 바로 재입력하는 것이 아닌, 좌석등급을 다시 입력하도록 수정해야 하였습니다. 입력한 등급의 좌석에 취소하고자 하는 이름이 없을 수 있으며, 심지어는 해당 등급에 등록된 이름이 하나도 없을 수 있습니다.
- `Scanner`는 매번 필요성이 있을 때마다 객체를 생성하는 것이 아닌 객체 레퍼런스를 인자로 전달하도록 하였습니다.

## Hw2_2
key-value쌍의 Map을 구현하기 위해서는 보통 해시함수, 버킷 등의 개념이 사용될 것이지만, 이 문제에서의 `PairMap`의 구현 방식은 key와 value에 대한 배열을 따로 정해진 크기만큼 유지하며, 같은 위치에 있으면 key-value쌍이 되도록 합니다. key-value쌍의 검색은 배열을 모두 순회하며 일어납니다.
- 먼저 주어진 추상클래스인 `PairMap`에, 추가적으로 생성자를 작성하였습니다. 생성자는 `PairMap`추상클래스가 갖는 필드를 초기화합니다.
- `Dictionary` 클래스는 `PairMap`클래스를 상속하여 작성합니다. 모든 메소드를 Override하고, 생성자를 추가합니다.
	- 생성자는 `keyArray, valueArray`의 크기를 정할 정수형 인자 `n`을 받아 `super`메소드를 호출하여 부모 클래스의 생성자를 호출합니다.
	- `get` 메소드 : for-each문으로 `keyArray`를 순회하며 인자로 주어진 `key`와 동일한 위치를 찾고, 해당 위치의 `valueArray`값을 반환합니다. `key`와 일치하는 경우가 없었다면 `null`을 반환합니다.
	- `put` 메소드 : 이미 key가 있으면 value를 수정하고, 없으면 새로 삽입합니다. 이미 key가 있는지 확인하기 위해 `get`메소드의 반환값을 확인하며, 이에 따른 수정or삽입 연산을 수행합니다.
	- `delete` 메소드 : `key`에 해당하는 값이 `keyArray`에 존재하면 이를 삭제하고 반환하며, 존재하지 않는다면 `null`을 반환합니다.
	- `length` 메소드 : `valueArray`를 순회하며 `null`이 아닌 값의 개수를 세고 반환합니다.
- `keyArray` 내에서 어떤 `key`와 동일한 값을 찾을 때, `compareTo` 메소드의 반환값이 0인지 확인하여 동등성을 검사하도록 하면, 두 값 중 어느 하나라도 `null`이 있는 경우를 신경써야 했습니다. 그러나 동등성 검사를 `equals`메소드로 진행한다면 `null`인 경우까지도 무리없이 검사할 수 있었습니다.
## Hw2_3
추상클래스를 상속하여 서브클래스들을 작성하고, 이 서브클래스들을 슈퍼클래스로 업캐스팅하여 여러 도형들을 한번에 관리하는 문제였습니다.
- 주어진 추상클래스 `Shape`를 작성하고, 이를 상속하는 `Line, Rect, Circle` 클래스를 작성합니다. 이 서브클래스들은 단지 추상메소드 `draw`만을 오버라이드합니다. 슈퍼클래스에 default생성자가 작성되어 있으므로, 서브클래스에서 호출할 슈퍼클래스의 생성자를 따로 명시할 필요는 없었습니다.
- 세 가지 도형을 연결리스트 형태로 유지하고, 삽입, 삭제, 모두 보기 등의 그래픽 편집 기능을 갖는 `GraphicEditor`클래스를 작성하였습니다.
	- 필드로는 부모클래스 타입의 레퍼런스인 `Shape list`만을 가지며, 이는 도형 연결리스트의 HEAD입니다.
	- `add` 메소드 : 연결리스트에 새 도형을 삽입합니다. 새 도형은 인자로 들어온 `type`에 맞는 서브클래스 타입으로 정해지지만, 슈퍼클래스인 `Shape`으로 업캐스팅되어 연결리스트에 삽입됩니다.
	- `remove` 메소드 : 연결리스트에서 특정 위치의 원소(도형)을 삭제하고 `true`를 반환합니다. 그러나 해당 위치에 원소가 존재하지 않으면 삭제할 수 없으므로, `false`를 반환합니다.
	- `showAll` 메소드 : 리스트를 순회하며 각 도형들의 `draw`메소드를 호출합니다. 이 때 각 원소의 원래 타입의 `draw`메소드를 호출하는 동적바인딩이 발생합니다.
	- `end` 메소드 : 종료메시지를 출력합니다.
- `main` : `GraphicEdtior`객체 인스턴스를 생성하고, 메뉴를 입력받아 이에 적절한 `GraphicEditor`객체의 메소드를 호출합니다. 4(종료)가 입력되기 전까지 이를 반복합니다.
