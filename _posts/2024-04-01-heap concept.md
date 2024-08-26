---
title:  "Heap Concept"
categories : DataStructure
tag : Heap
# 복수로 하려면 [Python, Blog]처럼 리스트 형태로 할당
toc : true
# toc순서는 markdown header(#) 기준 입니당
toc_sticky : true
toc_label : Content
toc_icon : "fas fa-book-open"
author_profile : false
use_math : true
---

# HEAP Concept

## 1. What is Heap?
<!-- - Abstract Data Type : Priority Queue(FIFO) 보고오기 -->

![heap_image](https://github.com/SEUNGYEOPOH/SEUNGYEOPOH/assets/81912557/adf1014c-20f5-4b8e-a452-4d5f45410198)

- heap의 특징
    - Binary Tree
    - heap에서는 항상 root node 제거
    - 종류
        - min heap
            - root node = min_value
            - 작은 데이터가 우선 제거
        - max heap
            - root node = max_value
            - 큰 데이터가 우선 제거
    - Heapify
        - heap을 구성하기 위한 함수
        - 종류
            - Min-Heapify(상향식)
                - terminal -> root까지 탐색 후 자신의 값이 부모보다 더 적은 경우 위치 교체
                - heapq 모듈의 default는 Min-Heapfify
            - Max-Heapify(하향식)
                - terminal -> root까지 탐색 후 자신의 값이 부모보다 더 클 경우 위치 교체

## 2. How to Use?
- heapq module or PriorityQueue(PQ) Module 사용

- PQ는 BOJ기준 Runtime Error로 인해 heapq 활용 구현

- heapq module
    - function
        - heapify(list)
            - default는 Min
            - list를 heap 형태로
        - heappush(list,value)
            - terminal node에 value 추가
            - root로 올라가며 자신의 값이 부모보다 더 적은 경우 위치 교체 
        - heappop(list)
            - root node 제거

## 3. Base code
### Heapq
```python
import heapq

## min heap 구현

heap = [] # 선언
heapq.heappush(heap, 3) # min heapify에 따라 value insert
heapq.heappush(heap, 2)
heapq.heappush(heap, 1)

print(heap)


## max heap 구현

items = [1,3,2,5] 
max_heap = []

for x in items:
  heapq.heappush(max_heap, (-x, x)) # 음수를 통해 min heapify를 max heapify로

print(max_heap)
mval = heapq.heappop(max_heap)[1] # 출력
print(mval)
```


