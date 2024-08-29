---
title:  "[PROGRAMMERS] SUM, MAX, MIN"
categories : SQL
tag : [SUM, MAX, MIN]
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
<u>DBMS : MySQL</u>
{: .notice--success}

# 1. SUM, MAX, MIN LV.1
## 1. 가장 비싼 상품 구하기

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131697)

### 1.1 정답
```sql
SELECT MAX(PRICE) AS MAX_PRICE FROM PRODUCT
```

## 2. 잡은 물고기 중 가장 큰 물고기의 길이 구하기

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/298515)

### 2.1 정답
```sql
SELECT 
    CONCAT(LENGTH, "cm") AS MAX_LENGTH
FROM 
    FISH_INFO
ORDER BY 
    LENGTH DESC
LIMIT 1;

```

## 3. 최댓값 구하기

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/59415)

### 3.1 정답
```sql
SELECT 
    DATETIME AS "시간" 
FROM 
    ANIMAL_INS 
ORDER BY 
    DATETIME DESC
limit 1
```


# 2. SUM, MAX, MIN LV.2
## 1. 연도별 대장균 크기의 편차 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/299310)

### 1.1 정답
```sql
SELECT 
    A.YEAR, 
    (B.MAX_SIZE - A.SIZE_OF_COLONY) AS YEAR_DEV, 
    A.ID 
FROM 
    (SELECT 
        YEAR(DIFFERENTIATION_DATE) AS YEAR, 
        SIZE_OF_COLONY, 
        ID 
    FROM 
        ECOLI_DATA) AS A
JOIN 
    (SELECT
        YEAR(DIFFERENTIATION_DATE) AS YEAR,
        MAX(SIZE_OF_COLONY) AS MAX_SIZE
    FROM
        ECOLI_DATA
    GROUP BY
        YEAR) AS B
ON 
    A.YEAR = B.YEAR
ORDER BY 
    YEAR ASC, 
    YEAR_DEV ASC;
```

## 2. 조건에 맞는 아이템들의 가격의 총합 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/273709)

### 2.1 정답
```sql
SELECT 
    SUM(PRICE) as TOTAL_PRICE 
FROM 
    ITEM_INFO 
WHERE 
    RARITY = "LEGEND"
```

## 3. 가격이 제일 비싼 식품의 정보 출력하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131115)

### 3.1 정답
```sql
SELECT PR
    ODUCT_ID,PRODUCT_NAME,PRODUCT_CD,CATEGORY,PRICE 
FROM 
    FOOD_PRODUCT
WHERE 
    PRICE = (SELECT MAX(PRICE) FROM FOOD_PRODUCT)
```

## 4. 중복 제거하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/59408)

### 4.1 정답
```sql
SELECT 
    COUNT(DISTINCT NAME) as "count" 
FROM 
    ANIMAL_INS
```


## 5. 동물 수 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/59406)

### 5.1 정답
```sql
SELECT 
    count(*) as "count" 
FROM 
    ANIMAL_INS
```


## 6. 최솟값 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/59038)

### 6.1 정답
```sql
SELECT 
    MIN(DATETIME) AS "시간" 
FROM 
    ANIMAL_INS

OR 

SELECT 
    DATETIME AS "시간" 
FROM 
    ANIMAL_INS 
ORDER BY 
    DATETIME ASC
limit 1
```

# 3. SUM, MAX, MIN LV.3
## 1. 물고기 종류 별 대어 찾기

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/293261)

### 1.1 정답
```sql
SELECT 
    A.ID, 
    B.FISH_NAME, 
    A.MAX_LENGTH AS LENGTH 
FROM 
    (
        SELECT 
            B.ID, 
            A.FISH_TYPE, 
            A.MAX_LENGTH
        FROM 
            (
                SELECT 
                    FISH_TYPE,
                    MAX(LENGTH) AS MAX_LENGTH 
                FROM 
                    FISH_INFO 
                GROUP BY 
                    FISH_TYPE
            ) AS A, 
            FISH_INFO AS B
        WHERE 
            B.FISH_TYPE = A.FISH_TYPE 
            AND B.LENGTH = A.MAX_LENGTH
    ) AS A, 
    FISH_NAME_INFO AS B
WHERE 
    A.FISH_TYPE = B.FISH_TYPE
ORDER BY 
    A.ID ASC;
```