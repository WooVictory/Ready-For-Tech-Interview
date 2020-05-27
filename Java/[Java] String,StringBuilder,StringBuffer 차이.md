## String, StringBuilder, StringBuffer 차이



**[String]**

- Immutable하기 때문에 + 등 concat 연산 시 원본을 변경하지 않고 새로운 String 객체를 생성한다. 이로 인해 메모리 공간의 낭비가 발생하고 성능이 떨어진다.
- JDK 1.5 이후부터는 컴파일 타임에 StringBuilder로 변경한다고 한다.
- 불변 객체이기 때문에 멀티 쓰레드 환경에서 동기화를 신경쓰지 않아도 된다.
- 문자열 연산이 적고, 조회가 많은 상황에서 쓰기 좋다.



**[StringBuilder, StringBuffer]**

- 공통점
  - String과 다르게 Mutable한 객체이다.
  - 따라서 문자열 연산 시 새롭게 객체를 생성하지 않고, 처음에 만든 객체를 이용해 연산하고 크기를 변경시켜 문자열을 변경한다.
  - 따라서 문자열 연산이 자주 발생하는 상황에서 성능적으로 유리하며 쓰기 좋다.
- 차이점
  - StringBuilder : Thread-Safe 하지 않다. 멀티 쓰레드 지원하지 않음.
  - StringBuffer : Thread-Safe 하다. 멀티 쓰레드 지원함.
  - 즉, 동기화 지원의 유무.

StringBuilder는 동기화를 고려하지 않는 상황에서 사용.(Thread를 사용하지 않는 상황.) 문자열 연산이 많은 싱글 쓰레드 환경. 

StringBuffer는 동기화가 필요한 멀티 쓰레드 환경에서 사용. 문자열 연산이 많은 **멀티 쓰레드 환경**.
