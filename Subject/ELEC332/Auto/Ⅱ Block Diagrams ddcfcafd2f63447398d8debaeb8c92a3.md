# Ⅱ. Block Diagrams


# Contents

1. Block Diagrams
2. Multi-Loop Block Diagrams
3. Laplace Transform

# 1. Block Diagrams

## System Modelling

제어 시스템 문제를 해결하기 위한 **시스템** 및 구성 요소에 대한 설명을 분석 및 평가에 적합한 형식으로 작성**(모델링**)하는 방법

## **System Modelling Method**

### **Linear System**

: Superposition(중첩)과 homogenity(균등)의 조건을 충족시키는 Linear한 System

### **Differential Equations**

: Linear System의 입출력 관계는 선형 미분 방정식의 형태를 취함

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled.png)

n≥m 인 물리적 시스템인 경우 인과 관계(causal) 시스템이라고 함

→ Laplace Transform을 적용시켜 Transfer Function을 얻어낸다

### **Transfer Functions**

: 미분방정식에 라플라스 변환을 취해 출력을 입력으로 나누어준 형태

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%201.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%201.png)

시스템의 입출력을 설명, 블록 다이어그램을 쉽게 그리게 해줌

### **Block Diagrams**

: 제어 시스템의 기능적 표현을 제공하는데 사용됨

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%202.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%202.png)

시스템 동작의 이해를 위해 Y(s)와 R(s) 사이의 관계(전달함수)를 유도해야함

예시

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%203.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%203.png)

Y(s) = G(s)E(s)

E(s) = R(s)-B(s) = R(s)-H(s)Y(s)

∴ Y(s) = G(s)R(s)-G(s)H(s)Y(s)

So,

$$\frac{Y(s)}{R(s)} = \frac{G(s)}{1+G(s)H(s)}=\frac{FTF}{1+OLTF}$$

Feedback과 Comparator를 Element Block 하나로 축소할 수 있음

# 2. Multi-loop Block Diagram

## 주의사항

- forward path loop 전달함수는 항상 같아야한다.
- 한 loop의 전달함수는 항상 같아야한다.=

## Appendix

블록 다이어그램의 간략화를 도와줄 appendix

### 1. Take-off Point를 앞으로

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%204.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%204.png)

### 2. Take-off Point를 뒤로

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%205.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%205.png)

### 3. Summer를 앞으로

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%206.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%206.png)

### 예제

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%207.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%207.png)

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%208.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%208.png)

1. x포인트를 앞으로 밀고

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%209.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%209.png)

2. G2랑 G3를 합친 뒤 G4랑 합치고

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2010.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2010.png)

3. a포인트를 뒤로 민다

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2011.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2011.png)

4. summer을 앞으로 보낸 뒤 연산

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2012.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2012.png)

5. summer을 앞으로 보낸 뒤 연산

## Tips

모든 Variables를 다적어주기엔 계산이 너무 복잡해지므로 각 포인트마다 임시변수를 지정한다.

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2013.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2013.png)

# 3. Laplace Transform

## Laplace transform

: 변환하려는 함수에 특정 지수 함수를 곱한 뒤 적분을 취한 값(시간→주파수)

우리가 시스템, 신호함수를 다룰때는 미적분 방정식을 풀어야 하는데, 라플라스 변환을 하면 대수방정식으로 바뀌어 계산이 편해짐

$$F(s)={\mathcal  {L}}\left\{f\right\}(s)=\int _{{0^{-}}}^{\infty }e^{{-st}}f(t)\,dt.\\\ \\\displaystyle s=\sigma +i\omega , \   σ와 ω는 실수.$$

라플라스 변환 기본식

## Properties

### 선형성

$${\mathcal  {L}}\left\{af(t)+bg(t)\right\}=a{\mathcal  {L}}\left\{f(t)\right\}+b{\mathcal  {L}}\left\{g(t)\right\}$$

### 미분

$${\displaystyle {\mathcal {L}}\{f'\}=s{\mathcal {L}}\{f\}-f(0)}$$

$${\displaystyle {\mathcal {L}}\{f''\}=s^{2}{\mathcal {L}}\{f\}-sf(0)-f'(0)}$$

$${\mathcal  {L}}\left\{f^{{(n)}}\right\}=s^{n}{\mathcal  {L}}\{f\}-s^{{n-1}}f(0)-\cdots -f^{{(n-1)}}(0)$$

$${\mathcal  {L}}\{tf(t)\}=-F'(s)$$

$${\mathcal  {L}}\{t^{{n}}f(t)\}=(-1)^{{n}}F^{{(n)}}(s)$$

$${\mathcal  {L}}\left\{{\frac  {f(t)}{t}}\right\}=\int _{s}^{\infty }F(\sigma )\,d\sigma $$

### 적분

$${\mathcal  {L}}\left\{\int _{0}^{t}f(\tau )\,d\tau \right\}={\mathcal  {L}}\left\{u(t)*f(t)\right\}={1 \over s}F(s)$$

### Time Shifting

$${\mathcal  {L}}\left\{f(t-a)u(t-a)\right\}=e^{{-as}}F(s)$$

$${\mathcal  {L}}^{{-1}}\left\{e^{{-as}}F(s)\right\}=f(t-a)u(t-a)$$

### 합성곱(convolution)

$${\mathcal  {L}}\{f*g\}={\mathcal  {L}}\{f\}{\mathcal  {L}}\{g\}$$

## 기본 변환식

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2014.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2014.png)

## 초기치 정리, 최종치 정리

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2015.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2015.png)

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2016.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2016.png)

**최종치 정리 : sF(s)의 극점이 s 영역의 좌반면에만 존재해야함**

## 라플라스 역변환

위의 기본 변환식을 반대로 적용해서 얻는다.

부분분수전개는 각 분수의 성분을 0으로 보내고 해당 성분을 가리면된다

## 반복 미분법

F(s)의 분모에 높은 차수의 분모 항이 있어, 부분분수를 전개했을때 항이 많이 생기면 그 항들은 반복 미분법을 이용해서 분자를 구할 수 있음

![%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2017.png](%E2%85%A1%20Block%20Diagrams%20ddcfcafd2f63447398d8debaeb8c92a3/Untitled%2017.png)

## 삼각함수 공식

[두배각 공식,삼각함수 항등식,삼각함수의 역함수,주기성, 대칭성, 이동 ,n배각 공식 등등..](https://3dmpengines.tistory.com/951)

[https://stementor.tistory.com/entry/5Laplace-transform8문제-풀이](https://stementor.tistory.com/entry/5Laplace-transform8%EB%AC%B8%EC%A0%9C-%ED%92%80%EC%9D%B4)

[https://it-learning.tistory.com/25?category=758486](https://it-learning.tistory.com/25?category=758486)