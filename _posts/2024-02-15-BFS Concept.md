---
title:  "BFS Concept"
categories : Algorithm
tag : BFS
# 복수로 하려면 [Python, Blog]처럼 리스트 형태로 할당
toc : true
# toc순서는 markdown header(#) 기준 입니당
toc_sticky : true
toc_label : Content
toc_icon : "fas fa-book-open"
author_profile : false
use_math : true
---

# Breadth First Search

## 1. What is Breadth-First Search?
- Graph Search
    - Start Node와 Graph가 주어졌을 때 Edge를 통해 방문할 수 있는 Node를 찾는 문제
    - BFS와 DFS가 존재한다.
- BFS(FIFO 사용)
    - Start Node에서 인접 노드 기준으로 탐색
    - 즉 Tree를 수평으로 우선 탐색
    - 최단거리(경로) 해결에 효과적


<p align="center"><img src = "https://upload.wikimedia.org/wikipedia/commons/5/5d/Breadth-First-Search-Algorithm.gif?20100504223639" width = "50%" height = "50%" ></p>

## 2. How to Use?
- Queue(FIFO)를 활용하여 구현
- 1차원 혹은 2차원 Board에서 이동 가능한 좌표로 이동
- 직전 좌표에서 이동한 거리만큼 노드의 값을 가중시키며 목적지까지의 거리 탐색

## 3. Base Code
### BFS
```python
from collections import deque

def bfs(node): 
    a=deque([node]) # 초기 노드를 큐에 push
    state[node] = 1 # 방문 처리
    while len(a): # 큐가 빌때까지
        node = a.popleft() # 큐에서 처음 들어온 노드 제거
        ans_2.append(node) # 제거 후 출력 순서를 보여주기 위해 ans에 방문된 node 추가
        for nxt in graph[node]: # 관련된 다른 node
            if state[nxt]==0: # 방문하지 않은 노드일 경우
                a.append(nxt) # 큐에 추가하고
                state[nxt]=1 # 방문 처리

n,m = map(int, input().split()) # n은 노드 개수, m은 간선
graph =[[] for i in range(n+1)] #
ans_2=[]
for i in range(m):
    a,b=map(int,input().split())
    graph[a].append(b)
    graph[b].append(a)

state = [0 for i in range(n+1)] 
bfs(1) # 탐색
print(*ans_2) # 결과 출력

```

