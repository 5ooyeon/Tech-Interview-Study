<details>
  <summary><strong>스케줄링 정책들의 비교를 위해 어떤 평가 기준들이 존재하나요?</strong></summary>

<br>

  ### 반환시간 (turnaround time)  
  작업을 완료한 시간에서 작업이 시스템에 도착한 시간을 뺀 시간으로, 성능에 대한 평가 기준입니다.
  
<br>

  ### 공정성 (fairness) 
  모든 작업들이 골고루 자원을 할당받아 진행되고 있는지를 평가하는 평가 기준입니다. 반환시간과는 상충되는 평가 기준입니다.

<br>

  ### 응답 시간 (response time) 
  작업이 도착했을 때부터 처음 스케줄 될 때까지의 시간을 측정한 것으로, 시스템과의 상호작용이 원활한지를 평가하는 성능에 대한 평가 기준입니다.

<br>

  ### 추가요소들
  
  * 처리량 (Throughput) : 단위 시간당 처리되는 작업 수.

  * CPU 이용률 (CPU Utilization) : CPU가 얼마나 효율적으로 사용되고 있는지 평가.

</details>


<details>
  <summary><strong>비선점형 스케줄러와 선점형 스케줄러에 대해 설명해주세요.</strong></summary>

<br>

  ### 비선점형 스케줄러
  한 번 CPU를 할당받은 작업이 실행을 끝마칠 때까지 CPU를 계속 점유하며, 현재 실행중인 작업은 중단되지 않습니다.
  
<br>

  ### 선점형 스케줄러
  현재 실행 중인 작업을 중단하고 우선순위가 높은 작업이나 다른 조건에 따라 새로운 작업을 실행하며, 작업이 종료되기 전에 CPU를 할당받을 기회를 다른 작업으로 전환할 수 있습니다.

</details>


<details>
  
  <summary><strong>스케줄링 방법들 중 FIFO와 SJF, STCF에 대해서 각 방법의 개념 및 특징, 단점들을 설명해주세요.</strong></summary>

<br>

  ### FIFO (First In First Out)
  * 정의 : FIFO는 가장 먼저 도착한 작업을 가장 먼저 처리하는 비선점형 스케줄링 방식입니다. 작업이 도착한 순서대로 순차적으로 처리됩니다.
  특징 : 간단하고 구현이 쉽습니다.
  단점 : 긴 작업이 먼저 도착한 경우 뒤에 대기하는 짧은 작업들이 오랫동안 대기하게 되는 **Convoy Effect**가 발생할 수 있습니다. 결과적으로 반환시간과 응답시간이 비효율적으로 길어질 수 있습니다.

<br>

  ### SJF (Shortest Job First)
  * 정의 : SJF는 작업의 실행 시간이 가장 짧은 작업부터 처리하는 방식으로, 반환시간(Turnaround Time)을 최소화하는 데 매우 효과적입니다.
  * 특징 : 짧은 작업이 빠르게 완료되므로 시스템의 전반적인 효율이 높아집니다.
  * 단점 : 작업 길이를 사전에 정확히 알기 어렵고, 긴 작업이 계속 뒤로 밀려 **기아 현상(Starvation)**이 발생할 가능성이 높습니다. 또한, 비선점형 방식이기 때문에 작업 중간에 새로운 작업이 도착하더라도 이미 실행 중인 작업이 완료될 때까지 기다려야 합니다.

<br>

  ### STCF (Shortest Time to Completion First)
  * 정의 : STCF는 SJF의 선점형 버전으로, 작업의 남은 실행 시간이 가장 짧은 작업을 우선적으로 실행합니다.
  * 특징 : 반환시간 최적화가 SJF보다 더 뛰어나며, 작업 도중에 새로 도착한 짧은 작업이 기존 작업보다 먼저 처리될 수 있습니다.
  * 단점 : 선점으로 인해 스케줄링 오버헤드가 발생할 수 있으며, 작업의 남은 실행 시간을 예측하기 어렵다는 점에서 구현 난이도가 높아질 수 있습니다.


</details>

<details>
  <summary><strong>Convey Effect와 Starvation에 대해서 정의 및 원인과 해결방법에 대해 설명해보세요.</strong></summary>

