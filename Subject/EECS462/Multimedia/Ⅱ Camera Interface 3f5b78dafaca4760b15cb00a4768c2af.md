# Ⅱ. Camera Interface

# Contents

1. Digital Interface
2. DSI,CSI

인터페이스의 개념부터 확실히 잡고 갑시다.

[인터페이스(Interface)](https://www.notion.so/Interface-5b8859787f994b0da7fdec16db769910)

# 1. Digital Interface

카메라에는 여러 종류가 있습니다. DSLR부터 산업용 카메라, 모바일 카메라 등 용도에 맞는 여러가지 카메라가 있는데 이 카메라들이 다른기기와 통신하기 위해서는 미리 정해진 규약(protocol), 즉 인터페이스가 필요합니다. 이 인터페이스들을 배워봅시다.

**아날로그 인터페이스 :** NTSC - BNC 커넥터 - 이미지 캡쳐 카드

**디지털 인터페이스** : [USB](https://www.notion.so/casselkim/USB-f0c8b0fbd9bb4a039a84bbc17c7dcd37), [GigE](https://www.notion.so/casselkim/Camera-Interface-3f5b78dafaca4760b15cb00a4768c2af#a4cd87a36b2c445f8198592343e225ff), [Camera Link](https://www.notion.so/casselkim/Camera-Interface-3f5b78dafaca4760b15cb00a4768c2af#0d5f4ca583274e729ee5828e8163f5b3), [IEEE 1394](https://www.notion.so/casselkim/Camera-Interface-3f5b78dafaca4760b15cb00a4768c2af#c97d8af6f43d4db7acc31768e74c6610) 등

## **USB**

## IEEE 1394

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled.png)

IEEE 1394는 IEEE(전기 전자 기술자 협회)에서 규정한 인터페이스 규격 중 하나입니다. 비싼 SCSI를 대체하고자 애플을 중심으로 개발되어 Texas Instruments에서 발표하였습니다. 애플에서 얘를 부르는 이름인 **FireWire**로 유명합니다

USB에 비해 빠르고 안정적이며, 낮은 CPU 점유율, [데이지 체인 연결](https://www.notion.so/casselkim/USB-f0c8b0fbd9bb4a039a84bbc17c7dcd37#76ecb4a9c1d8487f8172754393a67aa1)이 가능하다는 장점이 있었지만 흥행에 실패해 USB 3.0에게 자리를 내주었습니다.

### **속도**

- IEEE 1394a : 400 Mbits/s with 6 pin connector
- IEEE 1394b : 800 Mbits/s(일반), 3.2Gbits/s(최대)

### 연결 디바이스

- PC(direct of capture card)

### **케이블**

- IEEE 1394a,b : STP(Shielded twisted pair) 케이블을 사용
- IEEE 1394b : optical fiber cable(HPCF, GOF, POF) or UTP 케이블 사용 가능

### 커넥터

- IEEE 1394a : Latch Type
- IEEE 1394b : Screw Type

## Camera Link

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%201.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%201.png)

머신 비전용 카메라 많이 사용되는 인터페이스입니다.

높은 화소 수 데이터, 빠른 fps를 가진 카메라에서 발생되는 대량의 데이터를 그대로 PC에 인가하면 CPU 점유율이 올라가게 되고, 시스템의 불안정성으로 이어지게 됩니다.

카메라 링크는 이 데이터를 Frame Grabber에 전달해 PC 대신 데이터를 처리하여 다량의 데이터이 발생해도 CPU에 부하가 걸리지 않도록 도와 시스템의 안정성을 보장합니다.

### 속도

단일 케이블 : 최대 255 Mbytes/s
2개 케이블 : 최대 850 Mbytes/s

### 연결 디바이스

Frame grabber

### 케이블

카메라링크 전용 케이블

### 커넥터

MDR 26-pin connector;
SDR, HDR 26-pin connector (Mini Camera Link)
HDR 14-pin connector (PoCL-Lite).

### 파워

Frame grabber

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%202.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%202.png)

