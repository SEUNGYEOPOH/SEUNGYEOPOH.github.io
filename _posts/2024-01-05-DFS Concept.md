---
title:  "DFS Concpet"
categories : Algorithm
tag : DFS
# 복수로 하려면 [Python, Blog]처럼 리스트 형태로 할당
toc : true
# toc순서는 markdown header(#) 기준 입니당
toc_sticky : true
toc_label : Content
toc_icon : "fas fa-book-open"
author_profile : false
use_math : true
---

# Depth First Search

## 1. What is Depth First Search?
- Graph Search
    - Start Node와 Graph가 주어졌을 때 Edge를 통해 방문할 수 있는 Node를 찾는 문제
    - BFS와 DFS가 존재한다.
- DFS
    - Start Node에서 Depth를 기준으로 탐색
    - 즉 Tree를 수직으로 우선 탐색하며 leaf node에 다다르면, 같은 Edge를 공유하는 동일 Depth 상 노드를 탐색

<p align="center"><img src = "https://github.com/SEUNGYEOPOH/SEUNGYEOPOH/assets/81912557/b1f6a1c9-fa61-4977-9107-cd161700cf21" width = "50%" height = "50%" ></p>

## 2. How to Use?
- Graph 형태 구현을 위해 adjacency list 구현
    - adjacency list란?
        - Graph 표현을 위해 Edge를 공유하는 Node를 list형태로 표현한 list
        - 위의 그림의 adjacency list
        ```python
            [[1] : [2,5,9]
             [2] : [1,3]
             [3] : [2,4]
             [4] : [3]
             [5] : [1,6,8]
             [6] : [5,7]
             [7] : [6]
             [8] : [5]
             [9] : [1, 10]
             [10] : [9]
            ]
        ```
- 탐색 여부 확인을 위한 State list 구현
- Start Node를 State list에서 방문처리
- adjacency list를 통해 Edge를 공유하는 다음 Node로 이동 (Recursive Function)
- State list 상 방문처리가 된 Node라면 Skip, 아니라면 방문처리 후 탐색 반복
- 참고로 Python의 maximum recursion depth는 default가 1000이다.
    - 추가적인 탐색을 원할경우 sys.setrecursionlimit(value)를 통해 늘릴 수 있다.

## 3. Base Code
### DFS
```python
n= int(input()) # Node 개수
m= int(input()) # Node간 관계
graph = [[] for i in range(n+1)] # adjacency list
state = [0 for _ in range(n+1)] # State list
for _ in range(m): 
    a,b = map(int,input().split())
    graph[a].append(b) # adjacency list에 추가
    graph[b].append(a) # adjacency list에 추가



def recur(node): # Node 탐색 용
    state[node] = 1 # start node 방문처리
    for nxt in graph[node]: # 같은 Edge를 공유하는 Node 할당
        if state[nxt] ==1: # 방문처리 된 노드?
            continue # 연산 x
        recur(nxt) # 방문 안한 곳이면 재귀호출을 통해 탐색

recur(1) # start node가 1
print(state) # 방문된 노드 출력
```


### Result

