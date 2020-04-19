**Q. Context Switching이란?**

- CPU는 한번에 하나의 프로세스만 처리할 수 있다.
- 여러 프로세스를 처리해야 하는 상황에서 현재 진행중인 Task(프로세스, 스레드)의 상태를 PCB에 저장하고 다음에 진행할 Task의 상태값을 읽어 적용하는 과정을 말한다. (**다른 프로세스에게 CPU를 할당해 작업을 수행하는 과정을 말한다.**)
- 과정
  - Task의 대부분 정보는 Register에 저장되고 PCB로 관리된다.
  - 현재 실행하고 있는 Task의 PCB 정보를 저장한다.
  - 다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있다.
- Context Switching은 많은 비용이 소모된다.
  - Cache 초기화
  - Memory mapping 초기화
  - 커널은 항상 실행되어야 한다.
- Context Switching의 비용은 프로세스가 스레드보다 더 많이 든다.
- 이유 : 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 Context Switching 발생시 Stack 영역만 변경을 진행하면 되기 때문이다.