# Ⅲ. Modeling

# Contents

1. Modeling of Physical System
2. Mechanical System
3. Electronic Mechanical System
4. Rotational System
5. Modeling of Motor & Gear Train

# 1. Modeling of Physical System

기본 소자 RLC로 구성된 직렬회로와 병렬회로를 라플라스 변환 후 KCL와 KVL을 이용해 실제 시스템을 해석해보자. 중요한 점은 입력과 출력을 확실하게 정하고 해석을 해야 함.

## 직렬회로

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled.png)

기본 RLC회로를 생각해보자

$$e(t) = Ri(t)+L\frac{di(t)}{dt}+\frac{1}{C}\int i(t)dt$$

i(t)에 관한 식이니까 q(t)에 관한식으로 바꾸면 *q(t)' = i(t)*

$$L\frac{d^{2}q}{dt^{2}}+R\frac{dq}{dt}+\frac{q}{C}=e$$

초기화조건을 적용해 라플라스변환하면

$$(s^{2}L+sR+\frac{1}{C})Q(s) = E(s)$$

$$\frac{E(s)}{Q(s)} = \frac{1}{(s^{2}L+sR+\frac{1}{C})}$$

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%201.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%201.png)

이렇게 전달함수를 찾아낼 수 있다.

## 병렬회로

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%202.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%202.png)

병렬회로에서 i가 input, 인덕터의 자기플럭스 Φ가 output일때,

$$C\frac{d^{2}\phi}{dt^{2}}+\frac{1}{R}\frac{d\phi}{dt}+\frac{\phi}{L}=i$$

라플라스 변환을 거치면 주파수 영역에서

$$(s^{2}C+s\frac{1}{R}+\frac{1}{L})\Phi (s)=I(s)$$

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%203.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%203.png)

**만약 (input : i, output : v0)라면?**

$$C\frac{d^{2}v_{0}}{dt^{2}}+\frac{1}{R}\frac{dv_{0}}{dt}+\frac{v_{0}}{L}=\frac{di}{dt}$$

# 2. Mechanical System(기계 시스템)

## 시스템 분석을 위한 매개변수

### Mass(질량)

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%204.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%204.png)

- 질량(M)을 가진 물체에 F라는 힘을 가하면 a라는 가속도로 움직임
- 가속도(a)는 속도의 시간 미분값
- 속도(v)는 이동거리의 시간 미분값

### Damper(점성 마찰)

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%205.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%205.png)

- 점성 계수(B)를 가지고 있음
- 상대속도(relative_velocity)와 곱해져 F를 만듦

### Spring(탄성)

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%206.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%206.png)

- 탄성계수(K)를 가지고 있음
- 연장(압축)되는 거리(x)와 곱해져 F를 만듦

## 예시

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%207.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%207.png)

뉴턴 방정식으로 풀자

$$M\frac{d^{2}x}{dt^{2}}+B\frac{dx}{dt}+Kx=F$$

라플라스 변환

$$(s^{2}M+sB+K)X(s)=F(s)$$

Input F(s)에 대한 Output X(s)의 전달함수

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%208.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%208.png)

# 3. Electro Mechanical System(전기 기계 시스템)

[https://www.youtube.com/watch?v=j_F4limaHYI](https://www.youtube.com/watch?v=j_F4limaHYI)

## 로런츠 힘

가장 제한적인 형태로 도선의 길이가 L이고, 자기장과 전류가 수직한 방향으로 지난다면, 로런츠 힘 F는

$$F=BIL$$

또한, 길이가 L인 도체가 자기장 B에서 v의 속력으로 수직으로 움직이면 도체 양단에 걸리는 전압 e는

$$e = BLv$$

이다.

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%209.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%209.png)

## 예시(스피커)

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2010.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2010.png)

컨덕터의 힘이 Bobbin에 전달되어 코일이 voice에 따라 움직이며 sound를 발생시킴

**코일이 균일한 질량(M)과 점성 계수(B)를 가진다면 공기의 영향(이동한 거리)이 모델링될 수 있음**

### 코일의 질량과 점성계수에 의한 힘

$$M\ddot{x}+B\dot{x}=F$$

라플라스 변환

$$(s^{2}M+sB)X(s)=F(s)\\X(s)=\frac{1}{s^{2}M+sB}F(s)$$

### 코일이 자기장과 전류에 의해 받는 힘

$$F = B_{\phi}Li$$

라플라스 변환

$$F(s) = B_{\phi}LI(s)$$

### 블록 다이어그램

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2011.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2011.png)

전류(입력)과 움직인 거리(출력)간의 전달함수

### 회로에 연결된 스피커

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2012.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2012.png)

위 모델링의 연장선

로런츠 힘 공식

$$F = B_{\phi}Li$$

속도에 의한 공식으로 바꾸면

$$e_{coil}=B_{\phi}L\dot{x}$$

KCL을 돌리면

$$L\frac{di}{dt}+Ri+e_{coil}=V_{a}$$

라플라스 변환을 하면

$$E_{c}(s) = sB_{\phi}LX(s)$$

$$(sL+R)I(s)=V_{a}(s)-E_{c}(s)\\I(s)=\frac{v_{a}(s)-E_{c}(s)}{sL+R}$$

### 블록 다이어그램

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2013.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2013.png)

처음 걸어준 전압(Reference Input) + 자기장에 의해 발생한 전압(피드백)*

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2014.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2014.png)

전체에 대한 블록다이어그램

**결과적으로 인가한 전압(Va)에 의해 만들어지는 코일의 이동거리 관계식(전달함수)를 얻을 수 있음**

## Most Important

😠 **우리가 알고 싶은 입출력을 정하고, 그에 대한 미분 방정식을 만드는 것**

