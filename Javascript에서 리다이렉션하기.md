[원본 포스팅 링크](https://www.daleseo.com/js-location/)

원래 HTML단에서 페이지 이동은 하이퍼링크를 통해
`<a href=“url”>` 과 같이, 요소의 속성에 명시
근데 자바스크립트단에서 처리하고자 하면

### window 전역객체의 location 프로퍼티 `window.location`
`location` 에는 현재 브라우저에 열린 페이지 위치 정보가 담겨있다
url => 프로토콜 호스트네임 포트번호 경로명 등
- .href : 전체 url을 문자열로 받기
- .pathname : 경로명
- .search : 쿼리스트링
등등

### 1. `location` 또는 `location.href` 직접 변경
그냥 `location.href = “url”` 이렇게 할당한다
- 방문기록 추가 : 뒤로가기 가능 (`history.back()`)
- 타입스크립트에선 location 직접할당하기 까다로움
- .href에 할당은 타입스크립트도 되지만 테스트 곤란

### `location.assign()` 메서드
괄호안에 url 넣기
- 방문기록 추가 : 뒤로가기 가능
- 느리다곤 하지만 별 의미없는듯
### `location.replace()` 메서드
괄호안에 url 넣기
- 방문기록 덮어쓴다 : 뒤로가기 불가. 이전으로 못 가게 막고싶은 경우

### 마무리
웹 접근성 측면에서는 자바스크립트보다는 html단에서 처리하는게 좋다.
혹시 <a> 요소로 가능하면 여기서 하도록하자