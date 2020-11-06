# Ⅳ. Image Processing

# Contents

1. Digital Images
2. Linear Filtering
3. Spartial Filtering
4. Edge Detection
5. Template matching

# 1. Digital Images

**디지털 이미지** : 2차원의 n x m 행렬

**해상도** : 픽셀의 개수

## Point

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled.png)

이미지는 이차함수 `f(x,y)` 로 표현됩니다. 각 함수값은 해당 컬러에 대한 밝기값이죠.

## Neighborhood

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%201.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%201.png)

한개의 Point는 n x n -1 개의 neigborhood를 가지고 있습니다.

3 x 3이 보편적이긴 하지만 5 x 5, 7 x 7로 사용됩니다.

## Point Operation

원본 Point는 q(x,y), Operate 된 Point는 p(x,y)로 표현됩니다.

### Threshold

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%202.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%202.png)

문턱 임계값(Threshold)를 기준으로 Point Operation의 결과값을 출력합니다.

위의 예시는 Threshold를 기준으로 크면 255, 작으면 0을 출력하는 Binary image입니다.

### Image Inversion

`p(x,y) = 255 - q(x,y)`

색 반전을 수행하는 Point Operation입니다.

### Hisrogram Stretching

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%203.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%203.png)

특정 밝기값에 weight와 bias를 주는 Operation입니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%204.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%204.png)

0에서 100 사이의 밝기부분만 있으므로 0에서 255까지 weight(255/100) 만큼 Stretching하여 골고루 퍼지게 함

## Area Operation

### Convolution

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/1_D6iRfzDkz-sEzyjYoVZ73w.gif](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/1_D6iRfzDkz-sEzyjYoVZ73w.gif)

움짤 최고

식은 외울필요 없다. 원리만 이해하자. 중요한 점은, 내적이 아니라 행렬 곱을 하는 거다.

# 2. Linear Filtering

1차원 Filter로 convolution operation 하는것을 의미합니다.

## Single Filter

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%205.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%205.png)

저렇게 생긴 필터라고 생각하시면 편합니다.

neighborhood를 전혀 고려하지 않으니까 원본 이미지가 나오겠죠?

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%206.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%206.png)

반면, 위의 경우 p(x)가 q(x+3)의 값을 가져오므로  왼쪽으로 -3만큼 Shift된 영상이 나옵니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%207.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%207.png)

이 경우, p(x)가 q(x-1), q(x), q(x+1)의 값을 1/3씩 가져오므로 평균값이 취해진(흐린) 영상이 나옵니다.

## Multi Filter

영상처리는 Linear하기 때문에 원본영상에 각각의 필터 연산을 해주고 합칠 필요없이 필터끼리 연산을 하고 원본에 적용해도 결과가 똑같이 나오게 됩니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%208.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%208.png)

p(x) = q(x)*h1(x) - q(x)*h2(x) = 2q(x) - q(x) = q(x)

p(x) = q(x) * ( h1(x)-h2(x) ) = q(x) * h3(x) = q(x)

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%209.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%209.png)

위의 경우를 생각해봅시다. 위의 그림을 그대로 연산하면

0, 0, 0, -1/3, 5/3, -1/3, 0, 0, 0

라는, neighborhood와 굉장히 어색한 사이인 Sharpening filter가 되는 겁니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2010.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2010.png)

영상이 좀 뚜렷해(Sharp)진게 보이시나요?

# 3. Spatial Filtering

2차원 Filter로 convolution operation 하는것을 의미합니다. 3 x 3 필터를 주로 사용합니다.

## Average Smoothing

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2011.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2011.png)

1차원 Blur 필터와 마찬가지로 neighborhood 들과의 평균을 구하는 필터입니다.

원본 이미지의 밝기가 유지되도록(합치면 1) 앞에 coefficient를 붙여줍니다(1/9).

## Gaussian Smoothing

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2012.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2012.png)

확률과정에서 나오는 개념으로, 평균값에서부터 퍼져나가는(통계적 분포를 따르는) 가우시안 함수를 이용하여 이미지를 부드럽게(Smoothing) 만듭니다. 

$$G(x) = \dfrac{1}{(2\pi\sigma^2)^{1/2}}\exp\left\{-\frac{x^{2}}{2\sigma^2}\right\}$$

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2013.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2013.png)

1차원 가우시안 분포함수입니다.  위의 함수를 거치면 1차원의 가우시안 필터가생깁니다.

시그마 σ 값이 커질수록 Blur가 더 많이 됩니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2014.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2014.png)

