---
title:  "[Lightweight-Sereis] 2. Quantization"
categories : [Lightweight, Optimization, Quantization]
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


## 1. Weight Tensor
<p align="center">
  <img src="https://github.com/user-attachments/assets/33021fd7-0831-48fc-a479-8180e226403e" width=900 height=500 alt="Example Image">
</p>
- Pytorch, Tensorflow의 Tesnor의 dtype은 float32
- 여기서 32라는 의미는 해당 Type의 Value를 저장하기 위해 32bit(4bytes)를 사용한다는 의미.



| 형식    | 부호 비트 | 지수 비트 | 가수 비트 | 메모리 크기 | 표현 가능한 정밀도      | Bias |
|---------|-----------|-----------|-----------|-------------|------------------------|------------------------|
| float32 | 1         | 8         | 23        | 4 bytes     | 소수점 이하 약 7자리   | 127 |
| float16 | 1         | 5         | 10        | 2 bytes     | 소수점 이하 약 3-4자리 | 15 |

- 부호(Sign)
  - 0 : 양수
  - 1 : 음수

- 지수(Exponent)
  - 8bit로 표현된 지수 부분
  - 3.14XX의 3을 지수로 표현한다면?(float32)
    - 3 -> 11(2) -> Normalization -> 1 -> 1+127(bias) -> 128 -> 1000000

- 가수(Mantissa)
  - 정규화 된 소수 부분


## 2. Computation time(int vs float)

 ```python
import numpy as np
import time

a = np.random.randn(10**6).astype(np.float32)
b = np.random.randn(10**6).astype(np.float32)

a_it = a.astype(np.int8)
b_it = b.astype(np.int8)

def measure_multiplication_time(a,b):
    start_time = time.time()
    result = a-b
    end_time = time.time()
    return end_time - start_time

arr_1=[]
arr_2=[]

for i in range(100):
    f_32=measure_multiplication_time(a,b)
    i_8 = measure_multiplication_time(a_it,b_it)
    arr_1.append(f_32)
    arr_2.append(i_8)
    
print(f"float32 연산 시간: {sum(arr_1)/len(arr_1):.6f} 초")
# 0.001500

print(f"int8 연산 시간: {sum(arr_2)/len(arr_2):.6f} 초")
# 0.000447
``` 

- CPU 기준 integer 연산이 3.36배 빠름
- 4Bytes인 Float32에 비해 Int8의 경우 1Byte를 사용하므로, 더 적은 크기로 빠르게 연산을 수행할 수 있음.(4배)
- 이처럼, dtype 혹은 bit를 줄여, Model의 크기와 Learning Cost를 줄이는 시도가 진행되고 있음.

>※ 단, 편차가 존재할 수 있으며, Numpy의 dot 연산의 경우 오히려 Float32가 더 빠름.
>>즉, Target H/W 그리고 연산에 따라, 가속을 위한 dtype은 상이할 수 있음을 주의.


## 3. Quantization(To-Be Updated)
