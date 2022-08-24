Coursera에서 제공되고 있는 [A Crash Course in Causality: Inferring Causal Effects from Observational Data(University of Pennslyvania)](https://www.coursera.org/learn/crash-course-in-causality/home/welcome) 수업을 들으면서 정리한 내용입니다.  

이번 문서에서는 causal graph 관련 내용을 집중적으로 살펴보겠습니다.

------------------------------------

## Causal graph에서의 기본 용어 및 개념
### Node,edge
주어진 causal graph가 아래와 같다고 하자.  
<center>A &rarr; Y</center>  
  
A, Y: nodes(vertices, variables)  
arrow: link(edge, directed path)  
 - 위와 같이 directed edge가 있는 그래프는 directed graph
 - 위처럼 연결된 nodes를 adjacent하다고 한다.

 ### Path
  - 강의를 들어보면 path는 한 개의 vertex에서 다른 vertex로 가는 방법이라고 한다. 그런데, 이상한 부분이 있다? 아래 예시를 보자.
    <center>W &larr; Z</center>
  자, 위 상황에서 W에서 Z로 가는 path는 몇 개일까? 직관적으로 보이듯이 1개이다. 그렇다면 Z에서 W로 가는 path는 몇 개일까?   0개일까? 땡! 오답이다.  
  **강의에 따르면 Z에서 W로 가는 path는 1개이다.** 이부분이 정말 이해가 안 갔는데, [관련 discussion](https://www.coursera.org/learn/crash-course-in-causality/discussions/forums/CUAFygtMEee34QowGm8Gmg/threads/5tAtKr8kEeeA8BKEefIB9g)을 찾았다. 해당 discussion을 참고해보면 말에 따르면, 그냥 "path"를 이야기 할때는 화살표의 방향을 무시하고 생각하면 된다. 사실 이 부분이 동의가 어려웠다.. 왜냐하면 backdoor path 등을 셀 때는 또 화살표 방향을 고려하는 것같기 때문이다 ㅠㅠㅠ 그렇지만 다른 강의에서도 path를 따질 때, 화살표의 방향을 참고하지 않았다. 추가 참고 강의](https://youtu.be/BY2DfBrOi-Q?t=127)

  - 다른 강의도 참고해보니, **화살표의 방향을 고려한 path는 directed path라고 별도 명시**를 하는 것으로 보인다.

  - Types of paths
    <ul>
      <li>Forks</li>
      <li>Chains</li>
      <li>Inverted forks</li>
    </ul>

### DAGs
 - Directed Acyclic Graphs
 - No undirected paths, No cycles
 - **Causal Inference에서 실제적으로 사용할 형태로 보인다**
   &rarr; **DAG에서 봐야할 것: 변수간 (조건부) 독립 여부**
 - DAG의 특징: joint probability distribution과 compatible하다. 그렇지만 특정 probability distribution과 대응되는 DAG는 unique하지 않을 수 있다.

### Parent, child, ancestor, descendant

### Association
 - 노드 A와 B가 "associate"되었다는 말은 무슨 말일까? 바로 A와 B를 양끝점으로 가지는 path가 존재하면서 해당 path가 아래 조건 중 하나를 충족한다는 뜻이다.
   <ul>충족해야하는 조건
      <li>양노드에 모두 information이 유입되어야한다</li>
      <li>하나의 노드에 information이 다른 하나의 node로 유입되어야한다</li>
   </ul>

 - 그렇다면 association 이 아닌 관계는 어떤 게 있을까? 예시로 inverted fork 형태를 떠올릴 수 있다.  
   <center>A &rarr; B &larr; C</center>  
  이때, 위 B를 **collider** 라고 한다.

### Collider
 - Collider bias: Collider를 통제함으로써 발생하는 문제 상황을 가리키는 듯(불필요한 association이 생기는 문제 상황)
 - Path 중간에 collider가 있다면 노드 간 association은 없어보인다.

### Blocked
 - Block 은 condition 을 취함으로써 이루어진다.  
   &rarr; 변수 A에 condition을 취했다는 말은 **변수 A를 통제했다는 말과 같다!**
 - <주의> Collider에 condition 을 취할 경우, 새로운 association이 생긴다!!

### D-separation
 - 어떤 **path**가 어떤 노드의 집합 C에 의해서 d-separated 되었다는 말은 C의 원소 vertices에 의해서 이 path가 block 되었다는 뜻이다.
 - 마찬가지로, A와 B라는 두개의 노드가 어떤 노드의 집합 C에 의해서 d-separated 되었다는 말은 C에 속하는 vertices에 의해서 A와 B사이에 **모든** path가 막혔다는 뜻이다.  
   &rarr; 즉, C에 condition이 취해졌을 때, A와 B는 독립이다.

### Frontdoor path
 - A frontdoor path from A to Y: A에서 출발하는 화살표로 시작되는 path
 - 예시: A &rarr; Z &rarr; Y
 - **이 frontdoor path가 우리가 목표하는 treatment effect를 나타낸다!**  
   &rarr; 따라서 이 frontdoor path는 block 하면 안 된다.

### Backdoor path
 - A backdoor path from A to Y: A에서 Y로 가는 path인데, A로 들어가는 화살표를 포함한 path
 - 예시: A <- X -> Y
 - 이러한 backdoor path가 A와 Y의 관계를 confounding 한다 &rarr; **Backdoor path를 blocking 해야한다!** (이 작업이 사실상 confounder를 controlling하는 작업이라고 생각할 수 있다)

### Backdoor path criterion
 - How to block all backdoor paths from treatment to the outcome
 <ul>
   <li>Treatment에서 outcome으로 가는 모든 backdoor path 를 블록하면서</li>
   <li>Treatment의 descendant는 confounder 집합에 포함시키지 않는 confounder set을 찾아야함!</li>
 </ul>

 - 이러한 backdoor path criterion은 반드시 unique하지는 않다.
 
### Disjunctive cause criterion
 - DAG의 전체 형상을 모를 때, 대안으로 사용할 수 있는 방법
   &rarr; 전체 그래프를 몰라도 treatment(A) 혹은 outcome(Y)에 영향을 주는 변수들만 알면 된다.

 - 한계점
   <ul>
     <li>이러한 set이 존재하지 않을 수도 있고</li>
     <li>A 혹은 Y에 영향을 끼치는 모든 variables을 식별할 수 있어야함</li>
   </ul>






