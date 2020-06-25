### 서론

***RecyclerView***는 앱에서 거의 필수적인 존재라고 생각이 든다. 대부분의 서비스가 리스트 형식이 존재하기 때문이다. 이렇듯 리스트를 효율적으로 보여주기 위해 사용하는 것이 ***RecyclerView***이다. 그렇다면 우리가 자주 사용하는 `setHasFixedSize`를 true로 설정한다는 게 무엇을 의미할까??



### 본론



필자는 `setHasFixedSize = true`의 문장을 별 의미 없이 타이핑했다. 이렇게 하는 것은 정말 좋지 않은 습관이다. 필자도 이 코드만 이렇게 했을 뿐, 다른 코드는 다 생각하고 작성한다. 아무튼, 저 함수는 무엇을 의미하는지 살펴보자.





***[setHasFixedSize]***

- [StackOverflow](https://stackoverflow.com/questions/28709220/understanding-recyclerview-sethasfixedsize)의 답변을 해석했다.

- 아래의 함수를 보자

```java
void onItemsInsertedOrRemoved() {

   if (hasFixedSize) layoutChildren();

   else requestLayout();

}
```



- 기본적으로 아이템을 삽입, 이동 혹은 제거할 때마다 RecyclerView의 크기 및 너비나 높이가 변경될 수 있으며, 뷰 계층 구조의 다른 뷰의 크기가 변경될 수 있다.

- 따라서 항목을 자주 추가하거나 제거하는 경우, 특히 문제가 될 수 있다.

- 어댑터의 내용을 변경해도 높이나 너비가 변경되지 않는 경우, setHasFixedSize를 true로 설정하여 불필요한 레이아웃 패스를 피하라.





결국, 아이템 항목을 추가할 때마다 RecyclerView의 크기는 변경된다. ***크기가 변경되기 때문에 레이아웃을 그릴 때, 크기를 측정하고 다시 그리는 것을 반복할 것이다.*** `setHasFixedSize`의 기능은 RecyclerView의 크기 변경이 일정하다는 것을 사용자의 입력으로 확인한다. 항목의 높이나 너비가 변경되지 않으며, 추가 또는 제거된 모든 항목은 동일하다. `setHasFixedSize`를 설정하지 않으면 항목의 크기가 변경되어 비용이 많이 드는 작업을 하는지 확인한다.



### 결론

대부분 RecyclerView를 사용하는 목적은 동일한 크기의 아이템 항목을 사용자에게 리스트로 보여주기 위해서다. 따라서 아이템의 크기가 변하는 경우는 없을 것이고, 그렇다면 ***setHasFixedSize를 true로 설정함으로써 변경되지 않는다는 것을 명시하는게 좋다.*** 따라서 레이아웃을 다시 그리는 비용이 많이 드는 작업을 피하도록 하여 성능 하락을 방지할 수 있다고 생각한다. 





**Reference**

- [stack overflow](https://stackoverflow.com/questions/28709220/understanding-recyclerview-sethasfixedsize)

- [안드로이드 리사이클러뷰 사용법](https://godog.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EB%A6%AC%EC%82%AC%EC%9D%B4%ED%81%B4%EB%9F%AC%EB%B7%B0RecyclerView-1)