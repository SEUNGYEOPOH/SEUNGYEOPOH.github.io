---
title:  "[Attention-Series] 1. Self-Attention"
categories : [NLP,Attention]
published: true
tag : [Self-Attention]
# 복수로 하려면 [Python, Blog]처럼 리스트 형태로 할당
toc : true
# toc순서는 markdown header(#) 기준 입니당
toc_sticky : true
toc_label : Content
toc_icon : "fas fa-book-open"
author_profile : false
use_math : true
---


# Self - Attention
<p align="center">
  <img src="https://github.com/user-attachments/assets/304337e4-5b81-4b54-a1f5-81719bd20366" alt="Example Image">
</p>
- 자연어를 처리하기 위해선 문맥을 이해하는 것이 필수적.
- 사람은 문법을 학습하고 노출되어 왔기에, 특정 문장에서 단어 간의 관계를 이해 가능.
> Ex. The paper was rejected because it was poorly written
>> it -> The Paper / 컴퓨터는 어떻게 이해하지??
- Self Attention은 이러한 단어 간 관계에 대한 정보를 정량화된 수치로 표현하기 위한 Technique


## 1. Query, Key, Value
- Self - Attnetion을 이해하기 위해선 Query, Key, Value에 대한 이해가 선행되어야 함.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f54c7672-b5fe-4f89-b549-7960e2566222" width=500 height=500 alt="Example Image">
</p>

- 볼펜은 색상에 따라 용도가 다름.
- Query, Key, Value 역시, 본질은 입력 문장에 Embedding Vector지만 각각 사용하는 용도 상이.

> Query : 탐색의 대상

> Key : Query와 내적을 통해, Attention Score를 산출

> Value : Query와 Key의 내적으로 표현된 Attention Weight와의 내적을 통해 최종적인 Output을 산출

## 2. Calculation
\\[
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{Q K^T}{\sqrt{d_k}}\right) V
\\]

## 2.1 Inner Product
\\[
  \frac{Q K^T}{\sqrt{d_k}} 
\\]

- 내적의 성질
    - 유사 방향의 Vector는 내적 값이 太
- 즉, 유사한 관계를 가진 단어일수록 내적 값은 증가
- 이렇게 산출된 단어 간 관계를 나타내는 Vector는 Embedding Vector가 가지는 Dimension의 제곱근으로 Scaling 
    - 내적 후의 크기를 Scaling함으로서 수치 안정성 확보

> Input = Slow But Steady Wins the race, Embedding Dim = 36
>> Embedding Vector's Shape : (6,36) -> $\sqrt 36$인 6으로 Scaling

```python
def Innerproduct(query, key):
    mat = np.dot(query, key.T) 
    mat = mat/(key.shape[1]**(1/2))
    return mat
``` 

- Key의 TransPose 의미?
    - Ex. Input = Slow But Steady Wins the race, Embedding Dim = 5
        - 위의 경우 Query, Key의 Shape은 (6,5)
        - 행렬 연산을 위해선 5,6으로 변경할 필요 有
    - Vector의 관점
        - 각 단어 별 Embedding에 대응되는 Attention weight 산출

<p align="center">
  <img src="https://github.com/user-attachments/assets/2537c060-b398-4683-b573-1873105fc8ab" width=1000 height=1000 alt="Example Image">
</p>

## 2.2 softmax
\\[
  \text{Softmax}(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}
\\]
- softmax를 통해 0~1사이의 값으로 각 Embedding Vector를 표현가능
- 지수함수의 특성 상 큰 값은 크게 변화
- 즉, 확률 형태로 표현하며, 중요한 관계일수록 더 높은 가중치를 가짐

```python
 def softmax(a) : 
    c = np.max(a) 
    exp_a = np.exp(a-c) # 각 Vector에서 최댓값을 빼, Overflow를 방지
    sum_exp_a = np.sum(exp_a)
    y = exp_a / sum_exp_a
    return y
``` 

## 2.4 Attention Score
\\[
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{Q K^T}{\sqrt{d_k}}\right) V
\\]

- 위의 과정을 거쳐 0~1로 표현된 Attention Weight와 Value의 내적을 통해 Output 산출
> Ex. Attention Weight's Shape = (6,6), Value's Shape = (6,5)
>> Output = 6,5
- 즉, 원본 Embedding vector에 각각 대응되는 0~1로 표현된 관계 정보를 mapping하여 각 Vector의 중요도를 반영한 Representation vector를 산출  

<p align="center">
  <img src="https://github.com/user-attachments/assets/3f6b4f1f-c317-4247-9861-ef92b3c166bc" width=1000 height=1000 alt="Example Image">
</p>

```python
 def attention(r_mat, value):
    return np.dot(r_mat,value)
``` 

## 3. Code Version

## 3.1 Set-up
- Example sentence : slow but steady wins the race 
- Self-Attention 상 Mask (opt.)의 경우 문장 생성에서 사용하므로 해당 예제에선 배제하고 진행
- 본격적으로 진행 전 예제 문장에 대한 Embedding을 수행
    - 편의 상 Embedding Layer를 사용해 Vector Representation
    - Embedding Dimension은 10으로 설정
    - Embedding Output의 Shape : (Vocasize, Embedding Dimension)
      
 ```python
import numpy as np
from tensorflow.keras.layers import Embedding

sentence = "slow but steady wins the race"
words = sentence.split()


word_to_index = {word: idx for idx, word in enumerate(words)}
input_indices = [word_to_index[word] for word in words]

vocab_size = len(word_to_index)  
embedding_dim = 10

embedding_layer = Embedding(input_dim=vocab_size, output_dim=embedding_dim)

input_indices = np.array(input_indices)  
embeddings = embedding_layer(input_indices).numpy()
print("Word Embeddings:\n", embeddings)
``` 

## 3.2 Self - Attention Code
 ```python
class SelfAttention:
    def __init__(self):
        pass

    def inner_product(self, query, key):
        mat = np.dot(query, key.T)
        mat = mat / (key.shape[1] ** (1 / 2))
        return mat

    def softmax(self, a):
        c = np.max(a, axis=-1, keepdims=True)  # Stabilize computation by subtracting max
        exp_a = np.exp(a - c)
        sum_exp_a = np.sum(exp_a, axis=-1, keepdims=True)
        y = exp_a / sum_exp_a
        return y

    def self_attention(self, r_mat, value):
        return np.dot(r_mat, value)

    def compute_attention(self, query, key, value):
        r_mat = self.inner_product(query, key)
        attention_weights = self.softmax(r_mat)
        attention_output = self.self_attention(attention_weights, value)

        return attention_output, attention_weights


if __name__ == "__main__":
    attention = SelfAttention()
    
    query, key, value = embeddings,embeddings,embeddings
    
    output, weights = attention.compute_attention(query, key, value)

    print("Attention Weights:\n", weights)
    print("Attention Output:\n", output)
``` 