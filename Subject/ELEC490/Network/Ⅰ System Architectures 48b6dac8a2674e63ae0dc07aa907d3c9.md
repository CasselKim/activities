# Ⅰ. System Architectures

# Contents

1. A brief history of industiral automation
2. Computer controlled systems
3. Control system architectures
4. Benefits of NCS

---

# 1. A brief history of industiral automation

## Beginning of Feedback Control

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled.png)

기술이 발전하면서 기존의 제어방법보다 안정성, 퍼포먼스, 효율성, 그리고 강인함이 높은 **피드백 컨트롤**이 요구되게 됩니다. 기원전 270년 Ktesibios의 물시계, 기원전 50년의 self-leveling bowl등이 대표적이죠.

## Feedback Control for Industrial System

[1620년] 인큐베이터

[1788년] Flyball

[1920년] On-Off 제어

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%201.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%201.png)

껐다 켰다하면서 값을 조정

[1930년] PID 제어(비례-적분-미분 제어기)

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%202.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%202.png)

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/PID_Compensation_Animated.gif](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/PID_Compensation_Animated.gif)

비례, 적분, 미분을 이용해 값을 조정

## Beginning of Industrial Automation

원래는 그냥 눈으로 보고 대충(Manually) 제어를 했습니다. 하지만 센터와 엑츄에이터의 발전으로 공장 자동화가 진행되죠. 전자기기는 공장을 중앙집권제어화하기에 이릅니다.

---

# 2. Computer controlled systems

기기의 표준이 세워지고 작업들이 모듈화(세분화)되자 공장은 점점 넓어지기 시작합니다. 그에따라 효과적인 제어방법의 필요성이 대두됩니다.

그리고 1950년대, **DIgital Control**이 도입됩니다.

## DDC(Direct Digial Control)

DDC는 쉽게말해, 한대의 컴퓨터가 센서들의 제어기능을 담당하는 제어기입니다. 

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%203.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%203.png)

**장점**

- 파워, 속도, 제어의 수치를 제공
- 경제적임
- 가볍고 작음
- 명령(operation)이 없어짐

**단점**

- 신뢰성이 낮음

    (한 대의 컴퓨터에 집중되어 있으므로)

## Activities of Computer

**정보 제공** : 센서로부터 정보를 얻거나, 오퍼레이터에게  request를 보내 조언을 합니다.

**데이터 표시** : 센서 데이터를 읽고, 해석하여 오퍼레이터에게 디스플레이 해줍니다.

**직접 지시** : 오퍼레이터는 컴퓨터를 통해 다양한 레벨의 결정을 수행합니다.

---

# 3. Control system architectures

역사적으로 관리·제어 함수는 컨트롤러마다 나뉘어졌습니다.

## 중앙집권화식 구조(Centralized Architecture)

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%204.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%204.png)

1960년대부터 1980년대까지 이어져온 중앙집권화식 구조는, 디바이스들을 컴퓨터의 엉덩이에 와이어를 꼽으면서 이루어졌습니다. CPU의 강력한 제어기능, 모니터링 기능, 인터페이스 기능 등으로 DDC 시대의 시작을 알렸죠.

**장점**

- 전기적 측면에서 봤을 때, 명령 체계가 더욱 효율적으로 변하고
- 소프트웨어 모델이 더욱 간단해졌죠. 컴퓨터 하나에서 다 해결 가능하니까요.

**단점**

- 하지만 전선들이 너무 복잡하고
- 추후 수정이 어렵고
- 고성능 컴퓨터가 요구되고
- 강인함이 부족했죠(연결문제, 다른 치명적 오류)
- 결정적으로 예방적 유지보수가 안됩니다

## 구조의 변화(Transition of System Architecture)

중앙집권화식 구조에서 분리식 구조로의 변신은 많은 이점을 가져왔습니다.

**소비자 측면에서**

- 개발·운영비용이 줄어들고
- 퍼포먼스·기능성이 증가
- 라이프 사이클이 줄어들었습니다
- 의존성이 늘어남에 따라 표준이 더욱 빡빡해지게 되었죠(안전함)

**엔지니어 측면에서는**,

- 시스템이 더욱 복잡해졌기에 처리과정또한 더욱 빨라져야했죠.

    (멀티프로세싱 기술의 발전)

