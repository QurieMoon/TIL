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
 - 노드 A와 B가 "associate"되었다는 말은 무슨 말일까? 바로 A와 B를 양끝점으로 가지는 path가 존재하면서 해당 path가 아래 조건을 충족한다는 뜻이다.
   <ul>충족해야하는 조건
      <li>양노드에 모두 information이 유입되어야한다</li>
      <li>양노드에 모두 information이 유입되어야한다</li>

   </ul>

   다른 강의 보고 association 정의 다시 찾고
   코세라 Paths and associations 부터 정리!
   
