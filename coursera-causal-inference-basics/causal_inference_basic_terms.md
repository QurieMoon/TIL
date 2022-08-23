Coursera에서 제공되고 있는 [A Crash Course in Causality: Inferring Causal Effects from Observational Data(University of Pennslyvania)](https://www.coursera.org/learn/crash-course-in-causality/home/welcome) 수업을 들으면서 정리한 내용입니다.

------------------------------------

## 인과관계 추론에서의 관심사
 - causal effect of some treatment A on some outcome Y

## 인과관계 추론에서 알아야하는 기본 용어 및 개념
### Treatment
 - 처리

### Potential outcomes
 - 특정 treatment를 가했을 때, 관측할 수 있는(would) outcome
 - Notation
   - Y<sup>a</sup>: Treatment A 상태를 a로 했을 때(A = a) 관측될 수 있는 outcome
   - 예) Treatment A가 영양제 섭취 여부라고 생각해보자. 이때, 영양제 섭취는 1, 섭취 안 함은 0이라고 표시하자. 따라서 영양제 섭취 case는 A = 1이라고 쓸 수 있다. 또한, 위 케이스에 대한 potential outcome은 영양제를 섭취한 경우에 관측할 수 있는 결과로, Y<sup>1</sup> 라고 표기할 수 있다.

### Counterfactuals(Counterfactual outcomes)
 - 실제 가한 처리가 아닌 다른 처리를 가했을 때, 예측되었을 수 있는 결과
 - Treatment A가 취할 수 있는 값이 1 아니면 0이라고 하자. 또한, 실제로 가한 treatment가 1이라고 하자.(A=1) 이때, counterfactual outcome 은 Y<sup>0</sup>이다.  
   &rarr; **즉, counterfactual outcome은 observed outcome의 반대 결과라고 생각할 수 있다.**
 - 실제 처리가 가해지기 전에 가능한 모든 outcome은 **"potential outcome"**이다.

### Causal Effect란 무엇일까?
 - Treatment A에 대한 potential outcome 간에 차이가 있을 때, causal effect가 존재한다고 한다.  
   &rarr; 예를 들어, 진정 여부(outcome)에 대한 청심환의 효과가 있는지 알아본다고 하자. 이때, 청심환을 먹은 경우와 먹지 않은 경우에 매핑되는 potential outcome 간에 차이가 있다면 청심환 섭취에 대한 causal effect 가 존재한다고 할 수 있을 것이다.  
   &rarr; 문제는! **이러한 차이가 정말 청심환 때문인지 판단이 어렵다.** 예를 들어서, 어쩌면 청심환을 먹지 않았어도 진정될 상황이었을 수도 있기 때문이다.  
   &rarr; **따라서 실제로 관측한 결과의 반대 결과, 즉 counterfactual 을 알아야한다.** 그렇지만 또 문제는? 현실에서는 한개의 potential outcome만을 관측할 수 있다는 것!  
   &rarr; **이게 바로 Fundamental problem of causal inference**이다.  
   &rarr; 따라서 문제를 individual-level이 아닌, population-level로 끌어올려서 보자! 즉, Average causal effect에 대해 생각해보자.

### Average causal effect
 - Population-level
 - $E[Y^1-Y^0]$
 - **주의**
   - $E[Y^1-Y^0]\ !neq\ E[Y|A=1]-E[Y|A=0]$ 

### Causal Effect of treatment on the treated
 - $E[Y^1-Y^0|A=1]$

### Causal Assumptions
<ol>
  <li>Stable Unit Treatement Value Assumption(SUTVA)</li>
    - No interference btn units
    - One version of treatment
  <li>Consistency</li>
    - $Y^a = $(observed outcome when the treatment was actually A=a)
  <li>Ignorability</li>
    - Covariate X가 통제된 상황에서는 treatment assignment가 random하게 이루어진다.(Potential outcome에 상관없이 treatment assignment가 이루어진다)
  <li>Positivity</li>
    - $P(A=a|X=x) > 0$ for all a and x
</ol>
 

### Confounder
 - Treatment와 outcome 모두에 영향을 주는 변수!
 - 따라서 ignorability assumption을 지키기 위해서 이러한 confounder를 통제해야한다..!
 - 이때, 이러한 confounder로 분류될 변수를 식별해내려는 상황에서 유용하게 사용할 수 있는 게 바로 causal graph!

-----------------------------------------

Causal graphs 관련 내용은 다음 문서에서 살펴보겠습니다.
