### CPU 스케줄링

CPU가 하나의 프로세스 작업이 끝나면 다음 프로세스 작업을 수행해야 한다. 이때 어떤 프로세스를 다음에 처리할 지 선택하는 알고리즘을 CPU Scheduling 알고리즘이라고 한다. 따라서 상황에 맞게 CPU를 어떤 프로세스에 배정하여 효율적으로 처리하는가가 관건이다.



### Preemptive vs Non-Preemptive

1) Preemptive(선점)

- 프로세스가 CPU를 점유하고 있는 동안 I/O나 인터럽트가 발생하지 않았음에도 다른 프로세스가 해당 CPU를 강제로 점유할 수 있다. 
- 즉, 프로세스가 정상적으로 수행중인 동안 다른 프로세스가 CPU를 강제로 점유하여 실행할 수 있다.



2) Non-Preemptive(비선점)

- 한 프로세스가 CPU를 점유했다면 I/O나 인터럽트 발생 또는 프로세스가 종료될 때까지 다른 프로세스가 CPU를 점유하지 못하는 것이다. 





### 선점형 스케줄링

1) SRT(Shortest Remaining Time) 스케줄링

- 짧은 시간 순서대로 프로세스를 수행한다.
- 현재 CPU에서 실행 중인 프로세스의 남은 CPU 버스트 시간보다 더 짧은 CPU 버스트 시간을 가지는 프로세스가 도착하면 CPU가 선점된다.

2) Round Robin 스케줄링

- 시분할 시스템의 성질을 활용한 방법
- 일정 시간을 정하여 하나의 프로세스가 이 시간동안 수행하고 다시 대기 상태로 돌아간다.
- 그리고 다음 프로세스 역시 같은 시간동안 수행한 후, 대기한다. 이러한 작업을 모든 프로세스가 돌아가면서 진행하며, 마지막 프로세스가 끝나면 다시 처음 프로세스로 돌아와서 작업을 반복한다.
- 일정 시간을 Time Quantum(Time Slice)라고 부른다. 일반적으로 10 ~ 100msec 사이의 범위를 갖는다.
- 한 프로세스가 종료되기 전에 time quantum이 끝나면 다른 프로세스에게 CPU를 넘겨주기 때문에 선점형 스케줄링의 대표적인 예시다.

3) Multi-level Queue 스케줄링

- 프로세스를 그룹으로 나누어, 각 그룹에 따라 Ready Queue(준비 큐)를 여러 개 두며, 각 큐마다 다른 규칙을 지정할 수도 있다.(ex. 우선순위, CPU 시간 등)
- 즉, 준비 큐를 여러 개로 분할해 관리하는 스케줄링 방법이다.
- 프로세스들이 CPU를 기다리기 위해 한 줄로 서는 게 아니라 여러 줄로 선다.

![img](https://user-images.githubusercontent.com/34755287/53879673-5e979880-4052-11e9-9f9b-e8bfec7c9be6.png)

4) Multi-level feedback Queue 스케줄링

- 기본 개념은 Multi-level Queue와 동일하나, 프로세스가 하나의 큐에서 다른 큐로 이동 가능하다는 점이 다르다.

![img](https://user-images.githubusercontent.com/34755287/53879675-5f302f00-4052-11e9-86a2-c02ee03bac64.png)

- 위 그림에서 모든 프로세스는 가장 위의 큐에서 CPU의 점유를 대기한다. 이 상태로 진행하다가 이 큐에서 기다리는 시간이 너무 오래 걸린다면 **아래의 큐로 프로세스를 옮긴다.** 이와 같은 방식으로 대기 시간을 조정할 수 있다. 
- 만약, 우선순위 순으로 큐를 사용하는 상황에서 우선순위가 낮은 아래의 큐에 있는 프로세스에서 starvation 상태가 발생하면 이를 우선순위가 높은 위의 큐로 옮길 수도 있다.
- 대부분의 상용 운영체제는 여러 개의 큐를 사용하고 각 큐마다 다른 스케줄링 방식을 사용한다. 프로세스의 성격에 맞는 스케줄링 방식을 사용하여 최대한 효율을 높일 수 있는 방법을 선택한다.



### 비선점형 스케줄링

1) FCFS(First Come First Server)

- 준비 큐에 먼저 도착한 프로세스가 먼저 CPU를 점유하는 방식이다.
- CPU를 할당받으면 CPU 버스트가 완료될 때까지 CPU를 반환하지 않으며, 할당되었던 CPU가 반환될 때만 스케줄링이 이루어진다.

<img src="https://user-images.githubusercontent.com/33534771/89703489-500b8a00-d986-11ea-9b6c-27cca4ea1016.png" width="300" height="300"/>