## GigE Vision

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%203.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%203.png)

IEEE 802.3 Standard 기반으로 만들어진 GigE(기가비트 이더넷)은 초기에 너무 느린 전송속도(10M, 100M)을 보완하기 위해 만들어진 표준입니다.

최대 100m의 전송거리, 별도 Frame Grabber가 필요없고 하나 PC에 다수 Camera를 연결 가능, 손쉽게 설치할 수 있다라는 장점이 있지만 대역폭에 한계가 있고 CPU 점유율이 높다는 단점이 있습니다.

### 속도

- 평균 : 1~2 Gbits/s
- 최대 : 10 Gbits/s

### 연결 디바이스

- PC

### 케이블

- 구리선 : 최대 100m
- 광섬유 : 최대 5km

### 커넥터

- Copper Ethernet
- Copper Ethernet with vision locking screws
- 10 Gigabit Ethernet direct attach cable
- Ethernet fiber optic cable

### 파워

- 이더넷 케이블
- 외부 전원

# 2. DSI, CSI

[[2016116783_김성록]DSI조사보고서.hwp](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/2016116783_DSI.hwp)

## 배경

기존의 커넥티비티 시스템에 호환되도록 문제없이 발전되던 전자기기들

→ 새로운 미디어개체의 발전으로 기기들이 점점 소형화되기 시작함

→ 배터리 동작을 하게 되면서 한정된 전원으로 효율적인 사용이 요구됨

→ 커넥티비티 부품들 또한 최소한으로 조정되야했음

→ 기술과 부품의 표준화를 통해 복잡성, 제조 단가의 절감 + 제조의 유연성 및 호환성 재고

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%204.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%204.png)

위와 같은 이유로 2003년에 ARM, 인텔, 노키아, 삼성 등이 모여 MIPI(Mobile Industry Processor Interface) 얼라이언스를 설립하게 됩니다.

MIPI는 기기들의 재사용, 호환성을 강화하기 위해 [AP(Application Processor)](https://www.notion.so/AP-Application-Processor-9551d8e9c7e94be98de702a49ae1968e) 와 인터페이스 사양을 개발하는데, 다양한 워킹 그룹 중 카메라와 디스플레이에 관련된 표준을 정하는 곳도 있습니다.

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%205.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%205.png)

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%206.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%206.png)

## 물리계층

MIPI에서는 정의하는 물리계층에 대한 사양서 3개를 발표 : D-PHY, M-PHY, C-PHY

- D-PHY(2009) : 카메라,디스플레이 연결 인터페이스
    - 일반적인 물리계층(PHY, Physical Layer, OSI 7 계층모델 상의 최하위 계층)의 역할을 수행.
    - 데이터의 시작과 끝을 알리는 SoT/EoT를 추가
    - 데이터 변환(직렬 ↔ 병렬)
    - DDR 클럭 시스템 관리(클럭 레인을 통한 클럭 신호 고속 전송)
    - **고속 모드**
        - SLVS(Scalable low voltage signaling) 방식
        - 0.2V 공통모드 전압 + 0.2V 스윙 인 80Mb/s ~ 1Gb/s 차분신호로 전송
        - 1개의 클럭 레인 + 1~4 데이터 레인
    - **저전력 모드**
        - LVCMOS(Low-vlotage CMOS) 방식
        - 1.2V 스윙인 최대 10Mbps 단일 출력 신호
        - 0개의 클럭 레인 + 2개의 데이터 레인

            (데이터에 클럭 신호를 포함, 임베디드 방식)

        - 단일 종단 전송 방식을 사용하면 한번에 두 비트 정보

            (고속 : 0, 1, 저전력 : 00, 01, 10, 11)를 전송 가능