- 또한 임베디드 제어 시스템이 매우 낮은 코스트로 이루어졌습니다.

    (스마트 디바이스·필드버스의 등장)

## 분리식 구조(Distributed Architecture)

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%205.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%205.png)

컨트롤러들은 연속적인(Serial) 네트워크에 의해 연결됩니다. 하지만 컨트롤러들은 **여전히** 자신의 센서랑 액츄에이터를 가지고 있죠. 그러니까 컨트롤러가 디바이스에 들어간 형태라고 보면 됩니다.

## 완전 분리식 구조(Fully-Distributed Architecture)

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%206.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%206.png)

필드버스(디바이스)가 연속적인(Serial) 디지털 네트워크에 연결된 형태입니다. 네트워크에서 컨트롤러 뿐만 아니라 필드 디바이스까지 제어해버리는거죠.

개꿀입니다. 강인함이 증가하고 보통의 필드 시스템에서 기능성도 증가하죠.

---

# 4. Benefits of NCS

## 분산 제어 시스템(Distributed Control System, DCS)

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%207.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%207.png)

한줄 요약하면, **DCS는** 소형 DDC 시스템 여러개를 Serial하게 연결시켜 시스템을 구성한 것입니다.

여러개의 작은 중앙처리 장치 단위를 기능별로 나눈 뒤, 각 단위에서 주어진 역할을 수행하게 되죠.

위에서 말한거를 시스템화 시킨겁니다.

## 네트워크 제어 시스템(Networked Control System, NCS)

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%208.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/Untitled%208.png)

**NCS는** 적어도 하나 이상의 피드백 루프가 **한개의 네트워크를 통해** 폐쇄된 것입니다.

각 센서와 액츄에이터들, 컨트롤러들은 그 네트워크에 대한 인터페이스를 장착하고 있습니다. 네트워크들끼리 통신하는데에는 Serial Bus가 가장 흔히 쓰입니다.

![%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/1.png](%E2%85%A0%20System%20Architectures%2048b6dac8a2674e63ae0dc07aa907d3c9/1.png)

위에서 본 DCS와는 다르게 Direct로 연결되어 있지 않죠?

NCS는 하나의 네트워크를 통해 컴퓨터와 통신하고 제어를 수행하게 됩니다.

그로인해 간단한 연결, 설치·점검의 편의, 플러그앤플레이, 신뢰성, 안전성, 경제성 등의 이점을 얻을 수 있습니다.

### 1. 쉬운 연결

더 간단하고, 얇고, 가벼운 와이어를 사용합니다. 잘못 꽂을 일도 거의 없죠.

### 2. 강인한 데이터 전송

디지털 데이터 기반이기 때문에 노이즈에 강합니다.

### 3. 모듈화 디자인

고유의 기능성을 가지고, 표준화된 인터페이스로 연결된 **모듈**들로 구성되어 있습니다. 모듈단위에서 디자인되기 때문에 신뢰성 있고 기술을 적용하기 쉽죠. 유지보수도 쉽습니다. 얘들만 바꿔주면 되거든요.

### 4. 쉬운 설치

하드웨어 인터페이스(콘센트), 현장 프로그래밍, 백업 작업만 하면 설치 완료!

### 5. 열린 구조

여러 장비를 사용할 수 있으며 플러그앤플레이도 지원합니다

### 6. 구성성, 설정가능성, 확장성

시스템을 구성하고 바꾸기 편합니다. 노드 하나만 추가하면 새로운 시스템을 추가할 수 있죠.

### 7. 자가진단, 예방적 유지보수

원래는 멀티미터 같은게 있어야 했는데 NCS는 그딴거 필요없습니다. **로그**로 확인할 수 있거든요. 심지어 오류를 예측할 수도 있습니다. 오류가 나기전에 바꿔버리는 예방적 유지보수(predictive maintenance)도 가능하죠.

### 8. 향상된 신뢰성, 안정성, 그리고 fault-tolerance

물리적인 연결이 없으니까 연결에 대한 신뢰성이 증가합니다. 만약 네트워크의 일부분이 작동하지 않더라도 Shut-down 되지 않고 제한적이나마 기능을 유지하는 **Graceful Degradation**도 가능하죠.

### 9. 향상된 환경 보존성

누수 현상을 조기에 발견하여 환경을 지킵니다.

### 10. 경제성

아무튼 존나 쌉니다.