## 힙 정렬(Heap Sort)

완전 이진 트리를 기본으로 하는 힙 자료구조를 기반으로 한 정렬 방식이다.

불안정 정렬에 속한다.

[완전 이진 트리?]

- 삽입할 때, 왼쪽부터 차례대로 추가하는 이진 트리





### 시간 복잡도

- 평균 : O(N logN)
- 최선 : O(N logN)
- 최악 : O(N logN)



### 로직

1. 최대 힙을 구성한다.
2. 현재 힙 루트는 가장 큰 값이 존재한다. 루트의 값을 마지막 요소와 바꾼 후, 힙의 사이즈를 하나 줄인다.
3. 힙의 사이즈가 1보다 크면 위의 과정을 반복한다.

![img](https://camo.githubusercontent.com/0104a65c5df44c342e310a24c1becd08c9596367/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393939383936343435414434393533303233)

루트 노드를 마지막 노드로 대체한다. (11->4) 그리고 다시 최대 힙 구성.

![img](https://camo.githubusercontent.com/000e4568cdab087691478961e100c8290df3af31/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393945314144343435414434393533303135)

이와 같은 방식으로 최대 값을 하나씩 뽑아내면서 정렬하는 것이 Heap Sort이다.

```java
private static void heapSort(int[] arr) {
        int n = arr.length;

  			// max heap 초기화.
        for (int i = (n / 2) - 1; i >= 0; i--) {
            heapify(arr, n, i); // 1
        }

  			// extract 연산. 
        for (int i = n - 1; i > 0; i--) {
            swap(arr, 0, i);
            heapify(arr, i, 0);
        }
    }
```



1번째 heapify

- 일반 배열을 힙으로 구성하는 역할을 한다.
- 자식노드로부터 부모 노드를 비교한다.
- (n/2)-1부터 0까지 인덱스를 돌리는 이유는?
  - 부모 노드의 인덱스를 기준으로 왼쪽 자식 노드 : ix2+1, 오른쪽 자식 노드 : ix2+2이기 때문이다.



2번째 heapify

- 요소 하나가 제거된 이후에 다시 최대 힙을 구성하기 위함이다.
- 루트를 기준으로 진행한다.

```java
private static void heapify(int[] arr, int n, int i) {
        int p = i; // 부모 노드.
        int l = i * 2 + 1; // 왼쪽 자식 노드.
        int r = i * 2 + 2; // 오른쪽 자식 노드.

        // 왼쪽 자식 노드와 부모 노드를 비교하여 큰 값을 부모 노드로 올린다.
        if (l < n && arr[p] < arr[l]) p = l;

        // 오른쪽 자식 노드와 부모 노드를 비교하여 큰 값을 부모 노드로 올린다.
        if (r < n && arr[p] < arr[r]) p = r;

        // 부모 노드를 가리키는 p 값이 바뀌면 위치를 교환하고
        // heapify()를 호출하여 과정을 반복한다.
        if (i != p) {
            swap(arr, p, i);
            heapify(arr, n, p);
        }
    }
```

- 다시 최대 힙을 구성할 때까지 부모 노드와 자식 노드를 swap 하며 재귀를 호출한다.
- 퀵 정렬과 합병 정렬의 성능이 좋기 때문에 힙 정렬의 사용 빈도가 높지는 않다.
- 하지만, 힙 자료구조가 많이 활용되고 있으며, 이때 함께 따라오는 개념이 Heap Sort이다.
- Heap Sort가 유용할 때
  - **가장 크거나 가장 작은 값을 구할 때** : 최소 힙 or 최대 힙의 루트 값이기 때문에 한 번의 힙 구성을 통해 구하는 것이 가능하다.
  - **최대 k 만큼 떨어진 요소들을 정렬할 때** : 삽입 정렬보다 더욱 개선된 결과를 얻어낼 수 있다.



**[Source Code]**

```java
package sort;

/**
 * created by victory_woo on 2020/03/14
 */
public class HeapSort {
    public static void main(String[] args) {
        int[] arr = {230, 10, 60, 550, 40, 220, 20};
        heapSort(arr);

        for (int i = 0; i < arr.length; i++) System.out.print(arr[i] + " ");
    }

    private static void heapSort(int[] arr) {
        int n = arr.length;

        // max heap 초기화.
        for (int i = (n / 2) - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }

        for (int i = n - 1; i > 0; i--) {
            swap(arr, 0, i);
            heapify(arr, i, 0);
        }
    }

    private static void heapify(int[] arr, int n, int i) {
        int p = i; // 부모 노드.
        int l = i * 2 + 1; // 왼쪽 자식 노드.
        int r = i * 2 + 2; // 오른쪽 자식 노드.

        // 왼쪽 자식 노드와 부모 노드를 비교하여 큰 값을 부모 노드로 올린다.
        if (l < n && arr[p] < arr[l]) p = l;

        // 오른쪽 자식 노드와 부모 노드를 비교하여 큰 값을 부모 노드로 올린다.
        if (r < n && arr[p] < arr[r]) p = r;

        // 부모 노드를 가리키는 p 값이 바뀌면 위치를 교환하고
        // heapify()를 호출하여 과정을 반복한다.
        if (i != p) {
            swap(arr, p, i);
            heapify(arr, n, p);
        }
    }

    private static void swap(int[] arr, int a, int b) {
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }

}
```



### 참고

- [힙 정렬(Heap Sort)]([https://gyoogle.dev/blog/algorithm/Heap%20Sort.html](https://gyoogle.dev/blog/algorithm/Heap Sort.html))

