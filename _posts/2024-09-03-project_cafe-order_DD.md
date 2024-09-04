---
title: "[소프트웨어공학] DD(Data Dictionary) 작성"
date: 2024-09-03 02:01:00 +09:00
categories: [프로젝트, 카페오더]
tags:
  [
    프로젝트 회고,
    소프트웨어공학,
    Cafe Order
  ]
use_math: true
---

## Data Dictionary
데이터베이스를 작성할 때 엔티티명이나 속성명 등을 짓게된다.<br>
하지만 엔티티명이나 속성명 그외 이름들을 아무리 잘 짓는다고 해도 몇몇 단어들은 사람마다 해석이 다를 수 있다.<br>
그리고 ERD 를 보고 개발을 할 때 사람마다 변수명을 다르게 작성할 수 있게된다.<br>
<br>
예를 들어, <br>

![사진1](https://github.com/Hoon1999/hoon1999.github.io/blob/main/assets/img/2024-09-01/project_cafe_order/4.png?raw=true)<br>

위 ERD 를 보자.<br>
주문 Entity 의 주문상태 속성을 봤을 때 이게 무슨 값을 보관하는 속성인지 알기 어렵다.<br>
그리고 변수명으로 작성할 때 A 라는 사람은 orderState 라고 작성하고, B 라는 사람은 state 라고만 작성할 수도 있다.<br>
위 두 상황을 방지하기 위해 Data Dictionary 작성이 필요하다.<br>
<br>

## 작성 순서
### 1. 속성 작성
모든 속성을 작성해준다.<br>

| Entity명 | 속성명    |
| ------- | ------ |
| 회원      | 회원id   |
|         | 전화번호   |
|         | 포인트    |
| 주문      | 주문id   |
|         | 총결제금액  |
|         | 주문상태   |
|         | 결제시간   |
| 주문상세    | 주문상세id |
|         | 상품id   |
|         | 가격     |
|         | 수량     |
| 추가옵션    | 주문상세id |
|         | 상품id   |
|         | 옵션id   |
|         | 옵션수량   |
| 상품      | 상품id   |
|         | 상품명    |
|         | 가격     |
|         | 재고     |
|         | 품절여부   |
| 옵션      | 옵션id   |
|         | 옵션명    |
|         | 재고수량   |
|         | 품절여부   |
|         | 옵션유형id |
| 옵션유형    | 옵션유형id |
|         | 옵션유형명  |
|         | 표기순서   |

### 2. 속성명 분리

| Entity명 | 속성명    | 단어1 | 단어2 | 단어3 |
| ------- | ------ | --- | --- | --- |
| 회원      | 회원id   |     | 회원  | id  |
|         | 전화번호   |     | 전화  | 번호  |
|         | 포인트    |     |     | 포인트 |
| 주문      | 주문id   |     | 주문  | id  |
|         | 총결제금액  | 총   | 결제  | 금액  |
|         | 주문상태   |     | 주문  | 상태  |
|         | 결제시간   |     | 결제  | 시간  |
| 주문상세    | 주문상세id | 주문  | 상세  | id  |
|         | 상품id   |     | 상품  | id  |
|         | 가격     |     |     | 가격  |
|         | 수량     |     |     | 수량  |
| 추가옵션    | 주문상세id | 주문  | 상세  | id  |
|         | 상품id   |     | 상품  | id  |
|         | 옵션id   |     | 옵션  | id  |
|         | 옵션수량   |     | 옵션  | 수량  |
| 상품      | 상품id   |     | 상품  | id  |
|         | 상품명    |     | 상품  | 명   |
|         | 가격     |     |     | 가격  |
|         | 재고     |     |     | 재고  |
|         | 품절여부   |     | 품절  | 여부  |
| 옵션      | 옵션id   |     | 옵션  | id  |
|         | 옵션명    |     | 옵션  | 명   |
|         | 재고수량   |     | 재고  | 수량  |
|         | 품절여부   |     | 품절  | 여부  |
|         | 옵션유형id | 옵션  | 유형  | id  |
| 옵션유형    | 옵션유형id | 옵션  | 유형  | id  |
|         | 옵션유형명  | 옵션  | 유형  | 명   |
|         | 표기순서   |     | 표기  | 순서  |

### 3. 단어 설명 작성
Entity명, 속성명 을 제외하고 단어만 골라 설명을 작성한다.

| 논리명 | 물리명          | 약어   | 설명      |
| --- | ------------ | ---- | ------- |
| id  |              |      |         |
| 회원  | member       |      |         |
| 전화  | telephone    | tel  | 회원 전화번호 |
| 번호  | number       | no   |         |
| 주문  | order        |      |         |
| 포인트 | point        |      |         |
| 총   | total        | tot  |         |
| 결제  | payment      | pay  |         |
| 금액  | amount       |      |         |
| 상태  | state        |      |         |
| 시간  | time         |      |         |
| 상세  | detail       |      |         |
| 상품  | product      | prod |         |
| 가격  | price        |      |         |
| 옵션  | option       | opt  |         |
| 수량  | amount       |      |         |
| 재고  | stock        |      |         |
| 품절  | out_of_stock | oos  |         |
| 유형  | type         |      |         |
| 표기  | marking      | mark |         |
| 순서  | order        |      |         |

## 도메인 정의서
속성들을 정의해 놓은 문서. 속성을 논리명에 작성하고, 위에 작성한 DD 를 참고해 물리명을 작성한다.

| Entity명 | 논리명    | 물리명               | 데이터타입     | 설명                                                     |
| ------- | ------ | ----------------- | --------- | ------------------------------------------------------ |
| 회원      | 회원id   | member_id         | integer   | 회원번호                                                   |
|         | 전화번호   | tel_no            | varchar() | 회원 전화번호                                                |
|         | 포인트    | point             | integer   | 회원 적립금                                                 |
| 주문      | 주문id   | order_id          | integer   | 주문번호                                                   |
|         | 총결제금액  | tot_pay_amount    | integer   | 최종결제 금액                                                |
|         | 주문상태   | order_state       | integer   | 주문 상태를 의미한다.(주문접수, 조리중, 주문취소, 주문완료)                    |
|         | 결제시간   | pay_time          | datetime  | 결제가 승인된 시각                                             |
| 주문상세    | 주문상세id | order_detail_time | integer   | 주문상세번호. 주문상세는 옵션이 적용된 상품이다.                            |
|         | 가격     | price             | integer   | 옵션이 적용된 상품의 가격                                         |
|         | 수량     | amount            | integer   | 옵션이 적용된 상품의 수량                                         |
| 추가옵션    | 옵션수량   | opt_aomunt        | integer   | 상품에 추가한 옵션의 수량                                         |
| 상품      | 상품id   | prod_id           | integer   | 상품번호                                                   |
|         | 상품명    | prod_name         | varchar() | 상품 이름                                                  |
|         | 가격     | price             | integer   | 상품 가격                                                  |
|         | 재고     | stock             | integer   | 상품 재고                                                  |
|         | 품절여부   | sso               | integer   | 상품의 품절여부                                               |
| 옵션      | 옵션id   | opt_id            | integer   | 옵션 번호                                                  |
|         | 옵션명    | opt_name          | varchar() | 옵션 이름                                                  |
|         | 재고수량   | stock             | integer   | 옵션 재고                                                  |
|         | 품절여부   | sso               | integer   | 옵션 품절여부                                                |
| 옵션유형    | 옵션유형id | opt_type_id       | integer   | 옵션 유형 번호                                               |
|         | 옵션유형명  | opt_type_name     | varchar() | 옵션 유형 이름(옵션 카테고리 이름). 얼음 적게/중간/많음 은 얼음 카테고리에 속해 있어야 함. |
|         | 표기순서   | mark_order        | integer   | 카테고리의 표기순서.                                            |

**References** <br>
[도메인과 용어사전의 정의](https://blog.naver.com/kimbh666/221391961062) <br>