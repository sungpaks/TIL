메모리 압축을 위해 갖은 노력을 했던 전통 C를 생각하면, int는 4바이트인데 반해 char는 1byte이므로.. 할거면 char로 하는게 낫지 않았겠는가? 라는 생각이 든다

내가 모르는 소리를 하는건가? 비트 연산을 하는게 보통이었을 수도
비트 선언은?

------

1비트 자료형을 선언할 수 있나요?
https://stackoverflow.com/questions/31310496/smallest-data-type-can-i-define-a-one-bit-variable
```c
typedef struct foo
{
    unsigned x:1;
} foo;
```
이렇게 하면 만들 수는 있는데, 어차피 1비트를 쓰든 2비트를 쓰든 얼마나 쓰든, 바이트 단위로 묶인다
- structure packing arrangements
그래서 이렇게 1비트로 만들어도 unsigned int만큼 공간을 먹는다
따라서 foo의 배열 또한 비트단위로 연속하지 않는다
이렇게 하는 쪽이 컴파일러가 최적화할 수 있는 것임. 

https://www.quora.com/Why-would-one-use-int-instead-of-bool-as-their-method-type-despite-there-being-only-two-possible-return-values
why use int instead of bool
C로 쓴 경우 : C99부터 `_Bool` 자료형이 stdbool.h에 생겼지만..
- 전통적으로, 0은 false, 0이 아닌 경우 모두 true를 뜻하도록 int를 썼다
- standard와 일관성을 유지하기 위함. 또는 내부, 또는 서드파티 라이브러리와의 일관성
- just 습관

https://stackoverflow.com/questions/9521140/char-or-int-for-boolean-value-in-c
이게 완전히 내 질문인데
"int가 보통 더 빠른 타입이고, char로 메모리 절약하는게 상당히 무시되는 수준임(likely negligible)"

정수로의 승격(promotion) (묵시적 형변환)과도 관계가 있는 듯?
그냥 "1"이라고 쓰면.. 어차피 Integer로 들어가는게


리틀 엔디언, 빅 엔디언
