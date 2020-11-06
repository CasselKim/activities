# Ⅴ. Time-Triggered Protocols

# Contents

1. Networks for hard real-time systems
2. Comparison of event-triggered vs 
3. Requirements of safety-critical systems
4. Typical time-triggered protocols
5. Industrial Ethernet

# 1. Networks for hard real-time systems

**보장되어야하는 것**

- Predictability : 어떻게 돌아갈 지 예측가능해야함
- Determinism : 메시지는 정해진 시간안에 도착해야함
- Higher bit rate : 추가적인 여유 전송속도를 가져야함
- Fault tolerance : 여유 버스 채널을 가져야함

## X-By-Wire

비행기만큼 안전하지만 자동차에 적용할만큼 값싼 네트워크

---

# 2. Comparison of event-triggered vs time-triggered

## Event Triggered

이벤트가 랜덤하게 일어남 → 예측 불가능

deterministic하지 못함

강인하지 못함 (충돌로 인한 오작동 위험)

재전송의 반복, Thrashing

동기화작업 → 불필요함 (고장에 대응하기 어려움)

랜덤 딜레이를 다루기 힘듦

## Time Triggered(스케쥴)

- Predictable
- Deterministic, No collision, No Arbitration
- Efficient, low overhead
- Fault-tolerance

![%E2%85%A4%20Time-Triggered%20Protocols%20c4148bd9a54b4efbafe607e4f43306ca/Untitled.png](%E2%85%A4%20Time-Triggered%20Protocols%20c4148bd9a54b4efbafe607e4f43306ca/Untitled.png)

노드가 있든 없든 간에 기차는 간다

→ 시불변 시스템

상대방의 준비 여부와 상관없이 **각자 테스트를 진행할 수 있음**. 나중에 통합하더라도 똑같이 움직임

**Fault-tolerant**

- 풍부한 메시지 채널
- 수신단에서 에러를 바로 탐지
- 버스 가디언 : Babbling idiot 오류(에러 시 더미값을 계속 송신하는 것)를 방지하는 스위치(메시지를 보낼때만 ON)

### 단점

**Inflexibility** : 유연하지 못함

모든 노드에서 시간동기화가 엄격하게 유지되야함 (어려움+부하)

이벤트 메시지에 대응하기 어려움 (에어백)

재전송을 허용 X → 메시지를 한번에 여러개보냄

![%E2%85%A4%20Time-Triggered%20Protocols%20c4148bd9a54b4efbafe607e4f43306ca/Untitled%201.png](%E2%85%A4%20Time-Triggered%20Protocols%20c4148bd9a54b4efbafe607e4f43306ca/Untitled%201.png)

interoperability : 호환성, sporadic : 비주기적,  replica : 중복

---

# 3. Requirements of safety-critical systems

## Message error rate (메시지 오류 발생률)

1 - ( 1 - bit_error_rate ) ^ bits per message

= 1 - ( 정상 작동할 확률 ) = 오류가 발생할 확률

---

# 4. Typical time-triggered protocols

## TTCAN

16비트 카운터, 64번의 기본사이클

**단점**

- TTCAN 칩을 사야함
- 풍부채널이 없음
- 버스가디언이 없음
- 데이터 비율이 CAN 한계를 넘지 못함
- Master가 클락 고장으로 메시지를 보내지 않는 오류(fail-silent)를 이해하지 못함
    - 동기화 실패의 가능성

## TTP/C

싼값에 safety-critical system을 쓰기 위한 해결책

1 사이클을 Round라는 시간 단위로 나눠서 그걸 또 SRU라는 시간 단위로 나눔(노드 단위)

이중 채널로 구성(똑같은 시간에 똑같은 내용 보냄)

### SRU

![%E2%85%A4%20Time-Triggered%20Protocols%20c4148bd9a54b4efbafe607e4f43306ca/Untitled%202.png](%E2%85%A4%20Time-Triggered%20Protocols%20c4148bd9a54b4efbafe607e4f43306ca/Untitled%202.png)

윗단은 다 알아서 해줌 (Host-Independant)

- 읽고 쓰는걸 동시에 할 수 있음

TTP Controller단에 메모리를 하나 박아놓음

- CAN에서는 버퍼를 사용
- TTP/C는 스케쥴표를 미리 다 넣어놓음

MeDL이라는 언어를 이용해 제어 수행

### Fault Tolerance

- 시간 동기화
- Determinism
- Fail-silent (3개의 노드를 하나로 구성)
- TDMA(똑같은 메시지를 두번보냄) : 똑같은 내용을 총 4번 보내는거임ㅋㅋ
- 멤버쉽 서비스  : 고장이 나면 컨트롤러에서 자동판단, 유저가 보기 쉽게 판단해서 보여줌
- Clique avoidance : 정상 판단 알고리즘 → 그룹이 나뉠수도잇음(vote) → 이걸 방지
- Never Give-up : 오류 발생해도 차선책을 지원함 (Graceful degradation)
- Bus Guardians

**장점**

- Fault-tolerant
- Efficient (low overhead)
- 호스트-독립적 (유저와 무관, 뒷단은 다 알아서 해줌)

단점

- Flexible하지 못함

## FlexRay

### Passive Bus

채널마다 다르게 운용가능

### Active Star

각 노드가 고장나더라도 Star가 Bus Guardians역할을 해줌

싱글 채널 - 듀얼 스타, 듀얼 채널 - 듀얼 스타, 듀얼 채널 - 적층 스타

**근데 하이브리드 듀얼 채널은 쓰지 맙시다**

(1채널은 버스, 2채널은 스타 이런거)

Bit coding = NRZ

microtick 크기는 달라도 됨

macrotick 크기는 다 같아야함

64 사이클

static + dynamic + symbol window + network idle time으로 이루어짐

모든 슬롯의 길이는 같아야함(적어도 비슷하게)

2개의 채널에 보낼거면 같은거 보내야함(다른거 x)

F-TDMA : Flexible한 TDMA, ByteFlight

카운트를 증가

해당되는 카운트 인덱스가 있으면 메시지를 보냄

메시지전송 중에는 카운트 x

채널별로 카운트가 달라지게됨

TDMA인데 Event-triggered느낌

 

장점

- 구조,전송,풍부의 유연함을 보장
    - Time + Event섞은거, 다양한 구조사용가능

---

# 5. Industrial Ethernet

deterministic하지 않다고 안쓰기에는 너무 아깝자나?

유저(이더넷) - 시간 동기화 - TTCAN, TTP/C 구조

**COTS** : Commercial off the shelf, 상용된 제품

## EtherCAT

- TDMA
- 비주기성 메시지 미지원
- SIL3 인증을 받음(존나 안전하다)
- Fault-tolerance(Bus guardian x)

## TTEthernet

- 이중채널 지원
- 주기성, 비주기성 메시지 지원
- SIL4 인증(씨발개안전함)
- 근데 유저그룹이 적음(잘 안씀)