# 4. Rotational System(회전 시스템)

## 시스템 분석을 위한 매개변수

### 관성 모멘트

$$토크 = J(관성모멘트)\times 각가속도$$

$$T = J\times\frac{d\omega}{dt}=J\times\frac{d^{2}\theta}{dt^{2}}$$

### 토션 스프링(뒤틀림 스프링) : 뒤틀어서 탄생 발생시키는 스프링

$$토크 = K(탄성계수)\times각변위$$

$$T = K\times(\theta_{1}-\theta_{2})=K\int_{-\infty }^{t}(\omega_{1}-\omega_{2})d\tau$$

### 점성마찰

$$토크 = B(마찰계수)\times각속도$$

$$T = B\omega=B\frac{d\theta}{dt}$$

위의 공식들을 이용해 각각 모터(M)와 로드(L)에 걸리

 는 토크 방정식을 세운다

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2015.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2015.png)

토크(T)가 기계 시스템에서의 F의 역할을 한다

# 5. Modeling of Motor & Gear Train

## Modeling of Motor

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2016.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2016.png)

### 발전기의 법칙

$$T_{m}=K_{T}i_{a}\\(T_{m}:모터의 토크,\ K_{T}:모터토크계수,\ i_{a}:모터에 흐르는 전류)$$

$$e_{b}=K_{b}\frac{d\theta}{dt}\\(e_{b}:모터의\ 역기전력\ ;\ 발전기처럼\ 작동해\ 역으로\ 기전력이\ 발생)$$

### 식 풀이

KVL로 식 하나 유도

$$L_{a}\frac{di_{a}}{dt}+Ri_{a}+e_{b}=e\ \cdots\  (1)$$

토크방정식으로 식 하나 더 유도(로드가 없으니까 하나만)

$$J\frac{d^{2}\theta}{dt^{2}}+B\frac{d\theta}{dt}=T_{m}\ \cdots\  (2)$$

발전기법칙 두개를 라플라스 변환

$$T_{m}(s)=K_{T}I_{a}(s)\ \cdots\  (3)$$

$$E_{b}(s)=sK_{b}\theta(s)\ \cdots\  (4)$$

(1)을 라플라스 변환

$$(L_{a}s+R_{a})I_{a}(s)=E(s)-E_{b}(s)$$

$$I_{a}(s)=\frac{1}{L_{a}s+R_{a}}(E(s)-E_{b}(s))$$

(2)를 라플라스 변환

$$(Js^{2}+Bs)\theta(s)=T_{m}(s)$$

$$\theta(s)=\frac{1}{Js^{2}+Bs}T_{m}(s)$$

블록다이어그램으로 그리면

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2017.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2017.png)

~~개복잡하네 쉬펄~~

간소화시키면

$$T(s)=\frac{\theta(s)}{E(s)}=\frac{K_{T}}{s[(L_{a}s+R_{a})(Js+B)+K_{T}K_{b}]}$$

보통 La가 존나게 작아서 무시한다.

## Gear Trains(서보 메커니즘 기어 트레인)

### 서보 메커니즘이란?

제어 대상의 공간적 위치, 방향 혹은 자세 등을 제어하는 피드백 제어 시스템

예) 로봇의 팔 제어 시스템

[서보 메커니즘 : 김상진](http://www.aistudy.co.kr/control/servo_kim.htm)

### 서보 모터

서보 메커니즘을 실행하는데 사용되는 물질을 움직일 힘을 내는 장치

### 기어트레인

시스템의 한 부분에서 다른 부분으로 에너지를 토크, 속도, 변위의 형태로 전달해주는 장치. 서보 모터에 포함된다.

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2018.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2018.png)

보통 두 톱니바퀴 이빨 수의 비로 정의된다

$$상대\ 관성모멘트\ =\ (\frac{N_{1}}{N_{2}})^{2}J_{2}$$

$$상대\ 점성마찰계수\ =\ (\frac{N_{1}}{N_{2}})^{2}B_{2}$$

$$상대\ 쿨롱마찰토크\ =\ \frac{N_{1}}{N_{2}}F_{c2}\times\frac{\omega_{2}}{|\omega_{2}|}$$

  

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2019.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2019.png)

### 관계식

KVL(1)

$$L\frac{di_{a}}{dt}+Ri_{a}+e_{b}=e_{i}\ \cdots\ (1)$$

발전기 법칙(2)

$$T=Ki_{a}\ \cdots\ (2)$$

토크방정식(3)

$$J\frac{d\omega_{m}}{dt}+B\omega_{m}=T\ \cdots\ (3)$$

역기전력(4)

$$e_{b}=K_{b}\omega_{m}\ \cdots\ (4)$$

관성모멘트(5)

$$J=J_{m}+\frac{1}{n^{2}}J_{L}\ \cdots\ (5)$$

점성마찰계수(6)

$$B=B_{m}\ \cdots\ (6)$$

각속도비(7)

$$n=\frac{\omega_{m}}{\omega{L}}\ \cdots\ (7)$$

### 풀이

(2)번 라플라스변환

$$T(s)=KI_{a}(s)$$

(4)번 라플라스변환

$$E_{b}(s)=K_{b}\Omega_{m}(s)$$

(1)번 라플라스변환

$$I_{a}(s)=\frac{1}{Ls+R}(E_{i}(s)-E_{b}(s))$$

(3),(7)번 라플라스변환

$$\Omega_{m}(s)=\frac{1}{Js+B}T(s)$$

$$\Omega_{L}(s)=\frac{1}{n}\Omega_{m}(s)$$

![%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2020.png](%E2%85%A2%20Modeling%202943fec3b5bd4a4ea56f9d7e20eee4b4/Untitled%2020.png)