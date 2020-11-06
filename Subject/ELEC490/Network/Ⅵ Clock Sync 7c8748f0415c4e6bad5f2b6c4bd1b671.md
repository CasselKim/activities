# Ⅵ. Clock Sync

# Contents

1. Clocks, drift rate, precision
2. A taxonomy for clock synchronization
3. Clock synchronization for embedded systems

동기화 Error = skew = offset = precision = accuracy

# 1. Clocks, drift rate, precision

## 시계의 오차 원인

- 온도차
- 최소 단위(int)
- 양자화효과(0.7초 = 1초)
- 읽고쓰는데 걸리는 시간

## 시간 동기화 기술

**하나의 시스템에서만 작용하는 근사화된 동기화 기술**

- 최대 허용오차를 지정
- 동기오차 → 대역폭의 손실
- 상황분석, 원인분석
- NCS는 어쩔수없이 딜레이와 지터(빨라졌다 느려졌다) 발생 → 동기화의 어려움

해결법

- 샘플링 주기를 짧게함 (비싸짐)
- 기준 시간을 보내줌 (ticks)
- 시간을 동기화 (처음에 동기화시키고 다음엔 알아서)

## 물리적인 시계

센서, 오실리에이터

## 논리적인 시계

[NCS20 0506-L6b](https://www.youtube.com/watch?v=WraVGfRnO3U&list=PLAlfUECvWx7l8oPvKpwYsrFTW7O1b6zKO&index=10)

---

# 2. A taxonomy for clock synchronization

---

# 3. Clock synchronization for embedded systems