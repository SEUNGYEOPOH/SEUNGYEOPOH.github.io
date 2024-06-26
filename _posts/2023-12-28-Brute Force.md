---
title:  "Brute Force"
categories : Algorithm
tag : Brute Force
# 복수로 하려면 [Python, Blog]처럼 리스트 형태로 할당
toc : true
# toc순서는 markdown header(#) 기준 입니당
toc_sticky : true
toc_label : Content
toc_icon : "fas fa-book-open"
author_profile : false
use_math : true
---

# Brute Force(Exhaustive Search)

## 1 What is Brute Force?
- Brute Force는 말 그대로 난폭한 혹은 정제되지 않은 힘
- 즉, 무차별적인 대입을 통해 결과를 도출하는 Algorithm
- 컴퓨터의 빠른 속도를 이용하여 문제를 풀어나가는 방식
- 모든 가능성을 검토하기에, 완전탐색으로도 불리기도 하고 완전탐색의 한 종류로도 정의된다.
- 현실적으로 모든 경우의 수를 단순한 선형구조인 무차별 대입으로 풀어내기에는 무리가 있다.
- But, 단순 구조 혹은 Solution Space가 적을 경우에는 효과적일 수 있다.

## 2. How to Use?
- solution space를 정의
- Condition 정의 후 Loop
- Condition에 부합하는 solution을 solution space에 추가
- 조건에 맞는 solution을 정리하여, 답을 도출한다.

## 3. Example

### 3.1 BOJ 1816번 암호 키

#### 3.1.1 문제
![image](https://github.com/SEUNGYEOPOH/SEUNGYEOPOH/assets/81912557/9c26771f-73ef-46dd-97b1-20211801f9d4)

- 해당 문제의 경우 입력된 수가 $10^6$보다 큰 소수라면 Yes, 아닐 경우 No를 출력하면 되는 간단한 문제이다.
- 구조화
    - Condition : 2~$10^6$
    - 반복을 통해 입력된 S(target)가 Solution Space에서 한번이라도 나눠지면 False
    - 그렇지 않을 경우 True

#### 3.1.2 해답
```python
n = int(input()) # test case
data =[] # test case space
ans = [] # solution space
for i in range(n):
    da  = int(input()) # n번 s 입력
    data.append(da) # data list에 저장

for i in range(len(data)): # S loop
    target = data[i] # 저장된 S가 차례대로 할당
    dd = "YES" # 기존 State = True
    for j in range(2,10**6+1): # Condition
        if target%j==0: # 약수 존재하는 solution
            dd="NO" # State 변경
            break # 더 이상의 loop는 무의미하므로 종료
    ans.append(dd) # solution space 추가
for i in ans:
    print(i) # 정답 출력
```

### 3.2 BOJ 2017 연세대학교 프로그래밍 경시대회
#### 3.2.1 문제
![image](https://github.com/SEUNGYEOPOH/SEUNGYEOPOH/assets/81912557/4fd0bcf5-a673-4645-945a-bc4244585ed9)

- 구조화
    - 모두 1개 이상이므로 min=1
    - max = n
    - 각 인원이 가질 수 있는 사탕의 범위 정의(1~n개)
    - 택희는 짝수이므로 2부터 n개까지 step은 2


#### 3.2.2 해답 
```python
n=int(input())

a=[i for i in range(1,n+1)] # 남규의 Solution Space
b=[j for j in range(1,n+1)] # 영훈 Solution Space
c=[q for q in range(2,n+1,2)] # 택희 Solution Space


count=0 # 경우의 수 
for i in a:
    for j in b:
        for q in c: 
            if i+j+q==n and i>=j+2: # 3개의 합이 사탕의 총 개수와 일치하며, 남규가 영훈이보다 2개 많을 경우
                count+=1 # 경우의 수 증가


print(count)

```

### 3.3 백준 19532번

#### 3.3.1 문제
![image](https://github.com/SEUNGYEOPOH/SEUNGYEOPOH/assets/81912557/520e118b-a10f-4d0f-91ce-00285337de90)

- 구조화
    - x, y의 condition 

        $-999 \leq x,y \leq 999$

    - loop를 통해 수식을 계산하여 입력된 c,f와 일치하면 출력

#### 3.3.2 해답 
```python
a,b,c,d,e,f = list(map(int, input().split()))

for i in range(-999,1000): # loop
    for j in range(-999,1000): # loop
        if (a*i) + (b*j) ==c and (d*i) + (e*j) ==f: # condition check
            print("%d %d"%(i,j)) 
```
### 3.4 백준 2503번

#### 3.4.1 문제
![screencapture-acmicpc-net-problem-2503-2024-01-07-00_49_00](https://github.com/SEUNGYEOPOH/SEUNGYEOPOH/assets/81912557/58a3f009-340a-40e0-8791-ac796d04d9b3)

- 구조화
    - Brute Force로 풀기위해 코드가 조금 길어졌지만, 어렵지는 않다.
    - 각 1~9까지이므로 각 자리수는 1~9에 해당
    - 자리 수 별 loop 구현
    - loop로 구현 된 값으로 세 자리 수 구성
    - 입력된 hint와 대조 후 ball, strike 계산
    - 계산된 ball, strike와 입력된 ball, strike의 case가 모두 일치하면 count를 증가
    - loop 종료 후 count 출력

#### 3.4.2 해답 
```python
n = int(input())
hint = []
for i in range(n):
    data = list(map(int, input().split()))
    hint.append(data)

answer = 0
for a in range(1,10):
    for b in range(1,10):
        for c in range(1,10):
            if (a == b or b==c or c==a):
                continue
            cnt=0
            for arr in hint:
                ball_count = 0
                strike_count = 0
                number = arr[0]
                strike = arr[1]
                ball = arr[2]
                number = list(str(number))

                if str(a)==number[0]:
                    strike_count+=1
                if str(b)==number[1]:
                    strike_count+=1
                if str(c)==number[2]:
                    strike_count+=1

                if ((str(a)==number[1]) or (str(a)==number[2])):
                    ball_count+=1
                if ((str(b)==number[0]) or (str(b)==number[2])):
                    ball_count+=1
                if  ((str(c)==number[0]) or (str(c)==number[1])):
                    ball_count+=1


                if ball == ball_count and strike == strike_count:
                    cnt+=1

            if cnt==n:
                answer+=1

print(answer)
```