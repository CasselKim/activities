# Ⅳ. Time Domain Analysis

# Contents

1. Test Signals
2. Time Response of First-Order Systems
3. Time Response of Second-Order Systems
4. Time response indices

# 1. Test Signals

시간응답(time Response)를 살펴보기 위한 test signals에는 단위계단 입력, 임펄스입력, 경사입력, 사인 입력 등이 있다.

그 중 단위 계단 입력(Unit step response)를 알면 나머지를 유추할 수 있기 때문에 가장 많이 사용된다.

## Time Response

Stable한 시스템에서, 총 시간 응답은 일반적으로

$$y(t)=y_{t}(t)+y_{ss}(t)\\y_{t}(t):과도응답(transient\ response)\\ y_{ss}(t)\ :\ 정상상태응답(steady-state\ response)$$

**Time domain Analysis : 과도 응답과 정상상태 응답의 특징을 분석하는 것**

**Transient Response(과도응답) :** 시간이 많이 지나고 나서 정상상태에 들어가기 전에 보이는 응답.

폐루프 시스템의 극점, 영점의 위치와 관련이 있다.

**Steady-state response(정상상태응답) :**  정착시간(Ts)가 지나고 나서 어떠한 기준 목표값에서 오차가 2~5% 이하인 응답. 전달함수의 형번호(type number)와 관계가 있다.

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled.png)

unit pulse를 가까이서 보면 이렇게 과도응답이 보인다

## Test Signals(상수,1차함수,2차함수)

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%201.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%201.png)

# 2. Time Response of First-Order Systems

## RC회로

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%202.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%202.png)

RC회로에서의 미분방정식

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%203.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%203.png)

RC회로 미분방정식을 라플라스 변환

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%204.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%204.png)

블록 다이어그램으로 표현

## Unit-step Response

입력이 **r(t) = u(t)**인 단위계단함수라면, 라플라스변환하면 **R(s) = 1/s**

$$Y(s)=\frac{1}{\tau s+1}\cdot\frac{1}{s}=\frac{1}{s}-\frac{\tau}{\tau s+1}=\frac{1}{s}-\frac{1}{s+\frac{1}{\tau}}$$

라플라스 역변환하면

$$y(t)=1-e^{-\frac{t}{\tau}}\ \ \ \ (t\geq0)$$

t=0에서의 기울기는

$$\left [\frac{dy}{dt}\right ]_{t=0}=\frac{1}{\tau}$$

error signal은

$$e(t)=r(t)-y(t)=e^{-\frac{t}{\tau}}$$

steady-state error(ess)은 0 (무한대로 보내는듯)

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%205.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%205.png)

오차가 발생한다

## Unit-ramp Response

입력이 **r(t) = t**인 단위램프함수라면, 라플라스변환하면 **R(s) = 1/(s^2)**

$$Y(s)=\frac{1}{\tau s+1}\cdot\frac{1}{s^{2}}\\=\frac{1}{s^{2}}-\frac{\tau}{s}+\frac{\tau^{2}}{\tau s+1}\\=\frac{1}{s^{2}}-\frac{\tau}{s}+\frac{\tau}{s+\frac{1}{\tau}}$$

라플라스 역변환하면

$$y(t)=t-\tau(1-e^{-\frac{t}{\tau}})\ \ \ \ (t\geq0)$$

error signal은

$$e(t)=r(t)-y(t)=\tau(1-e^{-\frac{t}{\tau}})$$

steady-state error(ess)은 τ (역시 t를 무한대로)

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%206.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%206.png)

## Unit-impulse Response

입력이 **r(t) = δ(t)**인 단위임펄스함수라면, 라플라스변환하면 **R(s) = 1**

error signal은

$$e(t)=r(t)-y(t)=\delta(t)-\frac{1}{\tau}e^{-\frac{t}{\tau}}$$

steady-state error(ess)은 0

# 3. Time Response of Standard Second-Order Systems



대부분의 제어설계가 2차함수 시스템 분석으로 이루어져있음. 차수가 그 이상이라도 2차함수로  근사시켜서 분석할 수 있음

## Transfer Function

$$\frac{Y(s)}{R(s)}=H(s)=\frac{\omega^{2}_{n}}{s^{2}+2\zeta\omega_{n}s+\omega^{2}_{n}}$$

## **Variables**

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%207.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%207.png)

### Dampling

**Dampling(제동, 감쇠)** : 기계적 진동에서 그 크기가 점차적으로 약화되는 현상

**Dampling Force(제동력, 감쇠력)** : 마찰력처럼 이동방향의 반대방향으로 운동을 방해하는 힘

$$s_{1,2}=\begin{cases} -\zeta\omega_{n}\pm j\omega_{n}\sqrt{1-\zeta^{2}}\equiv -\sigma\pm j\omega_{d} & \text{ if } 0< \zeta<1 \\  -\omega_{n}(\zeta\pm\sqrt{\zeta^{2}-1}) & \text{ if } \zeta\geq 1 \end{cases}$$

