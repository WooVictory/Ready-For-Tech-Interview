## BFS & DFS

그래프 알고리즘으로, 문제를 풀 때 상당히 많이 사용되는 개념이다.

문제의 상황에 맞게 BFS와 DFS를 활용하면 된다.

여기서 사용되는 코드는 백준에 있는 [DFS와 BFS](https://www.acmicpc.net/problem/1260) 문제를 기반으로 한다.

> V : 정점, E : 간선

#### BFS

- 너비 우선 탐색이라 하며 BFS(Breadth-First Search)라 부른다.
- 루트 노드 혹은 임의의 노드에서 시작해 인접한 노드를 먼저 탐색하는 방법.
- 시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법이다.
- 즉, 깊게 탐색하기 전에 넓게 탐색하는 것이다.
- 큐를 사용한다. (해당 노드의 주변부터 탐색해야 하기 때문이다.)
- 최소 비용(즉, 모든 곳을 탐색하는 것보다 최소 비용이 우선일 때)에 적합하다.

![img](https://camo.githubusercontent.com/b8073f26dfdf1644e8a92312fff100341987a8f5/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f352f35642f427265616474682d46697273742d5365617263682d416c676f726974686d2e676966)

- 시간 복잡도
  - 인접 행렬 : O(V^2)
  - 인접 리스트 : O(V+E)



**[Code]**

```java
import java.io.*;
import java.util.*;

public class Main {
    private static final String SPACE = " ";
    private static ArrayList<Integer>[] a;
    private static boolean[] visit;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String[] input = br.readLine().split(SPACE);
        int n = convert(input[0]); // 정점의 개수
        int m = convert(input[1]); // 간선의 개수
        int start = convert(input[2]); // 시작할 정점 번호

        // 배열 초기화.
        a = new ArrayList[n + 1];

        for (int i = 1; i <= n; i++) {
            a[i] = new ArrayList<>();
        }

        for (int j = 0; j < m; j++) {
            String[] inputs = br.readLine().split(SPACE);
            int u = convert(inputs[0]);
            int v = convert(inputs[1]);

            // 양방향 그래프일 경우 양쪽 다 추가해준다.
            a[u].add(v);
            a[v].add(u);
        }

        // 방문할 정점이 여러 개인 경우 정점 번호가 가장 작은 것부터 탐색하기 위해서 정렬한다.
        for (int i = 1; i <= n; i++) {
            Collections.sort(a[i]);
        }

        visit = new boolean[n + 1];
        bfs(start);
        System.out.println();
    }

    private static int convert(String command) {
        return Integer.parseInt(command);
    }

    private static void bfs(int start) {
        LinkedList<Integer> queue = new LinkedList<>();

        visit[start] = true;
        queue.add(start);

        while (!queue.isEmpty()) {
            int x = queue.remove(); // 큐에서 정점을 뺀다.

            System.out.print(x + SPACE);

            for (int y : a[x]) {
                // 방문한 적이 있는지 체크한다.
                if (!visit[y]) {
                    // 해당 정점을 방문한 적이 없다면 방문했다고 true 로 체크한다.
                    // 그리고 해당 정점을 큐에 넣는다.
                    visit[y] = true;
                    queue.add(y);
                }
            }
        }
    }
}
// 입력
5 5 3
5 4
5 2
1 2
3 4
3 1
// 출력 결과
3 1 4 2 5
```



#### DFS

- 깊이 우선 탐색이며 DFS(Depth-First Search)라고 부른다.
- 루트 노드에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색한다.
- 넓게 탐색하기 전에 깊게 탐색하는 것이다.
- 예를 들어, 미로를 탐색할 때 한 방향으로 갈 수 있을 때까지 계속 가다가 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아와서 이곳으로부터 다른 방향으로 다시 탐색을 진행하는 방법과 유사하다.
- 스택이나 재귀함수를 통해 구현한다.
- 모든 경로를 방문해야 할 경우 사용에 적합하다.

![img](https://camo.githubusercontent.com/aaad9e39961daf34d967c616edeb50abf3bf1235/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f372f37662f44657074682d46697273742d5365617263682e676966)

- 시간 복잡도
  - 인접 행렬 : O(V^2)
  - 인접 리스트 : O(V+E)



**[Code]**

```java
import java.io.*;
import java.util.*;

/**
 * created by victory_woo on 02/04/2019
 * DFS와 BFS 복습
 */
public class BOJ1260_RE {
    private static final String SPACE = " ";
    private static ArrayList<Integer>[] a;
    private static boolean[] visit;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String[] input = br.readLine().split(SPACE);
        int n = convert(input[0]); // 정점의 개수
        int m = convert(input[1]); // 간선의 개수
        int start = convert(input[2]); // 시작할 정점 번호

        // 배열 초기화.
        a = new ArrayList[n + 1];
        visit = new boolean[n + 1];

        for (int i = 1; i <= n; i++) {
            a[i] = new ArrayList<>();
        }

        for (int j = 0; j < m; j++) {
            String[] inputs = br.readLine().split(SPACE);
            int u = convert(inputs[0]);
            int v = convert(inputs[1]);

            // 양방향 그래프일 경우 양쪽 다 추가해준다.
            a[u].add(v);
            a[v].add(u);
        }

        // 방문할 정점이 여러 개인 경우 정점 번호가 가장 작은 것부터 탐색하기 위해서 정렬한다.
        for (int i = 1; i <= n; i++) {
            Collections.sort(a[i]);
        }
        dfs(start);
    }

    private static int convert(String command) {
        return Integer.parseInt(command);
    }

    private static void dfs(int x) {
        // 방문한 적이 있다면 종료한다.
        if (visit[x]) {
            return;
        }

        visit[x] = true;
        // 방문한 순서 출력
        System.out.print(x+" ");

        for (int y : a[x]) {
            if (!visit[y]) {
                dfs(y);
            }
        }

    }
}
// 입력
5 4 5
5 4
4 3
4 2
1 5
// 출력 결과
5 1 4 2 3

// 입력
5 5 3
5 4
5 2
1 2
3 4
3 1
// 출력 결과
3 1 2 5 4
```