<br>

  ### Convey Effect
  * 정의 : 하나의 긴 작업이 앞에 위치함으로 인해 뒤에 대기 중인 짧은 작업들이 오래 기다리는 현상입니다.
  * 원인 : 주로 FIFO 스케줄링에서 발생하는 문제로, 긴 작업이 CPU를 오랫동안 점유하면, 짧은 작업들이 처리되지 못하고 대기 상태에 머무르는데 이로 인해 발생하게 되니다.
  * 해결방법 : **SJF** 또는 **STCF**와 같은 알고리즘을 통해 짧은 작업을 먼저 처리함으로써 문제를 완화할 수 있습니다.

  ### Starvation
  * 정의 : 특정 작업이 자원을 계속 할당받지 못해 무한히 대기하는 상태를 의미합니다.
  * 원인 : 주로 우선순위 기반 스케줄링에서 발생하는 문제로, 자원의 우선순위가 낮은 작업이 우선순위가 높은 작업들에 의해 지속적으로 밀려날 때 발생합니다.
  * 해결방법 : **Aging**을 활용하여 해결할 수 있습니다.

  * Aging: 대기 시간이 길어질수록 작업의 우선순위를 점진적으로 높여주는 방식.
    
</details>


<details>
  <summary><strong>RR에 대해 설명해보고, STCF나 SJF와의 차이를 설명해주세요.</strong></summary>

<br>

  ### RR (Round Robin)
  RR은 **타임 슬라이스(Time Slice)**를 기반으로 한 선점형 스케줄링 알고리즘입니다. 각 작업에 동일한 시간 단위(타임 슬라이스) 동안 CPU를 할당하며, 타임 슬라이스가 끝나면 해당 작업은 정지되고, 다음 작업이 실행됩니다.이를 통해 **공정성**이 보장되며, 모든 작업이 CPU를 골고루 할당받습니다. 대화형(interactive) 시스템에서 **응답 시간**을 최소화하는 데 효과적입니다. 하지만 짧은 작업이라도 타임 슬라이스가 여러 번 반복될 수 있으므로 **반환시간**은 비효율적일 수 있습니다. 
  타임 슬라이스의 크기에 따라 성능이 달라지며, 너무 짧으면 스케줄링 오버헤드 및 문맥교환비용이 커지고 너무 길면 비선점형 스케줄링에 가까워져 응답 시간이 길어집니다.

  * 문맥교환 : CPU가 하나의 작업(Process)에서 다른 작업으로 전환할 때 발생하는 과정으로, CPU 레지스터, 프로그램 카운터, 메모리 상태 등을 저장하고 복원하는 작업이 필요합니다. 그리고 이때 추가적인 시스템 자원을 사용하는데, 이를 문맥교환비용이라고 합니다.

  ### 차이

  * 공정성
  RR은 모든 작업에 순서대로 CPU를 배정하니까 공정한 반면, STCF와 SJF는 짧은 작업 위주로 처리하니까 공정성은 떨어집니다.

  * 효율성(반환시간 최적화)
  STCF와 SJF는 짧은 작업을 먼저 끝내기 때문에 전체 반환시간을 줄이는 데 탁월하지만 RR은 효율성보다는 응답성을 중시하므로 반환시간은 길어질 수 있습니다.

  * 선점 여부
  RR과 STCF는 선점형이라서 작업 도중에도 새로운 작업이 오면 우선순위를 바꿀 수 있으나 SJF는 비선점형이라 작업이 시작되면 끝날 때까지 CPU를 점유해 현재 작업을 바꿀 수 없습니다.

  * 응답 시간
  RR은 빠르게 작업 간 순환하므로 대화형 시스템처럼 응답이 중요한 경우 적합합니다. 반면 STCF는 짧은 작업에 빠르게 응답하지만 긴 작업은 밀릴 가능성이 높으며, SJF는 긴 작업에 대한 응답이 느려질 수 있습니다.

  * 문맥교환비용  
  RR은 타임 슬라이스가 짧을수록 작업 간 전환이 자주 발생하여 **문맥교환비용**이 커질 가능성이 높은 반면, SJF는 비선점형 스케줄링이기 때문에 문맥교환이 발생하지 않아 비용이 최소화됩니다. STCF는 선점형이지만 남은 실행 시간을 기준으로 작업을 선택하므로, 문맥교환 빈도가 RR보다는 낮아 문맥교환비용이 비교적 적게 발생합니다.

  * 스케줄링 오버헤드  
  RR은 단순히 준비 큐의 순서대로 작업을 실행하므로 **스케줄링 오버헤드**가 상대적으로 적습니다. SJF와 STCF는 작업의 실행 시간을 예측하거나 남은 시간을 계산하는 작업이 필요하므로 스케줄링 오버헤드가 더 크며, 특히 STCF는 선점형 특성상 새로운 작업이 도착할 때마다 우선순위를 재조정해야 하므로 RR보다 높은 오버헤드를 가질 수 있습니다.

</details>

