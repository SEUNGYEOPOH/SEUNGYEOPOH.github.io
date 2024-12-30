---
title:  "[Lightweight-Sereis] 0. Intro"
categories : [Lightweight, Optimization]
published: true
tag : [Lightweight]
# 복수로 하려면 [Python, Blog]처럼 리스트 형태로 할당
toc : true
# toc순서는 markdown header(#) 기준 입니당
toc_sticky : true
toc_label : Content
toc_icon : "fas fa-book-open"
author_profile : false
use_math : true
---


## 1. Lightweight Deep Learning
<p align="center">
  <img src="https://github.com/user-attachments/assets/6bf6e4ba-a8c6-4aea-bb66-e23b13f4eda9" width=700 height=700 alt="Example Image">
</p>

- Computer Vision, LLM 등의 분야는 높은 성능을 보여주나, 한계점을 지니고 있음.
  - 막대한 연산 자원
    - Paramerts가 수입억 ~ 수천억 -> Train & Inference를 위한 Computational Cost가 매우 多.
  - 모바일 및 Edge Device에서의 제약
    - IoT 환경 혹은 모바일 Device에서 실행이 어려움.
  - 실시간 처리의 한계
    - 자율주행, 실시간 번역 등 응답속도가 중요한 실시간 처리의 경우 Latency가 느리다면 실용성이 떨어짐.
- 해당 분야가 아니더라도, 가지고 있는 H/W의 사양에 따라 탑재할 수 있는 모델은 제한적.

어떻게 해결할 수 있을까?

## 2. Lightweight Method

- 이를 해결하기 위한 Neural Network의 Cost & Size를 줄이는 방법
- 종류
  1. Pruning
    - Connect 된 Network를 잘라 Computational Cost를 줄이는 방식
  2. Quantization
    - floating-point의 Weight를 integer로 변환하여 Cost와 Memory를 줄이는 방식
  3. Knowledge Distillation
    - Teacher Network(Pre-Traiend)의 지식을 Student Network의 전달하며 Train 시키는 Method.
    - 즉, 더 큰 Network와 Smaller Network의 Loss의 차이를 학습시켜 Smaller Network의 성능을 향상시키는 학습 방법. 
  4. Low-Rank Adaptation
    - M X N 크기의 Weight Matrix를 M X K, K X N의 저차원 행렬로 분해하여 학습시킨 후, 복원하는 방식.
  5. Framework
    - onnx, TensorRT 등 가속 Framework를 활용 

이번 Sereis는 이러한 Lightweight Deep Learning 기법들을 분석하고 적용해보는 과정.