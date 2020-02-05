## equals() 메소드 동작 원리

`equals()`

- 비교를 위한 메소드이다. 
- Java에서는 대상의 내용 자체를 비교한다. 
- 그렇다면 두 문자열을 비교할 때, 어떤 원리로 비교할까?
- Ex) a = "Victory", b = "Victory"



```java
public boolean equals()(Object anObject){
  if(this == anObject) return true;
  
  if(anObject instanceof String){
    String anotherString = (String) anObject;
    int n = value.length;
    if(n == anohterString.value.length){
      char v1[] = value;
      char v2[] = anotherString.value;
      
      int i = 0;
      while(n-- !=0){
        if(v1[i] != v2[i]) return false;
        
        i++;
      }
      return true;
    }
  }
  return false;
}
```



- 먼저, 같은 객체인지 비교한다. 같은 객체라면 같은 값을 가지고 있기 때문에 true를 반환하며, 아래 문장은 수행되지 않는다. 
- 다음으로 인자로 들어온 Object가 String 타입인지 확인하고 조건을 만족하면 해당 객체를 String타입으로 형 변환을 한다. 
- 그리고 char[] 배열로 변환한 뒤, 문자를 앞에서부터 하나씩 비교한다. 한 개의 문자라도 다르다면 false를 반환하고 모든 문자가 동일하다면 true를 반환한다. 
- true -> 동일한 내용임을 의미. false -> 다른 내용임을 의미.