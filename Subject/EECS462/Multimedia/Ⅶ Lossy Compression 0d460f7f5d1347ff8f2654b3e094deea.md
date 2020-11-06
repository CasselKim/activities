# Ⅶ. Lossy Compression

# Contents

1. Introduction
2. DCT
3. KLT Algorithm

# 1. Introduction

Lossy Compression은 데이터가 손실되더라도 용량만 줄이면 된다라는 관점에서 시작되었습니다. 텍스트, 금융 데이터같은 데이터들은 압축을 하더라도 손실이 전혀 없어야만 하지만, 영상이나 오디오같은 멀티미디어 데이터들은 인간이 지각하기 힘든 영역( 고주파 등 )을 삭제하고 압축을 시켰을 때, 파일의 크기가 훨씬 많이 줄어듭니다. 

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled.png)

텍스트를 손실압축하면 대충 이렇게 되려나

우리가 스크린샷을 계속 찍으면 글자가 깨져서 보이는건 이 때문입니다. 손실 압축을 계속 해버리니까 본래의 이미지 값을 잃어가게 되는것이죠.

# 2. DCT

Discrete Cosine Transform, 즉 이산 코사인 변환은 주파수 영역으로 변환하여 높은 주파수 영역을 제거하는 방법입니다. 인간의 눈은 낮은 주파수 성분(DC)에는 민감한 반면, 높은 주파수 성분(AC)에는 덜 민감하기 떄문이죠. 시간영역을 주파수영역으로 바꾸는것이 라플라스 변환이라면, 공간영역을 주파수영역으로 바꾸는것이 DCT라고 할 수 있다는겁니다.

## 인코딩

### 2D DCT에 사용될 8x8 DCT basis 구하기

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%201.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%201.png)

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%202.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%202.png)

그럼 위와 같은 8x8 matrix가 64개 나오게 됩니다. 그러니까 원소의 개수는 8^4개 겠죠?

### Input 영상을 gray level로 변환

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%203.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%203.png)

일단은 얘를 input 영상이라 해보자구요.

### Input영상과 각각의 matrix를 행렬곱

예를들어 F(0,0)은 Input영상의 **8x8 matrix**와 DCT basis의 0,0의 성분 **8x8 matrix**끼리 행렬곱을 하고 다 더한 결과죠.

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%204.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%204.png)

그럼 이렇게 주파수 영역에 대한 결과로 나오게 됩니다.

### 양자화

보통 좌상단의 4x4만 남기고 나머지를 0으로 하거나,

좌상단의 2x2만 남기고 나머지를 0으로 해서 파일의 크기를 줄입니다.

## 디코딩

거꾸로하면 어려우니 다른방법을 생각해봅시다.

인코딩 방식을 그대로 한번 더 하면 놀랍게도 이미지가 복원됩니다.

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%205.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%205.png)

수도코드와 이에 출력 결과는 아래에 있습니다 🤩

[Homework#5 DCT Lossy Compression](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/DCTLossyCompression.md)

# 3. KLT Algorithm

DCT 처럼 고주파수 성분을 날려서 압축하는 손실압축 방법입니다.

(주의 : 본 내용은 선형대수 내용이 포함되어 있습니다. ~~저같이~~ 선형대수 내용이 생각나지 않는 분들은 간단하게 환기시키고 시작합시다)

[[선형대수학 #3] 고유값과 고유벡터 (eigenvalue & eigenvector)](https://darkpgmr.tistory.com/105)

## Auto-correlation matrix(Rx)를 정의합니다.

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%206.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%206.png)

여기서 X는 input, XT는 transpose된 X겠죠. E는 확률이구요.

이렇게 생긴놈을 Auto-correlation이라고 한다네요.

## Rx에 대한 eigen vector를 구합니다.

선형대수에서 배운 eigen vector들로 Karhunen-Loeve transform 함수를 정의할 수 있습니다.

$$T=\left [ u_{1},u_{2},\cdots,u_{k} \right ]^{T}$$

## Output Y에 대한 Auto-correlation(Ry)를 구합니다.

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%207.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%207.png)

## 원하는 만큼 양자화합니다

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%208.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%208.png)

원하는 비율의 데이터만 남기고 모두 0으로 만듭니다.

## 디코딩

$$R{}'_{Y}=TR_{X}T^{T}$$

양자화된 Ry를 R'y라고 했을때, R'y는 위와 같은 식으로 표현될 수 있습니다.

$$R_{X}=T^{T}R{}'_{Y}T$$

그렇기에 Rx는 위에서 구한 T함수로 디코딩될 수 있죠.

## 예시

예시로 좀 더 간단하게 이해해봅시다.

`x1=(4,4,5)`, `x2=(3,2,5)`, `x3=(5,7,6)`, `x4=(6,7,7)`

이라는 4개의 1x3 벡터가 있다고 합시다.

1. 평균을 계산한다.

    ![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%209.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%209.png)

2.  Auto-correlation matrix Rx를 구한다

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2010.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2010.png)

3.  Rx의 Eigenvalue와 Eigenvector를 구한다

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2011.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2011.png)

4.  KLT를 구한다

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2012.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2012.png)

5.  Input vector X에서 평균 벡터를 빼고 KLT를 적용한다

$$y = T(x-m_{x})$$

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2013.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2013.png)

6.  원하는 만큼 양자화한다

![%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2014.png](%E2%85%A6%20Lossy%20Compression%200d460f7f5d1347ff8f2654b3e094deea/Untitled%2014.png)

7. KLT를 이용해 디코딩한다

$$x{}'=T^{T}y{}'+m_{x}$$

8. 결과

**기존값**

`x1=(4,4,5)`

`x2=(3,2,5)`

`x3=(5,7,6)`

`x4=(6,7,7)`

**KLT 결과**

`x1' = (3.9336, 3.9058, 5.3621)`

`x2' = (2.9984, 2.0993, 4.7217)`

`x3' = (5.3719,, 6.6844, 6.3471)`

`x4' = (5.6959, 7.3102, 6.5690)`

(데이터는 1/3로 줄어든 반면에 데이터는 약간의 손실만 있다는걸 알 수 있습니다)