![img](https://user-images.githubusercontent.com/34755287/53879661-5d666b80-4052-11e9-8453-bad918a563ef.png)

표는 3개의 프로세스와 각 프로세스가 CPU를 사용한 시간(Burst Time)을 나타낸다.

이를 간트 차트로 표현하면 그림과 같다. (도착 시간은 모두 0초라고 가정한다.)

평균 대기 시간은 아래와 같다.

- Average Waiting Time = 0 + 24 + 27 / 3 = 17msec

만약, 프로세스가 들어온 순서가 P3, P2, P1이라면 간트 차트는 아래와 같이 바뀐다.

![img](https://user-images.githubusercontent.com/34755287/53879665-5d666b80-4052-11e9-8ad5-8639b73b13ac.png)

- Average Waiting Time = 3 + 6 + 0 / 3 = 3msec

두 경우에서 모든 프로세스가 끝난 시간은 30msec로 같지만, 평균 대기 시간으로 봤을 때는 위의 예제는 17msec이고 아래는 3msec로 차이가 난다. **즉, 들어온 순서로 수행한다고 해서 반드시 효율적인 것은 아니다.**

위의 예제처럼 `P1, P2, P3` 순서로 들어온 경우를 **Convoy Effect** 라고 한다. 

이는 CPU 시간을 오래 사용하는 프로세스가 먼저 수행되는 동안 나머지 프로세스들은 그만큼 오래 기다리는 것을 뜻한다. P1이 수행되는 동안 P2, P3는 오래 기다리게 된다. 

단점

- Convoy Effect 발생 : 소요 시간이 긴 프로세스가 짧은 프로세스보다 먼저 도착해서 뒤에 프로세스들이 오래 기다려야 하는 현상



2) SJF(Shortest-Job-First)

- 다른 프로세스가 먼저 도착했더라도 CPU 버스트가 짧은 프로세스에게 CPU를 먼저 할당하는 방식이다.
- 선점, 비선점 모두 가능하다.

<img src="https://user-images.githubusercontent.com/33534771/89703540-b7293e80-d986-11ea-9b11-0dabd8e5488f.png" width="300" height="300"/>

![img](https://user-images.githubusercontent.com/34755287/53879666-5d666b80-4052-11e9-93c2-86b725588403.png)

위의 간트 차트는 SJF를 사용했다. 평균 대기 시간은 아래와 같다.

- Average Waiting Time(AWT) = 3 + 9 + 16 + 0 / 4 = 7msec

이번에는 위의 표를 FCSF를 사용해 간트 차트로 나타내고 평균 대기 시간을 구해보자.

![img](https://user-images.githubusercontent.com/34755287/53879667-5d666b80-4052-11e9-8cd4-066aefcf3047.png)

- Average Waiting Time(AWT) = 0 + 6 + 14 + 21 / 4 = 10.25msec

SJF가 평균 대기 시간이 더 짧다. 수학적으로 증명되었으며, 어떠한 예제를 보더라도 SJF의 AWT가 짧다는 것을 알 수 있을 것이다. 



SJF가 가장 효율적인 CPU 스케줄링 방법 같지만, 매우 **비현실적**이다. 왜냐하면 컴퓨터 환경에서는 프로세스의 CPU 점유 시간(Burst time)을 알 수 없다. 한 프로세스가 실행 중에는 많은 변수가 존재하기 때문에 CPU 점유 시간을 알려면 실제로 수행하여 측정하는 수밖에 없다. 실제 측정한 시간으로 예측하여 SJF를 사용할 수도 있지만, 이는 오버헤드가 매우 큰 작업으로 잘 사용되지 않는다.



3) Priority

- 우선순위가 높은 프로세스가 먼저 선택되는 스케줄링 알고리즘이다.
- 우선순위는 정수값으로 나타내며, 작은 값이 우선순위가 높다.(Unix/Linux 기준)

- 선점, 비선점 모두 가능하다.

<img src="https://user-images.githubusercontent.com/33534771/89703556-e344bf80-d986-11ea-87f1-74994cc47510.png" width="300" height="300"/>

![img](https://user-images.githubusercontent.com/34755287/53879671-5e979880-4052-11e9-84d3-524270cdc920.png)

우선순위가 낮은 순서대로 수행한 모습을 간트 차트로 나타냈다.

- Average Waiting Time(AWT) : 0 + 6 + 16 + 18 + 1 / 5 = 8.2msec

우선순위를 정하는 방법은 크게 내부적인 요소와 외부적인 요소로 나뉜다.

- Internal : time limit, memory requirement, I/O to CPU burst(I/O 작업은 길고, CPU 작업은 짧은 프로세스 우선) 등
- External : amout of funds being paid, political factors 등



- 단점 : Starvation(기아) 현상

CPU의 점유를 오랜 시간 동안 하지 못하는 현상을 의미한다. Priority 스케줄링 방식에서 우선순위가 매우 낮은 프로세스가 ready queue에서 대기하고 있다고 가정해보자.

이 프로세스는 아무리 오래 기다려도 CPU를 점유하지 못할 가능성이 매우 크다. 실제 컴퓨터 환경에서는 새로운 프로세스가 자주 ready queue에 들어온다. 이러한 프로세스가 모두 우선순위가 높은 상태라면 이미 기다리고 있던 우선순위가 낮은 프로세스는 하염없이 기다리고만 있는 상태로 남아있을 수 있다. 



이를 해결하는 방법 중 하나는 **aging**이 있다. ready queue에서 기다리는 동안 일정 시간이 지나면 우선 순위를 일정량 높여주는 것이다. 그러면 우선순위가 매우 낮은 프로세스라 하더라도, 기다리는 시간이 길어질수록 우선순위도 계속 높아지므로 수행될 가능성이 커진다.







### Reference

- [운영체제(OS) 6. CPU 스케줄링](https://velog.io/@codemcd/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-6.-CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81)