- M-PHY(2011) : RF모듈,스토리지,멀티미디어 데이터부품 연결 인터페이스
    - D-PHY는 최대 전송속도의 한계(1Gb/s)
    - 소형 폼 팩터에서 EMI의 영향이 커지기 쉬워 이를 대처하기 위해 개발됨
    - 데이터에 클럭신호를 포함, 임베디드 방식
    - 수신단에서 데이터에서 클럭을 읽어내기 위한 CDR(clock data recovery)
    - 데이터에 0과 1이 반복되면 클럭을 읽어내기 힘드므로 8b/10b 인코딩
    - 고속모드 : 레인당 최대 5.8Gb/s

        저전력모드 : 레인당 최대 10k~600Mb/s

    - 양방향 송수신
        - 송신용 레인들이 송신용 서브 링크를 구성
        - 수신용 레인들이 수신용 서브 링크를 구성

            ![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%207.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%207.png)

    - D-PHY는 카메라,디스플레이를 위한 물리 계층이기때문에 DSI, CSI에 사용
    - M-PHY는 다양한 프로토콜에 사용됨(DSI-2, CSI-3, UFS, SSIC)
        - SSIC : [USB IF](https://ko.wikipedia.org/wiki/USB-IF)에서 USB 통신 전용 물리계층에서 모바일 기기와의 통신을 위한 규격  HSIC의 USB 3.0버전
        - HSIC → SSIC로 바꾸면서 PHY를 M-PHY로 사용하게됨

            ![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%208.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/Untitled%208.png)

- C-PHY(2014) : 카메라, 디스플레이 연결 개선 인터페이스
    - D-PHY를 개선한 버전
    - D-PHY : 1개 클럭레인 + 4개 데이터 레인, 레인당 2개의 라인, 총 10개의 라인
    - C-PHY : 0개 클럭레인 + 3개 데이터 레인, 레인당 3개의 라인, 총 9개 라인
    - 클럭은 데이터에 임베디드되므로 클럭을 찾아내는 모듈 CDR이 사용됨
    - 하나의 레인은 각각 High, Middle, Low의 데이터를 전송하는 3개의 라인으로 구성됨
        - 총 27가지의 신호 송신가능(차분신호 특성이 있는 6가지만 사용)
    - 전송 속도 단위 : Gsym/s(초당 심볼 수, 5,7 Gps)

(토글창을 내리면 세부설명이 나옵니다)

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/213.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/213.png)

모바일 기기를 구성하는 부품 중에서 디스플레이와 카메라를 어플리케이션 프로세서(AP)와 연결하기 위한 프로토콜이 바로 DSI와 CSI입니다. 얘들이 앞의 D-PHY, M-PHY, C-PHY들을 사용하게 되는거죠.

## **DSI**

DSI는 디스플레이를 위한 규격입니다. D-PHY를 사용하며 최근 4K와 같은 고해상도 영상을 지원하기 위해 VESA의 DSC를 채용하기도 했죠. DSI-2는 C-PHY를 사용하기 위해 만들어진 프로토콜입니다.

### DSI 버전별 스펙

![%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/123141.png](%E2%85%A1%20Camera%20Interface%203f5b78dafaca4760b15cb00a4768c2af/123141.png)

사실 DSI 버전별 스펙은 D-PHY, C-PHY 스펙에 영향을 받게 됩니다.

왜냐하면 DSI란건 애초에 D-PHY, C-PHY를 사용하기 위한 프로토콜일 뿐이니까요.

### DSI의 적용사례

스마트폰, 태블릿, 랩탑, 2in1PC 뿐만 아니라 자동차산업에서 대쉬보드 디스플레이, 차내정보시스템에서도 사용되고, 웨어러블, IoT 그리고 VR/AR 산업에서도 적용되고 있습니다.

## **CSI**

CSI는 카메라 모듈을 위한 규격입니다.

- CSI : D-PHY
- CSI-2 : C-PHY
- CSI-3 : M-PHY

를 지원합니다