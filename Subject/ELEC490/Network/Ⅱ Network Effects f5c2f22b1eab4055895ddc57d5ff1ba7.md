# Ⅱ. Network Effects

# Contents

1. Challenging problems with NCS
2. Bandwidth, delay, jitter, dropout
3. Effects of network on control
4. Choosing a sampling period for NCS

# 1. Challenging problems with NCS

## Safety-Critical Systems

![%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled.png](%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled.png)

*"If it fails, people die."*

**Safety-critical system(안전 필수 시스템)**은 **시스템 고장이 치명적인 시스템**입니다. 

**Dependability(믿을 수 있게 서비스 할 수 있는 능력)**를 위해 극도의 제한이 요구되는 시스템이죠.

## NCS vs CCS

CCS(Centralized Control System) : 올바른 input은 올바른 output으로 이어짐이 보장됨

NCS(Networked Control System) : 올바른 input이 항상 올바른 output으로 이어지지 않음

특히 NCS는 timing과 value의 일관성을 얻기가 쉽기 않습니다. 또한 네트워크 대역폭은 근본적으로 **한계**입니다.

## Networked Architecture Challenges

NCS에는 몇가지 문제점이 있습니다.

- **잠재적인 개발 비용이 높고**(소프트웨에가 복잡하니까)
- **시스템의 성립이 어렵고**(동기화작업, 노드의 동적 추가·제거, 노드간의 정보공유)
- **상호운용성이 낮습니다**(subsystem마다 다른 구조와 소프트웨어, 호환성이 낮음)
- **안전문제를 다루기 점점 어려워지고**
- 프로세싱 지엽적 실패는 **다른 프로세서들로 하여금 문제를 찾고 해결하게 합니다.**
- **전송지연문제**도 있습니다. 결국 데이터의 일관성을 파괴하고 결함문제로 이끌죠.
- **간헐적인 미디어 전송실패**또한 존재합니다.
    - Message losses(메시지 로스)
    - Reorder(재배열)
    - Duplicated(재전송)
    - Data inconsistency(비일관성)

그렇기에 우리는 이런 실패를 인정해야합니다. 그에대한 대책이 있긴합니다.

- [비잔티움 장애 허용](https://www.notion.so/casselkim/Two-Generals-Problem-657a913e7724407fa03ec91fc9ce8d0d)
- 투표, 분산 알고리즘

근데 근-본적으로 문제는, **커뮤니케이션 채널이 불완전**하다는 겁니다.

한정적인 대역폭과 속도는 여러가지 이슈와 트레이드오프를 발생시킵니다. 그래서 선택과 집중으로 많은 부분을 포기해야만 했죠😭😭

---

# 2. Bandwidth, delay, jitter, dropout

## Network Speed & Bandwidth

### Bandwidth(대역폭)

**1초당 비트가 전송될 수 있는 개수**입니다. 1Mb/s, 1Gb/s 등으로 표현되죠.

### Bus(버스)

**버스**는 **컴퓨터안의 부품들, 컴퓨터간에 정보를 전송하는 통로**입니다. 이러한 표현에는 모든 하드웨어 인터페이스, 소프트웨어 인터페이스들을 포함합니다.

버스의 속도는 Bandwidth로 표현됩니다.

Bus speed = 1/bandwidth = bit time(Tbit) [1비트를 전송하는데 걸리는 시간]

B**andwidth는 무조건 패킷의 사이즈와 오버헤드(처리 시간,메모리)가 고려되어야합니다.**

효과적인 대역폭 설계를 위한 유일한 요소는 네트워크 스피드이기때문이죠.

![%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%201.png](%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%201.png)

일반적인 메시지 프레임, 데이터들은 패킷들속에 꾸깃꾸깃 접혀서 캡슐화합니다.

## Network Delay

총 지연시간은 다음과 같이 계산됩니다.

$$T_{delay}=T_{pre}+T_{wait}+T_{tx}+T_{post}$$

### T_pre(post) : Pre(post)-processing time

인코딩과 디코딩을 통해 데이터 ↔ 패킷 간 변환을 수행합니다.

디바이스에 의해 결정됩니다.

### T_wait : Queuing delay, waiting time

패킷이 버퍼로 접근하는데까지+큐에서 벗어나는데 까지 걸리는 시간입니다.

MAC 메카니즘, 트래픽, 노드개수, 우선 순위에 의해 결정됩니다.

### T_tx : Transmission time

패킷이 버스채널을 통해 물리적으로 움직이는 시간입니다.

데이터 비율, 메시지 크기, 노드 사이 거리 등에 의해 결정됩니다.

$$T_{tx}=T_{frame}+T_{prop}$$

T_frame은 패킷을 보내는데 걸리는 시간( *n* bits x T_bits )

T_prop은 1비트가 채널의 끝에서 끝으로 움직이는데 걸리는 시간

## Jitter

**Jitter(지터)**는 쉽게말해 **처리 시간 및 결과물의 도달 시간의 변동 폭** 입니다. 딜레이에 대한 변동성이죠. 메시지 충돌, 스케쥴링, 코드의 분기, 클럭의 이동 등이 원인이 됩니다.

지터는 신호를 왜곡시키고 시스템을 시간-다양성 시스템으로 변화시킵니다. 퍼포먼스가 감소하고 불안정합니다. 추가 비용 밝생, 제어 방식의 변화등을 야기하죠.

## Packet Dropout

Packet Dropout(패킷 손실)은 물리적 네트워크 링크 전송실패, 노드 전송 실패, 버퍼 오버플로우, 너무 긴 딜레이 등에 의해 발생합니다. 다른 노드들에 데이터 불안정성을 야기할 수 도 있습니다.

그런데 말입니다.

**제어에 의한 딜레이**는 거기에 맞춰서 하드코딩하면되는데 반해 

**지터에 의한 딜레이**는 시간에 따라 달라지는 함수거든요.

그래서 블록-다이어그램을 그려서 전달함수를 구해버립니다

![%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%202.png](%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%202.png)

사실 엄격하게 따지면 못씀. 지터때문에 왜곡일어나잖아요.

이 징그러운걸 더 보고싶으신분은 아래 링크를 참고하세요

Ⅱ. Block Diagrams

---

# 3. Effects of network on control

## **딜레이에 대한 동적 시스템**

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/PID_Compensation_Animated.gif](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/PID_Compensation_Animated.gif)

Performance degradation

![%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/root_locus_plot.gif](%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/root_locus_plot.gif)

Destabilization

파라미터를 조절하여 딜레이를 원하는대로 조정할 수 있습니다.

![%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%203.png](%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%203.png)

요렇게 시변함수로써 지터(에러)를 확인할 수 있습니다.

---

# 4. Choosing a sampling period for NCS

## Sampling Period of Digital Control

샘플링 주기가

- 너무 길면 퍼포먼스의 저하와 불안정성을 야기하고
- 너무 짧으면 컴퓨터에 로드가 과하게 걸리죠.

## Sampling Period of NCS

NCS도 같습니다. 뭐든지 적당한게 좋죠

![%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%204.png](%E2%85%A1%20Network%20Effects%20f5c2f22b1eab4055895ddc57d5ff1ba7/Untitled%204.png)

무조건 시험에 나올듯

근데 DCS와 다르게 **NCS는 샘플링 주기가 짧으면 오히려 퍼포먼스가 하락**합니다.

트래픽이 많아지기 때문이죠(그래프를 잘봅시다 위쪽이 worst, 오른쪽이 small임)

**지터가 작은 네트워크가 훨씬 좋음 아무튼 그럼!!**