해당 부분에 가우시안 필터를 적용하면 주위에 비해서 도드라지게 높던 픽셀값이 주위와 비슷한 값을 가지게 되는 것을 볼 수 있습니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2015.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2015.png)

# 4. Edge Detection

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2016.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2016.png)

왼쪽 그림을 보면 배경,모자, 머리카락과 얼굴, 그리고 눈이 있습니다.

우리 사람은 어떻게 배경과 모자를 나누고, 모자와 머리카락을 나눠서 인식할 수 있는 것일까요?

정답은 밝기 변화량 입니다. 배경에서 모자로 갈때 급격하게 밝기가 변화하여 생기는 Edge를 보고 우리는 배경과 모자를 구분할 수 있는 것이죠.

이렇게 **밝기 변화량**을 보고 **Edge를 찾아내는 행위를 Edge Detection**, **Edge Detection을 수행할 때 사용하는 Filter를 Edge Filter**라고 합니다.

위의 그림에서 밝기 변화량은 기울기라고 할 수 있습니다. 기울기는 미분을 통해 알 수 있죠.

$$\frac{\partial f}{\partial x}=f(x+1,y)-f(x,y)$$

연속함수가 아닌 이산 함수 f(x,y)에서 x 방향으로의 일차 미분은 이렇게 근사할 수 있습니다.

그러므로

가로에 대한 밝기 변화량은 [1, 0, -1] 필터를 통해,

세로에 대한 밝기 변화량은 [1, 0, -1]T 필터를 통해,

둘 다에 대한 밝기 변화량은 그라디안트를 통해 얻어 낼 수 있습니다.

## Sobel Edge Detection

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2017.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2017.png)

위의 필터를 사용하여 edge를 검출해 내는 방법입니다.

x, y필터를 각각 입력 영상에 연산한 후, 그라디안트를 취해주면 모든 축에 대한 Edge 값이 출력됩니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2018.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2018.png)

흰색부분 = 기울기 값이 큰 부분 = Edge 부분

## Laplacian Filters

Sobel Edge Filter는 기울기가 최대가 되는 곳이 Edge라고 판별하는 반면에

Laplacian Filter는 기울기의 변화량이 0이 되는 곳, 즉 극대·극소값이 Edge라고 판별합니다.

$$\frac{\partial^{2}f}{\partial x^{2}}=[f(x+1,y)-f(x,y)]-[f(x,y)-f(x-1,y)]\\=f(x+1,y)+f(x-1,y)-2f(x,y)$$

이산 함수의 이차 미분은 일차 미분함수를 위와 같이 한번 더 미분해서 얻을 수 있습니다.

이 경우

가로에 대한 밝기 변화량은 [1, -2, 1] 필터를 통해,

세로에 대한 밝기 변화량은 [1, -2, 1]T 필터를 통해,

둘 다에 대한 밝기 변화량은 그라디안트를 통해 얻어 낼 수 있습니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2019.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2019.png)

그라디언트를 취한 필터의 모습

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2020.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2020.png)

원본(좌), 라플라시안 필터(우)

출력 영상의 기준값이 회색인 이유는 음수가 존재하기 때문입니다. (-127 ~ 127)

확실한 Edge 검출을 위해서 **Zero-detection** 알고리즘을 추가하기도 합니다.

또한, Gaussian Smoothing과 함께 자주 쓰이기 때문에 두 필터를 합쳐서 **LOG 필터**라고도 합니다.

## Median Filter

미디언 필터는 주변의 값들을 오름차순 정렬하여 그 중간값을 출력으로 내보내는 필터입니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2021.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2021.png)

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2022.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2022.png)

Salt&Pepper Noise

미디언 필터는 왼쪽과 같이 점처럼 생기는 Salt&Pepper Noise(소금&후추 잡음)을 효과적으로 제거할 수 있습니다.

Sorting이 사용되기 때문에 속도가 느릴 수 있긴 하지만요.

# 5. Template matching

Template matching은 도로 사진에서 사람이나 자동차가 어디에있는지를 탐색하는 알고리즘입니다. 요점은 **어디에 있는지(detection)** 입니다. **무엇인지(recognition)**는 그 이후의 문제이구요.

원리는 간단합니다. 원본영상에 찾고자 하는 필터 이미지를 convolution하는 거죠. 그러면 b와 같이 유사도(similarity)에 대한 영상이 나오게 됩니다. 여기서 제일 밝은 부분이 필터 이미지와 가장 유사한 부분이라고 판단하여 (c)와 같이 detect 합니다.

![%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2023.png](%E2%85%A3%20Image%20Processing%20ccc27ff32e4d48e9b985626fd480098d/Untitled%2023.png)