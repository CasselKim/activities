# Error Diffusion Dithering

[Coding Challenge #90: Floyd-Steinberg Dithering](https://www.youtube.com/watch?v=0L2n8Tg2FwI&t=277s)

3 = 11(2)

4 = 100(2)

2비트 : 0~3

8비트 = 2^8 = 0~255

내가 가지고 있는 이미지는 x,y축 값을 가지는 픽셀의 조합으로 이루어져있다. 그리고 그 픽셀들은 RGB 컬러의 값을 가지고있다.

보통 RGB는 256가지의 빨강, 초록, 파랑색으로 이루어져 있다. 그런데 만약 이 경우의 수가 줄어든다면 어떨까? 만약 빨강이 0 or 255, 초록이 0 or 255, 파랑이 0 or 255 만 가능하다면? 즉, 색의 데이터가 1bit라면?

```python
# import Requirements
import cv2

# Input Sample Image + Preprocessing
sampled= cv2.imread('ryan.jpg')

# Dithering
for y in range(len(sampled)) :
    for x in range(len(sampled[0])) : 
        sampled[x][y] = list(map(lambda a:round(a/255)*255,sampled[x][y]))
        
# Save Output
cv2.imwrite('sampled.jpg',sampled)
```

```python
# import Requirements
import cv2

# Input Sample Image + Preprocessing
sampled_greyscale = cv2.imread('ryan.jpg',cv2.IMREAD_GRAYSCALE)

# Dithering
for y in range(len(sampled_greyscale)) :
    for x in range(len(sampled_greyscale[0])) : 
        sampled_greyscale[x][y] = round(sampled_greyscale[x][y]/255)*255
        
# Save Output
cv2.imwrite('sampled_greyscale.jpg',sampled_greyscale)
```

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled.png](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled.png)

그럼 만약 한 가지 컬러를 표현하는데 4가지 방법이 있다면?

그러니까, 빨강 4가지 + 파랑 4가지 + 초록 4가지를 표현할 수 있다면? (4 bit)

```python
# import Requirements
import cv2

# Input Sample Image + Preprocessing
sampled_greyscale = cv2.imread('ryan.jpg',cv2.IMREAD_GRAYSCALE)

# Dithering
for y in range(len(sampled_greyscale)) :
    for x in range(len(sampled_greyscale[0])) : 
        sampled_greyscale[x][y] = round(**3***sampled_greyscale[x][y]/255)*(255**/3**)
        
# Save Output
cv2.imwrite('sampled_greyscale_2bit.jpg',sampled_greyscale)
```

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%201.png](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%201.png)

헉 졸귀탱

하지만 이렇게 색의 표현이 제한되면 원본과의 오차가 발생한다. 이 오차를 이용하여 최대한 원본과 비슷하게 만드는 기법이 바로 오차 최소화 Dithering이다.

에러를 계산하는 방법은 다음과 같다

RGB값이 `[255, 150, 10]`인 픽셀 → 2bit Sampling → `[255,255,0]`

즉  에러는 `[0, -105, 10]`이 된다.

```python
# import Requirements
import cv2

# Input Sample Image + Preprocessing
dithered = cv2.imread('ryan.jpg')

# Dithering
for y in range(0,len(dithered)-1) :
    for x in range(1,len(dithered)-1) : 
        sampled = list(map(lambda c:(round(3*c/255)*(255/3)),dithered[x][y]))
        err = list(map(lambda c,d:c-d,dithered[x][y],sampled))
        dithered[x][y] = sampled
        
        dithered[x+1][y  ] = list(map(lambda c,e:c+e*7/16.0,dithered[x+1][y  ],err))
        dithered[x-1][y+1] = list(map(lambda c,e:c+e*3/16.0,dithered[x-1][y+1],err))
        dithered[x  ][y+1] = list(map(lambda c,e:c+e*5/16.0,dithered[x  ][y+1],err))
        dithered[x+1][y+1] = list(map(lambda c,e:c+e*1/16.0,dithered[x+1][y+1],err))
        
# Save Output
cv2.imwrite('ditherted_2bit.jpg',dithered)
```

```python
# import Requirements
import cv2

# Input Sample Image + Preprocessing
dithered = cv2.imread('ryan.jpg',cv2.IMREAD_GRAYSCALE)

# Dithering
for y in range(0,len(dithered)-1) :
    for x in range(1,len(dithered)-1) : 
        sampled = round(3*dithered[x][y]/255)*(255/3)
        err = dithered[x][y]-sampled
        dithered[x][y] = sampled
        
        dithered[x+1][y  ] = dithered[x+1][y  ]+err*7/16.0
        dithered[x-1][y+1] = dithered[x-1][y+1]+err*3/16.0
        dithered[x  ][y+1] = dithered[x  ][y+1]+err*5/16.0
        dithered[x+1][y+1] = dithered[x+1][y+1]+err*1/16.0

# Save Output
cv2.imwrite('ditherted_greyscale_4bit.jpg',dithered)
```

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%202.png](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%202.png)

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%203.png](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%203.png)

크게 보면 차이가 확연하게 보이지만 멀리서보면 거의 모르겠다

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%204.png](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/Untitled%204.png)

가까이서 보면 요렇다

```python
# import Requirements
import cv2

# input video
cap = cv2.VideoCapture("Irene.mp4")

# assertion part
if(cap.isOpened() == False) :
    print("Unable to read camera feed")

# get width, height from capture and set codec for saving
width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fourcc = cv2.VideoWriter_fourcc(*'XVID')

writer = cv2.VideoWriter('Dithered_2bit_4.avi', fourcc, 30.0, (width, height), 0)

# start playing video
while True :
  ret, frame = cap.read()
  if ret == False : break

	# turn color from BGR to Grayscale
  frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

	# Error Diffusion Dithering Algorithm
  for y in range(0,len(frame)-1) :
      for x in range(1,len(frame[0])-1) : 
          downscaled = round(frame[y][x]/255)*(255)
          err = frame[y][x]-downscaled
          frame[y][x] = downscaled

          frame[y  ][x+1] = frame[y  ][x+1]+err*7/16.0
          frame[y+1][x-1] = frame[y+1][x-1]+err*3/16.0
          frame[y+1][x  ] = frame[y+1][x  ]+err*5/16.0
          frame[y+1][x+1] = frame[y+1][x+1]+err*1/16.0    
  
	# save frame
  writer.write(frame)
  
	# break when keyboard input occurs
  if cv2.waitKey(33) > 0 : break

# shutdown
cap.release()
writer.release()
cv2.destroyAllWindows()
```

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/original.gif](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/original.gif)

원본 영상(8비트)

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/not_dithered.gif](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/not_dithered.gif)

다운샘플링된 영상(1비트)

![Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/dithered.gif](Error%20Diffusion%20Dithering%20e5ec89319f1946bfb7f06e1e1d19816f/dithered.gif)

디더링된 영상(1비트)