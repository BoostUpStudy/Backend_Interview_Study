# CPU 스케줄러



# 설명

멀티프로그래밍에서 CPU 이용률을 최대화 하기 위해, 특정 알고리즘으로 Main memory에 적재되어 **ready queue**에 있는 프로세스를 선택하여 CPU를 프로세스에 할당해주는 것으로, **Short-term scheduler**라고도 한다.



# Dispatcher

CPU 스케줄러의 일부분으로, CPU의 제어권을 프로세스에 주는 작업을 한다.

- context switch

- user mode로 전환

- 유저 프로그램의 적절한 위치로 이동하여 프로그램을 재시작한다.

- Dispatch latency : dispatcher가 한 프로세스를 멈추고 다른 프로세스를 시작하는 시간(짧을 수록 좋음)

  

# CPU Scheduling이 발생하는 상황

- 선점(preemptive) 스케줄링: 프로세스가 강제(비자발)적으로 CPU를 내주는 방식
  
    ![Untitled](https://user-images.githubusercontent.com/58130501/147887039-3827bca7-1315-4dcf-a46f-637f53771f91.png)
    
    - running → ready
    - waiting → ready
- 비선점(nonpreemptive) 스케줄링: 프로세스가 자발적으로 CPU를 내주는 방식
  
    ![Untitled 1](https://user-images.githubusercontent.com/58130501/147887020-80ff370b-66e3-422a-b060-36a109731339.png)
    
    - running → waiting
    
    - running → terminate
    
      
    

# 스케줄링 기준

- CPU utilization(CPU 이용률) - CPU를 얼마나 바쁘게 유지했는지

- Throughput(처리량) - 시간 단위 당 실행시간을 완료한 프로세스의 수

- Turnaround time(수행 시간) - 프로세스가 시작해서 끝날 때까지의 시간

- Waiting time(대기 시간) - 프로세스가 **ready queue**에서 기다린 시간

- Response time(응답 시간) - 프로그램을 수행해서 첫 번째 응답이 나타날 때까지의 시간

  

# 스케줄링 알고리즘 최적화 기준

- Max CPU utilization

- Max throughput

- Min turnaround time

- Min waiting time

- Min response time

  

# 스케줄링 알고리즘



## 비선점형 스케줄링



### First Come, First Served(FCFS) Scheduling

- 먼저 CPU를 요청하는 프로세스에 CPU를 할당하는 방식

- Burst Time이 긴 프로세스가 먼저 요청하면 **convey effect**가 발생됨
  
    ![Untitled 2](https://user-images.githubusercontent.com/58130501/147887067-20bcf973-59ae-48d4-9967-c1f794c4fc7b.png)
    
    ![Untitled 3](https://user-images.githubusercontent.com/58130501/147887074-ce3e61e6-72e1-4392-a46f-e61d29e1c500.png)
    
    **대기 시간**: P1 = 0, P2 = 24, P3 = 27
    
    **평균 대기 시간**: (0+24+27)/3 = 17
    
- Burst Time이 짧은 프로세스가 먼저 요청할수록 유리함
  
    ![Untitled 4](https://user-images.githubusercontent.com/58130501/147887079-706ce285-6f03-4524-b2cf-7b3e8fcbed93.png)
    
    **대기 시간**: P1 = 6, P2 = 0, P3 = 3
    
    **평균 대기 시간**: (6+0+3)/3 = 3
    
- convey effect: 짧은 프로세스가 긴 프로세스 뒤에 기다리게 되는 현상

    

### Shortest-Job-First(SJF) Scheduling

- 짧은 수행 시간을 가진 프로세스를 먼저 처리하는 방식

- 평균 대기 시간이 최소화 됨
  
    ![Untitled 5](https://user-images.githubusercontent.com/58130501/147887057-045f5f3f-360d-4c89-ab11-f030b5d92c02.png)
    
    ![Untitled 6](https://user-images.githubusercontent.com/58130501/147887090-317e5ff8-fd93-4ec3-8a29-5ce304c57e0c.png)
    
    **평균 대기 시간**: (0 + 3 + 9 + 16)/4 =7
    
- 대기 시간이 긴 프로세스는 오래 기다려야 한다.

    

## 선점형 알고리즘

### Shortest Remaining Time First(SRTF) Scheduling

- SJF 알고리즘에서 선점 정책을 도입한 방식
- 잔여시간이 가장 짧은 프로세스를 우선으로 CPU할당을 한다.
- Arrival Time 개념이 추가됨
  
    ![Untitled 7](https://user-images.githubusercontent.com/58130501/147887097-d27faa69-c23d-4db6-b7b9-dfe307a545ac.png)
    
    ![Untitled 8](https://user-images.githubusercontent.com/58130501/147887102-bc31d250-4bb3-41a8-acff-8a5ab1cfb615.png)
    
    평균 대기 시간 : [(10-1)+(1-1)+(17-2)+(5-3)]/4 = 6.5
    
                           수행 시작된 시간 - 이미 처리한 시간 - 도착 시간
    
- 잦은 선점에 대한 문맥 교환 오버헤드 증가

### Priority Scheduling

- 프로세스에 우선순위를 메겨, 우선순위가 높은 프로세스부터 처리하는 방식
- 선점형, 비선점형 모두 존재
- Starvation 문제: 우선순위가 낮은 프로세스는 계속 기다려야한다.
- Aging 기법: 기다리는 시간만큼 프로세스의 우선순위를 높여준다.

### Round Robin(RR) Scheduling

- 각 프로세스는 작은 단위 시간(time quantum)을 가지고 있다. (보통 10-100 ms)

- 단위 시간이 지나면 프로세스는 선점되어 ready queue의 끝으로 이동한다.

- n개의 프로세스가 ready queue 안에 있고, 단위 시간이 q이면, 각 프로세스의 대기시간은 (n-1)q 시간보다 많이 기다리지 않는다.

- 단위 시간이 클 수록 FCFS와 같아지고, 작을 수록 context switch로 인한 오버헤드가 커진다.

  

# Multilevel Queue

- ready queue는 여러 단계의 큐로 나누어져 있다.
  
    ![Untitled 9](https://user-images.githubusercontent.com/58130501/147887111-0664276b-2d94-4a7f-b5d9-31dda5796b33.png)
    
    - 사용자와 상호작용하는 프로세스는 상위 레벨에, 백그라운드로 돌아가는 프로세스는 하위 레벨에 배치한다.
    - 상위 레벨은 주로 RR 알고리즘을, 하위 레벨은 주로 FCFS 알고리즘을 적용한다.
    
- 각 큐마다 스케줄링 알고리즘을 갖고 있다.

- 우선순위가 고정되어 있으면 하위 레벨 queue의 프로세스들은 상위 레벨의 프로세스가 모두 수행되지 않으면 실행되지 않는  **starvation** 현상이 나타남

- 하위 레벨의 프로세스가 실행되고 있어도 상위 레벨에 프로세스가 들어오면 선점된다.

    

# Multilevel Feedback Queue

- Multilevel Queue를 확장한 방식으로, 프로세스는 각 큐를 이동할 수 있다.
- aging 기법을 사용하여 starvation 현상을 방지한다.
- Parameter
    - 큐의 수
    
    - 각 큐의 스케줄링 알고리즘
    
    - 언제 프로세스 우선순위를 높이는 지 결정하는 메소드
    
    - 언제 프로세스 우선순위를 낮추는 지 결정하는 메소드
    
    - 프로세스가 서비스를 필요로 할 때 프로세스가 들어갈 큐를 결정하는 메소드
    
      
    

# Multiple-Processor Scheduling

- 여러 개의 CPU를 사용하는 시스템에서의 스케줄링 방법
- 제약: 다중프로세서 내의 동질의 프로세서들
- Asymmetric multiprocessing 비대칭 다중처리
    - Master-Slave 구조
    - Master 프로세서가 모든 스케줄링 결정을 하고, Slave 프로세서들은 그 결정에 따른다.
    - 오직 한 프로세서만 시스템 자료 구조에 접근하여 데이터 공유의 필요성을 배제한다.
- Symmetric multiprocessing(SMP) 대칭 다중처리
    - 각 프로세서가 자기 스케줄링을 한다.
    - 모든 프로세서는 common ready queue에 있거나, 각자의 private queue에 있게 된다.
    - **common queue**는 모든 프로세서가 접근할 수 있어서 경쟁 상태를 야기하기 때문에 lock이 필요하다.
    - **private queue**는 큐마다 부하의 양이 다르다.
- Processor affinity 프로세서 친화성
    - 프로세스는 현재 실행되고 있는 프로세서에 친화성을 가진다.
      
        ![Untitled 10](https://user-images.githubusercontent.com/58130501/147887120-680e5177-5eda-4d4a-8cdc-93b2f57b9ec6.png)
        
        특정 CPU에 할당된 프로세스를 CPU가 있는 가장 가까운 메모리에 할당하여 가능한 빠른 메모리 엑세스를 제공한다.
        
    - soft affinity 약한 친화성
    - hard affinity 강한 친화성
- Load Balancing 부화 균등화
    - SMP이면, 효율성을 위해 모든 CPU를 로드해야한다.
    
    - SMP 시스템에서 부하가 고르게 분산되도록 한다.
    
    - Push migration : 특정 테스크가 각 프로세서의 로드를 감시하다가 과부하된 CPU에서 다른 CPU들로 프로세스를 옮긴다.
    
    - Pull migration : idle상태의 프로세서들은 바쁜 프로세서에서 대기중엔 프로세스들을 가져온다.
    
      

---

- 참고자료
  
    [https://velog.io/@ss-won/OS-CPU-Scheduler와-Dispatcher](https://velog.io/@ss-won/OS-CPU-Scheduler%EC%99%80-Dispatcher)
    
    [https://velog.io/@jacob0122/CPU-Scheduling-Scheduler](https://velog.io/@jacob0122/CPU-Scheduling-Scheduler)
    
    [https://jhnyang.tistory.com/372](https://jhnyang.tistory.com/372)
    
    [https://imbf.github.io/computer-science(cs)/2020/10/18/CPU-Scheduling.html](https://imbf.github.io/computer-science(cs)/2020/10/18/CPU-Scheduling.html)
    
    [https://hyunah030.tistory.com/4](https://hyunah030.tistory.com/4)
    
    [https://haun25ne.tistory.com/52](https://haun25ne.tistory.com/52)
    
    운영체제 공룡책