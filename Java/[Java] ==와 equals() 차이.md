## ==와 equals() 차이

- == 
  - 비교를 위한 연산자.
  - 비교하고자 하는 대상의 **주소값**을 비교한다. 
- equals()
  - 메소드이며, 객체끼리 내용을 비교할 수 있다.
  - 비교하고자 하는 **대상의 내용 자체**를 비교한다.



[Code]

```java
String a = "a";
String b = a;
String c = new String("a"); // 새로운 객체 생성. 주소가 다름.

// 주소값을 비교. 
a == b; // true
a == c; // false

// 내용(값)을 비교. 
a.equals(b); // true
a.equals(c); // true
```

