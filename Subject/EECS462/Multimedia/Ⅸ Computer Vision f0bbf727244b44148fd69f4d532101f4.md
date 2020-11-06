# Ⅸ. Computer Vision


# Contents

1. Introduction of Computer Vision
2. Why Computer Vision?

# 1. Introduction of Computer Vision

## Importance of vision

인간의 오감 중 시각으로 얻는 정보는 전체 감각기관 중 90% 이상을 차지합니다. 인간은 태어나서 보기 시작한 모든 정보로부터 스스로 학습하게 되죠.

그렇기에 이 중요한 기능을 컴퓨터(로봇)에 구현하고자 하는 노력에서 비롯된 학문, CV(Computer Vision)이 점점 발전하고 있습니다.

## 2D, 3D Computer Vision

각각의 2D, 3D 영상 센서로부터 획득한 영상을 다양한 분야에 사용합니다.

2D Vision은 문자인식, 얼굴인식에 주로 사용되고 3D Vision은 3차원 스캐닝, 3차원 TV 등에 사용됩니다.

## Uses

- character recognition, car plate recognition
- face detection, recognition
- defect inspection
- gesture recognition
- detection, tracking

## Stereo Vision

![%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled.png](%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled.png)

사람의 양안은 서로의 각도가 살짝 다릅니다. 그래서 인간의 뇌는 이 두 정보를 종합하여 Depth(깊이)를 측정하죠. Stereo vision은 여기에서 영감을 받아 두개 이상의 이미지를 합쳐 Depth 정보를 얻어냅니다. 

![%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%201.png](%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%201.png)

- City modeling
- Augmented Reality
- 3D TV
- Vehicle Vision

등에서 사용됩니다.

# 2. Why Computer Vision?

현대는 이미지와 동영상정보가 엄청나게 범람하고 있습니다. 하지만 이 정보들에는 엄청난 가치가 있지만, 분석하기에 쉽지 않습니다. Ambiguity(3D세계 → 2D로 투영)와 다른 영향들(조명, 모양, 카메라 특성)등에 의해 쉽게 변형되기 때문입니다. 그래서 이 엄청난 정보를 적절하게 사용하기 위해 꼭 필요한 학문입니다.

## Three Stages of Computer Vision

### low-level

Image → Image

![%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%202.png](%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%202.png)

### mid-level

Image → features

![%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%203.png](%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%203.png)

### high-level

features → analysis

![%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%204.png](%E2%85%A8%20Computer%20Vision%20f0bbf727244b44148fd69f4d532101f4/Untitled%204.png)