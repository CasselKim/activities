# Ⅰ. What is Control?


# Contents

1. History of Control
2. What is Control Engineering?
3. Open and Closed-loop System
4. Control System Terminology

## 1. 제어의 역사

[1788] 제어의 기원, 원심 조속기(Centrifugal Governor) 1788

: 연료의 양(작동 유체)를 조절함으로써 엔진의 속도를 제어하는 피드백 시스템

[https://www.youtube.com/watch?time_continue=149&v=HS_YGZXP2xY&feature=emb_title](https://www.youtube.com/watch?time_continue=149&v=HS_YGZXP2xY&feature=emb_title)

[1850-1900] 미분(선형) 방정식을 이용한 제어의 수학적 접근(Maxwell & vyshnegradskii)

[1900-1950] 서강(수학적)과 소련(기계적)에 의해 **제어이론**이 탄생. 

[1940년대] 자동제어가 표준이 됨

[1950~70년대] 전자컴퓨터가 발명, 우주 개발 시대, 마이크로프로세서

[오늘날] 설비, 생산시설, 차량, 소비자 전자기기, 에너지 생산 제어 + 로봇, 의료

## 2. 제어공학(Control Engineering)이란?

**제어(Control) :** 시스템(비행기, 차 등)을 그 의도에 맞게 바꾸는(Change) 행동(Action)

**제어공학 :** 제어 이론을 시스템에 적용시켜 의도한 행동을 하도록 하는 규율(displine)

제어공학은 다음의 물리적 계층 or 과정을 거친다

- Performance Specifications(성능 명세) : 시스템이 원하는 모든 요구 조건을 만듦
- Modelling(모델링) : 물리적 시스템의 행위를 설명하는 미분 방정식을 세우거나 풂
- Analysis(분석) : 원래 시스템의 성능을 분석함
- Control(제어) : 성능이 성능 명세(Performance Specifications)를 충족하지 않는 경우, 설계 및 응답을 개선하기 위해 제어요소를 추가함

**피드백(Feedback)** : 행위의 결과와 그에 따라 행위를 재조정하는 등의 상관관계

![%E2%85%A0%20What%20is%20Control%20a8b30e5794de4830a80cd7905e8ed458/Untitled.png](%E2%85%A0%20What%20is%20Control%20a8b30e5794de4830a80cd7905e8ed458/Untitled.png)

**No Sensor(information) → No Feedback!**

### 성능명세(Performance Specifications)

예시) 엘리베이터

- 목적지에 가능한 빨리 도착해야함
- 탑승자가 다치지 않도록 부드럽게 동작해야함
- 1층→5층→4층 이 아니라 1층→4층으로 바로 가야함
- 승객이 1명이든 5명이든 같은 속도로 움직여야함
- 정확한 높이에서 멈춰야함(너무 높이가면 천장을 뚫고 너무 낮게가면 바닥에 떨어짐)

이와 같은 **모든 요구조건들**을 성능 명세(Performance specifications)라고함

## 3. Open and Closed-loop System

### Open-loop System

- 제어과정에서 출력이 입력에 영향을 미치지 않는 시스템 (선풍기 등)
- 정한 속도만큼 정확히 회전하기 위해 Calibration이라는 보정 능력이 요구
- **시스템이 처음부터 안정해야 함**

### Closed-loop System

- 출력 정보를 피드백 받아서 입력에 영향을 주는 시스템 (에어컨 등)
- 나는 26도를 원하는데 현재 온도가 27도일 때 에어컨이 조금 더 가동할 것임
- 루프를 닫는다 : 자동제어의 영향을 받도록 함 == **시스템의 입출력 동작을 변형할 수 있음**

![%E2%85%A0%20What%20is%20Control%20a8b30e5794de4830a80cd7905e8ed458/Untitled%201.png](%E2%85%A0%20What%20is%20Control%20a8b30e5794de4830a80cd7905e8ed458/Untitled%201.png)

보통 W0=Wd가 되도록 함

**Closed-loop system의 특성rr**

- 정확성이 증가함
- 외부 장애와 시스템 변수의 내부 변화에 따른 민감도를 감소
- 비선형성과 왜곡의 효과를 감소시킴
- 대역폭을 증가시킴(시스템의 응답을 만족 시키는 입력 주파수 범위)
- 제대로 수행되지 않으면 불안정을 초래

## 4. 자동 제어 용어

![%E2%85%A0%20What%20is%20Control%20a8b30e5794de4830a80cd7905e8ed458/Untitled%202.png](%E2%85%A0%20What%20is%20Control%20a8b30e5794de4830a80cd7905e8ed458/Untitled%202.png)

### Variable

- [Reference Input] r : 시스템의 실제 입력
- [Cotrolled Variable] y : 시스템의 출력
- [Primary Feedback] b : y에 대한 함수값(피드백)
- [Actuating Error] e : r-b(에러가 반영된 input)
- [Manipulated Variable] u : G1의 출력, G2의 입력(보통 e보다 높은 에너지)
- [Disturbance] d : 출력 y에 영향을 끼치는 원치않는 외부요인

### Components

- [Control Element] G1 : e(에러)로 부터 발생된 u(조정된 입력)
- [Control System] G2 : 제어될 공정 및 시설
- [Feedback Element] H : y(출력)로 부터 발생된 b(피드백)

### Supplementary Terminology

- Forward Path : Actuating error e → Controlled variable y로 전송되는 정방향 경로
- Feedback Path : Controlled variable y → Primary feedback b로 전송되는 피드백 경로