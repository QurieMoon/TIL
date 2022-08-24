Coursera에서 제공되고 있는 [A Crash Course in Causality: Inferring Causal Effects from Observational Data(University of Pennslyvania)](https://www.coursera.org/learn/crash-course-in-causality/home/welcome) 수업을 들으면서 정리한 내용입니다.

------------------------------------

## Propensity score에서의 기본 용어 및 개념
### Propensity score
 - 어떠한 Covariate X의 값이 x일 때(X = x), treatment를 받을 확률  
   &rarr; **Propensity score is a function of covariates!!**
 - 해석
 	+ Covariate X값이 $x_i$인 경우에 propensity score가 0.3이라는 건 해당 covariate 조건 하에서 treatment를 받을 확률이 30%라는 뜻
 - 특징
     + Propensity score은 balancing score이다.

### Estimated Propensity score
 - 계산 방법
     + 가정: Binary treatment(A = 0 or 1)
     + 이 경우, 우리가 추정해야하는 건 P(A=1|X)이다.  
       &rarr; Binary treatment를 가정했기 때문에 response var.이 A이고, predictor var.이 X인 logistic regression model을 사용해서 P(A=1|X)를 추정할 수 있다!  
       &rarr; 이때, 각 subject에 대해 이 predicted probability를 측정하면 바로 이게 estimated propensity score이다.

### Overlap
 - Positivity assumption과 관련되어있음
 - a lack of overlap &rarr; Trim tails!





