---
title:  "Chap.1 Probability and probability distribution"
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

- Probability는 사건이 일어날 가능성을 나타내는 Mathematical Measure

- Event의 기본 연산
  - Union event of A and B : $A\cup B$  = {$\{ w \,\vert\, w\in A \text{ or } w\in B\}$}
  - Intersection event of A and B : $A\cap B$  = {$\{ w \,\vert\, w\in A \text{ and } w\in B\}$}
  - Complementary event of A : $A^{c}$  = {$\{ w \,\vert\, w\notin A \text{ and } w\in S\}$}

**[Definition 1-1] Classical definition of probability(Laplace)** <br/>


- n개의 원소가 있는 sample space $S$ = {$e_1, \cdots, e_n$}에서 각 Elementary Event $e_i$가 일어날 가능성이 같을 경우, k개의 원소로 구성된 사건 A가 일어날 확률은 아래와 같다.
\\[
P[A] = \frac{k}{n}
\\]

- sample space의 element를 Sample point(표본점)라고 부르기도 한다.<br/> 사건 A의 sample point를 n(A)로 나타내면 사건 A의 Probability는 아래와 같다.

\\[
P[A] = \frac{n(A)}{n(S)}
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

### 1.1.3 Conditional Probability and Independent Events
**[Definition 1-4] Conditional probability(조건부확률)**<br/>
- event A에 대해 B의 Conditional probability는 아래와 같다.<br/>
\\[
  P \left\[ B \,\vert\, A  \right\] = \frac{P[A \cap B]}{P[A]}, \text{ (s.t. } P[A]>0 \text{)}
\\]

+ Multiplication theorem(승법공식)
\\[
  P[A \cap B] = P \left\[ B \,\vert\, A  \right\]P[A] = P \left\[ A \,\vert\, B  \right\]P[B]
\\]

- Conditional probability의 의미
  - event A가 발생했다면 A이외에는 <U>일어날 수 없다.</U> 
  - 따라서 이런 조건하에 A가 새로운 sample space 되고, **A내에서 $A \cap B$에 있는 sample point(element)가 발생할 때 B가 일어나게 된다.**
  - 그러므로 A하에서 B의 Conditional probability는 $P[A \cap B]$와 $P[A]$의 비로 표현된다.

**[Rule. 1-3] total probability theorem(전확률 공식)**
- $A_1, \cdots, A_n$이 sample space S의 한 분할일 때, 임의의 사건 B에 대하여 다음이 성립한다.
\\[
  P[B] = P \left\[ B \,\vert\, A_1  \right\]P[A] + \cdots + P \left\[ B \,\vert\, A_n  \right\]P[A_n] 
\\]
- 분할이란 $A_1, \cdots, A_n$이 아래의 조건을 만족할 때, $A_1 \cdots, A_n$을 S의 분할이라고 말함.<br/>
(i)$A_i \cap A_j = \emptyset, i \neq j$<br/>
(ii)$A_1 \cup \cdots \cup A_n = S$<br/>


**[Rule. 1-4] Bayes' theorem**
- $A_1, \cdots, A_n$이 sample space S의 한 분할이고, 각 i에 대해 $P[A_i] > 0$이며 $P[B] > 0$ 일 때 다음 등식이 성립한다.
\\[
  P \left\[ A_k \,\vert\, B  \right\] = \frac{P \left\[ B \,\vert\, A_k  \right\]P[A_k]}{ \sum_{i=1}^{n}P\left [B \,\vert\, A_i  \right ]P[A_i]}
\\]
- **[Bayes' theorem] 증명**
\\[
\begin{aligned}
P \left\[ A_k \,\vert\, B  \right\] &= \frac{P[A_k \cap B]}{P[B]} \\\\\\
&=\frac{P \left\[ B \,\vert\, A_k  \right\]P[A_k]}{P[B]} \text{  (multiplication theorem)}  \\\\\\
&=\frac{P \left\[ B \,\vert\, A_k  \right\]P[A_k]}{\sum_{i=1}^{n}P\left [B \,\vert\, A_i  \right ]P[A_i]} \text{  (total probability theorem)}
\end{aligned}
\\]

<!-- ## 1.2 Random variables and probability distributions

### 1.2.1 Random variables



### 1.2.2 Probability distributions

## 1.3 Expected value and moment

### 1.1.1 Expected value



### 1.1.2  Variance



### 1.1.3 Moment generating function


## 1.4 Multidimensional distribution

### 1.4.1 Joint distribution of two random variables



### 1.4.2 Independence of two random variables and conditional distribution



### 1.4.3 Covariance and Correlation



### 1.4.4 Linear Combination of Random Variables -->

