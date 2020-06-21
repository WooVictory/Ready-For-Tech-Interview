### HashSet과 HashMap

HashMap과 HashSet은 모두 Collection Framework에 속한다. 

기본적으로 Collection Framework는 Set, List, Queue 인터페이스로 나뉘어진다.

- Set : 객체를 받지만, 중복되는 값은 허용하지 않는다.(순서가 없다.)
- List : 인덱싱하여 중복을 허용한다.
- Queue : 선입선출(FCFS) 알고리즘을 기반으로 한다.



#### HashSet

Set 인터페이스를 구현한 것으로 중복된 값을 허용하지 않는다.

HashSet에 들어가는 객체들은 반드시 equals()와 hashCode() 메소드를 구현해야 하는데, 이 메소드들을 가지고 HashSet에 들어갈 때, 중복된 객체가 있는지 여부를 체크하게 된다. 



#### HashMap

Map 인터페이스를 구현한 것으로 Key-Value 형태의 데이터를 저장한다. 

중복된 Key 값은 허용되지 않는다. 다만, 중복된 값의 저장은 허용한다.

null value, null key 를 허용한다.

- HashMap : 집어 넣은 순서를 유지하지 않는다.
- TreeMap : 집어 넣은 순서를 유지한다.



#### 차이점

HashMap

1. Map 인터페이스 구현
2. 데이터를 Key-Value 형식으로 저장한다.
3. HashMap에서 hashCode 값은 key value를 이용하여 생성한다.
4. HashMap은 unique key를 이용하여 데이터에 바로 접근하기에 HashSet에 비해서 빠르다.



HashSet

1. Set 인터페이스를 구현
2. 객체만 저장할 수 있다.
3. 들어가는 객체를 이용하여 hashCode를 생성하고, equals() 메소드를 이용해 hashCode를 비교해서 중복된 객체가 있는지 체크한다. (equals() 메소드는 중복된 객체가 있으면 true, 없으면 false 반환)
4. HashMap에 비해서 느리다.



### 참고

- [[Java]HashSet과 HashMap](https://postitforhooney.tistory.com/entry/JavaHashSet과-HashMap)

