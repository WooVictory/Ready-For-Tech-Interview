## Stack과 Queue

스택과 큐는 선형 자료구조이다.



- Stack
  - 나중에 들어간 원소가 먼저 나오는 구조이다.
  - LIFO(Last in First Out)의 구조.
  - 안드로이드의 액티비티를 관리하는 데 스택이 사용된다.
  - 시간 복잡도 : O(n)
  - 공간 복잡도 : O(n)
  - 언제 사용? 함수의 콜 스택, 문자열 역순 출력, 연산자 후위 표기법 등
- Queue
  - 먼저 들어간 원소가 먼저 나오는 구조이다.
  - FIFO(First in First out)의 구조.
  - 큐는 활용 분야가 되게 많다. 안드로이드의 경우, 루퍼의 메시지 큐가 예시 중 하나이다.
  - 시간 복잡도 : O(n)
  - 공간 복잡도 : O(n)
  - 언제 사용? 버퍼, 마구 입력된 것을 처리하지 못하고 있는 상황, bfs 탐색 등



### 2개의 스택으로 큐 구현

가끔 이런 문제가 면접에서 나온다고 한다. 어렵다고 생각했는데, 그리 어렵지 않고 간단하게 구현할 수 있다.

![img](https://t1.daumcdn.net/cfile/tistory/222BDF4E5462B1E00D)

1. inbox에 데이터를 삽입한다(push) -> A,B
2. inbox에 있는 데이터를 추출(pop)하여 outbox에 삽입(push) 한다. -> B,A
3. outbox에 있는 데이터를 추출(pop)한다. -> A,B 순으로 출력된다.



즉, inbox 스택에 A,B 순으로 데이터를 삽입하면 위의 그림처럼 스택에 데이터가 쌓인다. 그리고 inbox 스택에 있는 데이터를 pop해서 outbox로 옮긴다. 그렇게 되면 outbox에는 B,A 순서로 데이터가 쌓인다.

그리고 다시 outbox 스택에 있는 데이터를 pop하게 되면 A,B 순으로 데이터가 출력된다.



[Code]

```java
package Stack;

import java.util.Stack;

/**
 * created by victory_woo on 2020/05/06
 * Stack 2개를 이용해서 Queue 구현하기.
 */
public class StackWithQueue {
    public static void main(String[] args) {
        StackQueue<String> queue = new StackQueue<>();
        queue.enQueue("A");
        queue.enQueue("B");
        queue.enQueue("C");

        System.out.println(queue.deQueue());
        System.out.println(queue.deQueue());
        System.out.println(queue.deQueue());
    }

    static class StackQueue<T> {
        private Stack<T> inBox;
        private Stack<T> outBox;

        StackQueue() {
            inBox = new Stack<>();
            outBox = new Stack<>();
        }

        void enQueue(T item) {
            inBox.push(item);
        }

        Object deQueue() {
            if (outBox.isEmpty()) {
                while (!inBox.isEmpty()) {
                    outBox.push(inBox.pop());
                }
            }

            return outBox.pop();
        }
    }
}

```



위의 내용은 [Creator Developer](https://creatordev.tistory.com/83) 님의 블로그를 참고했다.





### Stack 구현

TODO



### Queue 구현

TODO

