---
title:  "[PROGRAMMERS] IS NULL"
categories : SQL
tag : IS NULL
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

# 1. IS NULL LV.1
## 1. 경기도에 위치한 식품창고 목록 출력하기


[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131114)

### 1.1 정답
```sql
SELECT WAREHOUSE_ID,WAREHOUSE_NAME, ADDRESS, IF(FREEZER_YN IS NULL, "N", FREEZER_YN) AS FREEZER_YN 
    FROM FOOD_WAREHOUSE 
    WHERE ADDRESS LIKE "%경기도%"
    ORDER BY WAREHOUSE_ID ASC
```

## 2. 이름이 없는 동물의 아이디



[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/59039)

### 2.1 정답
```sql
SELECT ANIMAL_ID 
    FROM ANIMAL_INS
    WHERE NAME IS NULL
    ORDER BY ANIMAL_ID
```

## 3. 이름이 있는 동물의 아이디



[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/59407)

### 3.1 정답
```sql
SELECT ANIMAL_ID 
    FROM ANIMAL_INS
    WHERE NAME IS NOT NULL
    ORDER BY ANIMAL_ID
```

## 4. 나이 정보가 없는 회원 수 구하기



[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/131528)

### 4.1 정답
```sql
SELECT COUNT(*) AS USERS 
    FROM USER_INFO 
    WHERE AGE IS NULL
```


## 5. 잡은 물고기의 평균 길이 구하기



[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/293259)

### 5.1 정답
```sql
SELECT ROUND(AVG(IF(LENGTH IS NULL, 10,LENGTH)),2) AS AVERAGE_LENGTH 
    FROM FISH_INFO
```

* * *

# 2. IS NULL LV.2
## 1. NULL 처리하기

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/59410)

### 1.1 정답
```sql
SELECT 
    ANIMAL_TYPE,
    IF(NAME IS NULL,"No name",NAME) AS NAME,
    SEX_UPON_INTAKE 
    FROM ANIMAL_INS
```

## 2. ROOT 아이템 구하기

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/273710)

### 2.1 정답
```sql
SELECT A.ITEM_ID, B.ITEM_NAME
    FROM
        (SELECT ITEM_ID FROM ITEM_TREE 
            WHERE PARENT_ITEM_ID IS NULL) AS A, ITEM_INFO AS B
    WHERE A.ITEM_ID = B.ITEM_ID
    ORDER BY A.ITEM_ID ASC
```




* * *

# 3. IS NULL LV.3

## 1. 업그레이드 할 수 없는 아이템 구하기

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/273712)

### 1.1 정답
```sql
SELECT ITEM_ID, ITEM_NAME, RARITY 
    FROM  ITEM_INFO
    WHERE 
        (ITEM_ID NOT IN 
            (SELECT PARENT_ITEM_ID FROM ITEM_TREE 
                WHERE (PARENT_ITEM_ID IS not NULL)
            )) 
    ORDER BY ITEM_ID DESC
```