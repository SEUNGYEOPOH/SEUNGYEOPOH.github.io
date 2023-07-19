---
title:  "Probability and probability distribution"
categories : Math
tag : Mathematical Statistics
# 복수로 하려면 [Python, Blog]처럼 리스트 형태로 할당
toc : true
# toc순서는 markdown header(#) 기준 입니당
toc_sticky : true
toc_label : Content
toc_icon : "fas fa-book-open"
author_profile : false
use_math : true
---

**[Notification]** 
<br/>
<u>Hello world!, I'm going to read the contents and papers I'm studying and record them here!</u>
{: .notice--success}



# 1. Probability and probability distribution

##  1.1 Probability

### 1.1.1 The Basics of Probability

- Sample Space(S, 표본공간) : 확률 실험에서 모든 가능한 결과들의 집합.

- Event(사건, 사상) : Sample Space의 부분집합 

- Elementary Event(근원사건) : Event 중 한 개의 원소로 이루어진 Event 

[Ex. 1-1]  주사위 1개를 던진다고 가정하고 Sample Space를 S, 짝수가 나오는 Event를 A라고 정의할 때,
- $ S $ = {$1, 2, 3, 4, 5, 6$} 
- $ A $ = {$2, 4, 6$}  
  - 여기서 사건 A가 발생한다는 의미는 2 or 4 or 6 중 하나가 나온다는 것
- Event의 기본 연산
  - Union event of A and B : $A\cup B$  = {$\{ w \,\vert\, w\in A \text{ or } w\in B\}$}
  - Intersection event of A and B : $A\cap B$  = {$\{ w \,\vert\, w\in A \text{ and } w\in B\}$}
  - Complementary event of A : $A^{c}$  = {$\{ w \,\vert\, w\notin A \text{ and } w\in S\}$}

- Probability는 사건이 일어날 가능성을 나타내는 Mathematical Measure

**[Definition 1-1] Classical definition of probability(Laplace)** <br/>


- n개의 원소가 있는 sample space $S$ = {$e_1, \cdots, e_n$}에서 각 Elementary Event $e_i$가 일어날 가능성이 같을 경우, k개의 원소로 구성된 사건 A가 일어날 확률은 아래와 같다.
\\[
P[A] = \frac{k}{n}
\\]

- sample space의 element를 Sample point(표본점)라고 부르기도 한다.<br/> 사건 A의 sample point를 n(A)로 나타내면 사건 A의 Probability는 아래와 같다.

\\[
P[A] = \frac{n(A)}{n(S)}
\\]

[Ex 1-2] 주사위 1개를 던질 때, 짝수가 나올 확률
- $ S $ = {$1, 2, 3, 4, 5, 6$}, $n(S) = 6$
- $ A $ = {$2, 4, 6$}, $n(A) = 3$ <br/>

\\[
  \therefore P[A] = \frac{1}{2}
\\]


**[Definition 1-2] Frequentism definition of probability**<br/>
- probability를 사건 A가 일어나는 빈도의 극한비율로 정의<br/>
- 실험 횟수를 n이라고 정의할 때, 사건 A가 일어날 확률은 아래와 같다.

\\[
\displaystyle P[A] = \\lim_{n\rightarrow \infty}\frac{1}{n} \times \text{[The number of occurrences of event A]}\
\\]

**[Definition 1-3] Axiomatic definition of probability(Kolmogorov)** <br/>


- sample space S에서 다음의 axiom(공리)를 만족하는 P[A]를 Event A의 probability라고 한다. <br/>

  - 공리 1.   $ P[S] = 1 $ 
    - 어떤 실험에서도 sample space S는 반드시 일어난다.
  - 공리 2.   $ 0 \leq P[A] \leq 1 $ 
    - 어느 event도 probability는 음수가 될 수 없다.
  - 공리 3.   상호 배반 사건인 $ A_1, A_2, A_3, \cdots$에 대하여 
    - 상호 배반 사건에 대해 합사건의 probability는 각각의 probability의 합과 같다.
\\[
  P \left [ \bigcup_{i=1}^{\infty } A_i\right] = P[A_1] + P[A_2] + \cdots 
\\]

### 1.1.2 Calculation of probability
**[Rule. 1-1]**
\\[
  \text{(1)     }P[A^c] = 1-P[A] 
\\]

\\[
  \text{(2)     }P[\varnothing] = 0 
\\]

**[Rule. 1-2]**
\\[
  \text{(1)     } A \subset B \text{이면} P[A] \leq P[B]
\\]

\\[
  \text{(2)     } P \left [A\cup B  \right ] = P[A] + P[A] - P[A \cap B]
\\]

[Ex 1-3] Coin을 2번 던져 H, T가 나오는 실험
\\[
  S = {(H,H), (H,T), (T,H), (T,T)}  
\\]

여기서 A를 ${(H,H),(H,T)}$ B를 ${(H,H),(T,H)}$라고 가정했을 때, $P[A \cup B]$는?
\\[
  A \cap B = (H,H)
\\]

\\[
  P[A \cap B] = \frac{1}{4}
\\]
Rule 1-2.(2)에 의해 $P \left [A\cup B  \right ] = P[A] + P[A] - P[A \cap B]$
\\[
  \therefore P[A \cup B] = \frac{1}{2} + \frac{1}{2} - \frac{1}{4} = \frac{3}{4}
\\]

### 1.1.3 Conditional Probability and Independent Events
**[Definition 1-4] Conditional probability(조건부확률)**<br/>
- event A에 대해 B의 Conditional probability는 아래와 같다.<br/>
\\[
  P \left\[ B \,\vert\, A  \right\] = \frac{P[A \cap B]}{P[A]}, \text{ (s.t. } P[A]>0 \text{)}
\\]
- Conditional probability의 의미
  - event A가 발생했다면 A이외에는 <U>일어날 수 없다.</U> 따라서 이런 조건하에 A가 새로운 sample space 되고, **A내에서 $A \cap B$에 있는 sample point(element)가 발생할 때 B가 일어나게 된다.**
  - 그러므로 A하에서 B의 Conditional probability는 $P[A \cap B]$와 $P[A]$의 비로 표현된다.

[Ex 1-4] 어느 대학 코딩테스트 대회에 참가한 30명의 학생 중 문제를 모두 풀어낸 학생과 다 풀지 못한 학생의 수는 아래와 같다.


|구분|남학생|여학생|
|:---:|:---:|:---:|
|다 푼 사람|12|11|
|다 못 푼 사람|3|4|


참가한 학생 중 임의로 선택한 학생이 남성이었을 때, 이 학생이 문제를 모두 풀어낼 확률을 구하라.

- 모두 푼 event를 A, 남성일 경우를 B라고 가정
- $P \left\[ B \,\vert\, A  \right\] = \frac{P[A \cap B]}{P[A]}$
- $ n(A \cap B) = 12$, $n(B) = 15$ <br/>

\\[
  \therefore P \left\[ B \,\vert\, A  \right\] = \frac{12}{15} = \frac{4}{5}
\\]

#### Example.



## 1.2 Random variables and probability distributions

### 1.2.1 Random variables



### 1.2.2 Probability distributions



#### Example.

## 1.3 Expected value and moment

### 1.1.1 Expected value



### 1.1.2  Variance



### 1.1.3 Moment generating function



#### Example.

## 1.4 Multidimensional distribution

### 1.4.1 Joint distribution of two random variables



### 1.4.2 Independence of two random variables and conditional distribution



### 1.4.3 Covariance and Correlation



### 1.4.4 Linear Combination of Random Variables



#### Example.