**감쇠비 ζ에 따라 두 개의 실수 또는 켤레 복소수 극점을 가진다.**

## unit step response

$$Y(s)=\frac{\omega^{2}_{n}}{s^{2}+2\zeta\omega_{n}s+\omega^{2}_{n}}\times\frac{1}{s}\ \ \ \ as\ R(s)=\frac{1}{s}$$

### Undamped response(ζ=0)

$$Y(s)=\frac{\omega_{n}^{2}}{s(s^{2}+\omega_{n}^{2})}=\frac{1}{s}-\frac{s}{s^{2}+\omega_{n}^{2}}\\y(t)=1-cos\omega_{n}t$$

$$s_{1},s_{2}=\pm j\omega_{n}$$

에서 두 극점을 가진다

### Undamped response(0<ζ<1)

$$s_{1},s_{2}=-\zeta\omega_{n}\pm j\omega_{n}\sqrt{1-\zeta^{2}}$$

$$Y(s)=\frac{\omega^{2}_{n}}{s^{2}+2\zeta\omega_{n}s+\omega^{2}_{n}}\times\frac{1}{s}=\frac{1}{s}-\frac{s+2\zeta\omega_{n}}{s^{2}+2\zeta\omega_{n}s+\omega_{n}^{2}}$$

이 때,

$$\frac{s+2\zeta\omega_{n}}{s^{2}+2\zeta\omega_{n}s+\omega_{n}^{2}}=\frac{(s+\zeta\omega_{n})+\zeta\omega_{n}}{(s+\zeta\omega_{n})^{2}+(1-\zeta^{2})\omega_{n}^{2}}\\=\frac{s+\zeta\omega_{n}}{(s+\zeta\omega_{n})^{2}+(1-\zeta^{2})\omega_{n}^{2}}+\frac{\zeta}{\sqrt{1-\zeta^{2}}}\times\frac{\sqrt{1-\zeta^{2}}\omega_{n}}{(s+\zeta\omega_{n})^{2}+(1-\zeta^{2})\omega_{n}^{2}}\\=\frac{s+\zeta\omega_{n}}{(s+\zeta\omega_{n})^{2}+\omega_{d}^{2}}+\frac{\zeta}{\sqrt{1-\zeta^{2}}}\times\frac{\omega_{d}}{(s+\zeta\omega_{n})^{2}+\omega_{d}^{2}},\ \ \ \mathit{(\omega_{d}^{2}=(1-\zeta^{2})\omega_{n}^{2})}$$

라플라스 역변환하면

$$e^{-\zeta\omega_{n}t}(cos\omega_{d}t+\frac{\zeta}{\sqrt{1-\zeta^{2}}}sin\omega_{d}t)=\frac{e^{-\zeta\omega_{n}t}}{\sqrt{1-\zeta^{2}}}(\sqrt{1-\zeta^{2}}cos\omega_{d}t+\zeta sin\omega_{d}t)$$

삼각함수의 합공식을 이용하면

$$y(t)=1-\frac{e^{-\zeta\omega_{n}t}}{\sqrt{1-\zeta^{2}}}sin(\omega_{d}t+\phi)\ ,which\ \phi=tan^{-1}\frac{\sqrt{1-\zeta^{2}}}{\zeta}$$

### Critically damped response(ζ=1)

$$s_{1},s_{2}=-\omega_{n},-\omega_{n}$$

$$Y(s)=\frac{\omega_{n}^{2}}{(s+\omega_{n})^{2}}\frac{1}{s}=\frac{1}{s}-\frac{1}{s+\omega_{n}}-\frac{\omega_{n}}{(s+\omega_{n})^{2}}$$

라플라스 역변환하면

$$y(t)=1-e^{-\omega_{n}t}-\omega_{n}te^{-\omega_{n}t}$$

### Overdamped response(ζ>1)

$$s_{1},s_{2}=-\zeta\omega_{n}\pm\omega_{n}\sqrt{\zeta^{2}-1}=-\beta_{1}\omega_{n},-\beta_{2}\omega_{n},$$

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%208.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%208.png)

## Summary

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%209.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%209.png)

제타 값에 따른 그래프

제타 값이 0에 가까울수록 임계 안정한 상태가 되고 출력은 사인함수 곡선처럼 된다.

반면, 제타 값이 0에서 멀어질수록 시스템이 불안정하게 된다.

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%2010.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%2010.png)

## Time domain Analysis

Under-damped standard 2nd-order control system(0<ζ<1)에서 time response input은

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%2011.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%2011.png)

과 같이 주어진다.

# 4. Time response indices

![%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%2012.png](%E2%85%A3%20Time%20Domain%20Analysis%2094ff498f830e48e882c3eece38b7464b/Untitled%2012.png)

[블록선도, 과도응답](http://blog.naver.com/PostView.nhn?blogId=pro_000&logNo=220917994253)