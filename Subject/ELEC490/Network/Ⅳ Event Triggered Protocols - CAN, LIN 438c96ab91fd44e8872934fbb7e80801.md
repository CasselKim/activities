# Ⅳ. Event Triggered Protocols - CAN, LIN

# Contents

1. CAN Physical Layer - bit timing, encoding
2. CAN Data Link Layer - message frame, error handling, arbitration
3. CAN message latency and bus length
4. LIN overview

# 1. CAN Physical Layer - bit timing, encoding

---

# 2. CAN Data Link Layer - message frame, error handling, arbitration method

## Frame format

- Data Frame : ID(고유번호)에 해당하는 **데이터를 보내는 프레임**
- Remote Frame : 데이터 프레임의 **전송을 요청하는 프레임** (데이터가 없음)
    - 아무리 많이 반복되도 상관없음

## Data Frame

2.0A와 2.0B 버전 두개가 있음

A는 A만, B는 AB둘다 받을 수 있음

## 우선순위

1. ID가 낮은 값 > ID 높은 값
2. 데이터 프레임 > 리모트 프레임
3. 2.0A  > 2.0B 

## 접근 필터링

![%E2%85%A3%20Event%20Triggered%20Protocols%20-%20CAN,%20LIN%20438c96ab91fd44e8872934fbb7e80801/Untitled.png](%E2%85%A3%20Event%20Triggered%20Protocols%20-%20CAN,%20LIN%20438c96ab91fd44e8872934fbb7e80801/Untitled.png)

`1`-`1`이면 이 부분의 ID는 무조건 1이여야함

`1`-`0`이면 이 부분의 ID는 무조건 0이여야함

`0`-`0,1`이면 이 부분의 ID는 뭐가 오든 상관없음

## Error Counter

에러가 발생하면 +8

정상적으로 동작하면 -1

128이상이 되면 Error Passive상태가 됨 (송수신 가능)

256이상이 되면 Bus OFF (송수신 불가, 껏다 켜야함)

---

# 3. CAN message latency and bus length

## Message Latency

최대 전송지연 : T + B_High + B_Low

T : 순수한 메시지 전송지연 (propagation, processing time), waiting 제외

B_High : 나보다 우선순위 높은 메시지 전송지연시간

B_Low : 나보다 우선순위 낮은 메시지 전송지연시간 (먼저 전송한경우)

**우선순위 최상 메시지 최대지연 : 메시지 1개 지연 2개만큼 (B_LOW 1개+자기꺼)**

---

# 4. LIN overview

- Master-Slave 방식 (Polling, 주기적으로 처리하는 것)
- 케이블 하나만 써서 전송
- 멀티캐스트
- 비동기방식 (CAN과 다르게 특별한 signal을 주면 시작임을 확인함)

## Physical Layer

- NRZ 인코딩
- 최대 16개 노드 연결 가능
- 최대 20kbps (CAN의 1/50)
- 전송거리 40m

## 동작 원리

Master-Slave : event triggered

Master가 요청을 해야지만 메시지를 전송할 수 있음 → 충돌 X

- arbitration이 필요없음
- deterministic하다
- flexible하다
- 재전송이 필요없음

## 구성

앞부분이 Master, 뒷부분이 Slave

### Master

Synch(1010101010) : 속도 참고용

ID(10비트) : 시작(1비트) + 종류(4비트) + 크기(2비트) + parity 체크(1의 갯수)(2비트) + 끝(1비트) 

### Slave

01이 시작되면 새로운 데이터가 시작됨