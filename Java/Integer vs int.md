### Integer vs int

사실, 이 둘의 차이는 대부분 알 것이라고 생각한다. 

정리하는 이유는 최근에 알게 된 사실 때문이다.

int

- Primitive 자료형
- 산술 연산이 가능하며, null 값을 가질 수 없다.

Integer

- Wrapper 클래스(객체)
- Unboxing을 하지 않으면 산술 연산이 불가능하지만, null 값을 가질 수 있다.
- Collection, null 값이 필요한 경우 사용한다.



### Integer와 int의 size 비교

- Integer 및 int 배열을 1,000,000개 생성한다.
- 결과
  - Integer :  19986824 byte
  - int : 3998536 byte
  - 4.99배(약 5배)



**요약**

- Object : 8 byte
- Integer : 16 byte
- Integer를 참조하는데 4 byte
- 따라서 Integer의 size = 20 byte
- int의 size : 4 byte
- 5배 차이가 난다.



### 참고

- [[Java] Integer와 int의 차이](https://includestdio.tistory.com/1)

