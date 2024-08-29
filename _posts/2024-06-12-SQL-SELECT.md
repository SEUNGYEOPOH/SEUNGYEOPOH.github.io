---
title:  "[PROGRAMMERS] SELECT"
categories : SQL
tag : SELECT
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

# 1. SELECT LV.1
## 1. 강원도에 위치한 생산공장 목록 출력하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131112)

<!-- ### 1.1 해설

- LIKE 구문
    - 컬럼 조회 시 Target Value가 조회하려는 조건과 부분적으로 일치하는 Case를 찾을 때 사용
    - % : 정해지지 않음
    - _ : 특정 위치를 지정

### 1.2 예시
```sql
LIKE "%강원도%" 
-- Value 중 강원도가 들어가 있다면 

LIKE "%강원도"
-- Value가 강원도로 끝난다면

LIKE "강원도%"
-- Value가 강원도로 시작한다면

LIKE '강원도_'
-- Value가 강원도로 시작하되, 4글자라면

``` -->


### 1.1 정답 

```sql
SELECT FACTORY_ID, FACTORY_NAME, ADDRESS FROM FOOD_FACTORY 
WHERE ADDRESS LIKE "%강원도%"
ORDER BY FACTORY_ID ASC
```



# 2. SELECT LV.2
## 1. 3월에 태어난 여성 회원 목록 출력하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131120)

### 1.1 정답
```sql
SELECT MEMBER_ID,MEMBER_NAME,GENDER,DATE_FORMAT(DATE_OF_BIRTH,"%Y-%m-%d") AS DATE_OF_BIRTH 
    FROM MEMBER_PROFILE 
    WHERE MONTH(DATE_OF_BIRTH) = "3" AND TLNO IS not NULL AND GENDER = "W"
    ORDER BY MEMBER_ID ASC
```

## 2. 재구매가 일어난 상품과 회원 리스트 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131536)

### 2.1 정답
```sql
SELECT USER_ID,PRODUCT_ID FROM ONLINE_SALE
    GROUP BY USER_ID, PRODUCT_ID HAVING COUNT(PRODUCT_ID) >1
    ORDER BY USER_ID, PRODUCT_ID DESC
```


## 3. 특정 물고기를 잡은 총 수 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/298518)

### 3.1 정답
```sql
SELECT COUNT(*) AS FISH_COUNT 
    FROM FISH_INFO AS A, FISH_NAME_INFO AS B
    WHERE (A.FISH_TYPE=B.FISH_TYPE) AND ((B.FISH_NAME = "BASS") OR (B.FISH_NAME = "SNAPPER"))
```

## 4. 업그레이드 된 아이템 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/273711)

### 4.1 정답
```sql

SELECT ITEM_ID, ITEM_NAME, RARITY 
    FROM ITEM_INFO 
    WHERE ITEM_ID IN (SELECT ITEM_ID FROM ITEM_TREE WHERE PARENT_ITEM_ID IN (SELECT ITEM_ID FROM ITEM_INFO WHERE RARITY="RARE"))
    ORDER BY ITEM_ID DESC
```

## 5. 조건에 맞는 개발자 찾기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/276034)

### 5.1 정답
```sql
SELECT B.ID, B.EMAIL, B.FIRST_NAME, B.LAST_NAME
    FROM 
        (SELECT SUM(CODE) CODE FROM SKILLCODES
        WHERE NAME = "Python" or NAME = "C#") AS A, DEVELOPERS AS B
    WHERE B.SKILL_CODE & A.CODE >0
    ORDER BY B.ID ASC
```

## 6. 부모의 형질을 모두 가지는 대장균 찾기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/301647)

### 6.1 정답
```sql
SELECT A.ID, A.GENOTYPE, B.GENOTYPE AS PARENT_GENOTYPE 
    FROM ECOLI_DATA AS A, ECOLI_DATA AS B
    WHERE A.PARENT_ID = B.ID AND (B.GENOTYPE & A.GENOTYPE) = B.GENOTYPE
    ORDER BY A.ID ASC
```

* * *

# 3. SELECT LV.3
## 1. 대장균들의 자식 수 구하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/299305)

### 1.1 정답
```sql
SELECT B.ID, IF (A.COUNT IS NULL, 0, A.COUNT) AS CHILD_COUNT
    FROM
        (SELECT IF (PARENT_ID IS NULL, 0, PARENT_ID) AS PARENT_ID, COUNT(PARENT_ID) AS COUNT FROM ECOLI_DATA 
        GROUP BY PARENT_ID) AS A 

RIGHT OUTER JOIN ECOLI_DATA AS B

ON A.PARENT_ID = B.ID
```

## 2. 대장균의 크기에 따라 분류하기 1
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/299307)

### 2.1 정답
```sql
SELECT ID, 
    CASE WHEN SIZE_OF_COLONY<=100 THEN "LOW"
    WHEN SIZE_OF_COLONY<=1000 THEN "MEDIUM"
    ELSE "HIGH"
    END AS SIZE 
    FROM ECOLI_DATA 
    ORDER BY ID ASC
```

## 3. 대장균의 크기에 따라 분류하기 2
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/301649)

### 3.1 정답
```sql
SELECT A.ID,
    CASE WHEN A.PERCENT<=0.25 THEN "CRITICAL"
    WHEN A.PERCENT<=0.5 THEN "HIGH"
    WHEN A.PERCENT<=0.75 THEN "MEDIUM"
    ELSE "LOW"
END AS COLONY_NAME
    FROM
        (SELECT ID, SIZE_OF_COLONY, 
            PERCENT_RANK() OVER(ORDER BY SIZE_OF_COLONY DESC) AS PERCENT 
            FROM ECOLI_DATA) AS A 
    ORDER BY ID ASC
```

* * *

# 4. SELECT LV.4
## 1. 서울에 위치한 식당 목록 출력하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131112)

### 1.1 정답
```sql
SELECT 
    B.REST_ID, B.REST_NAME, B.FOOD_TYPE, B.FAVORITES, B.ADDRESS, A.SCORE 
    FROM 
    (SELECT REST_ID, ROUND(AVG(REVIEW_SCORE),2) AS SCORE FROM REST_REVIEW
    GROUP BY REST_ID) AS A, REST_INFO AS B

    WHERE (A.REST_ID = B.REST_ID) AND B.ADDRESS LIKE "서울%"

    ORDER BY A.SCORE DESC, B.FAVORITES DESC
```


## 2. 오프라인/온라인 판매 데이터 통합하기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131537)
### 2.1 정답
```sql
SELECT 
    DATE_FORMAT(SALES_DATE,"%Y-%m-%d") AS SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT 
    FROM ONLINE_SALE 
    WHERE SALES_DATE LIKE "2022-03%"

UNION ALL

SELECT 
    DATE_FORMAT(SALES_DATE,"%Y-%m-%d") AS SALES_DATE, PRODUCT_ID, NULL, SALES_AMOUNT 
    FROM OFFLINE_SALE 
    WHERE SALES_DATE LIKE "2022-03%"

    ORDER BY SALES_DATE ASC, PRODUCT_ID, USER_ID
```


## 3. 특정 세대의 대장균 찾기
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/301650)

### 3.1 정답
```sql
SELECT ID 
    FROM ECOLI_DATA
    WHERE PARENT_ID IN (SELECT ID FROM ECOLI_DATA WHERE PARENT_ID IN (SELECT ID FROM ECOLI_DATA WHERE PARENT_ID IS NULL))
    ORDER BY ID ASC
```