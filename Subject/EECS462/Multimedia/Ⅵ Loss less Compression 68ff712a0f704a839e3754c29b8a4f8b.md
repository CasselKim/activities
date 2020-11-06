# Ⅵ. Loss less Compression


# Contents

1. What is Compression?
2. Information Theory
3. Shannon-Fano coding
4. Huffman coding
5. LZW Compression

# 1. What is Compression?

압축이란, 데이터 크기를 줄여서 저장공간을 더욱 더 잘 활용하기 위한 기술입니다.

그 중에서도 손실이 없는 압축방식을 **Loss less Compression(무손실 압축)** 이라고 합니다.

무손실 압축은 말 그대로 손실이 없는 압축이기 때문에 정보 엔트로피의 한계가 그대로 반영됩니다.

# 2. Information Theory

정보이론은 최대한 많은 데이터를 매체에 저장하거나 채널을 통해 통신하기 위해 **데이터를 정량화**하는 응용 수학의 한 분야입니다.

(더 자세한건 여기 정리해뒀습니다 😀)

3줄 요약해드리면,

- 정보 엔트로피란 사건에 대한 불확실성를 정량화한 것입니다.
- 정보가 불확실할수록 정보 엔트로피는 증가하게 되죠.
- **정보가 제일 불확실할때의 엔트로피가 최대 메시지 길이입니다.**

여기서 문제는 3번째입니다. 최대 메시지 길이가 정해져버리는거죠. 최소한 그거이상은 메모리를 확보해야되요! 더 압축시키고 싶어도 못시킨다는겁니다! 그게 바로 정보 엔트로피의 한계입니다.

# 3. Shannon-Fano coding

Prefix 방법을 이용한 가장 기본적인 데이터 압축방법입니다.

ZIP 파일 압축에 사용되는 대표적인 기법이죠.

## 인코딩

![%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled.png](%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled.png)

1. 높은 확률부터 낮은 확률 순으로 정렬된 부호와 확률의 배열을 두개의 조로 나눕니다.

    (이 때, 두개의 조는 확률이 같아야 합니다.)

2. 두개의 조에 각각 0과 1을 대응시킨 후, 각 조가 하나의 항 만을 포함하게 될때까지 반복합니다.

예를 들어, `HELLO WORLD` 라는 문자열은

![%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%201.png](%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%201.png)

와 같은 과정을 거쳐 `100 101 00 00 01 110 01 1110 00 1111` 으로 인코딩되겠죠.

# 4. Huffman coding

**데이터 문자의 등장 빈도에 따라서 다른 길이의 부호를 사용하는 알고리즘**입니다.

적게 나오는 문자일수록 더 긴 부호를 쓰고, 많이 나올수록 더 짧은 부호를 씁니다. 주어진 빈도에 대해 항상 죄적의 접두 부호를 만들어내며, Sorting 데이터의 경우 O(n)의 속도로 처리할 수 있습니다.

## 인코딩

![%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%202.png](%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%202.png)

알고보면 존나쉬워요. 위에꺼를 잘보세요.

1. 메세지에 대한 모든 캐릭터의 주파수(빈도)를 체크한다.
2. 주파수에 따라 캐릭터를 재정렬한다.
3. 제일 작은 거 두개를 합쳐서 트리를 만든다
4. `if 합친 부모노드 ≤ 다음 캐릭터 주파수` : 또 합친다
5. `else` : 다음 캐릭터랑 다다음 캐릭터로 새로운 서브트리를 만든다
6. 작은게 왼쪽으로 가게 해서 두 부모노드를 합친다
7. 끝까지 한다
8. 왼쪽 노드가 0, 오른쪽 노드가 1이 되게하면 인코딩 끝

위의 경우, 2번나온 캐릭터는 1000으로 길게 압축된 반면, 9번 나온 캐릭터는 01로 짧게 압축된 것을 볼 수 있습니다.

# 5. LZW Compression

허프만 알고리즘에서 살짝 진보한 형태입니다. 딕셔너리를 기반으로 행해집니다.

캐릭터 심볼 뿐만 아니라 심볼들의 조합 또한 딕셔너리에 넣기때문에 더 많은 데이터를 저장할 수 있습니다. gif, tiff 뿐만 아니라 유닉스에서의 압축에도 사용됩니다.

## 인코딩

문자열 : **BABAABAAA**

![%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%203.png](%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%203.png)

```markup
* PSEUDOCODE 
1  Initialize table with single character strings 
2  P = first input character 
3  WHILE not end of input stream 
4    C = next input character 
5    IF P + C is in the string table 
6      P = P + C 
7    ELSE 
8      output the code for P 
9      add P + C to the string table 
10     P = C
11 END WHILE
12 output code for P
```

같이 보면서 생각해보자구요.

문자열이 **BABAABAAA**입니다. 그러면 P=B에서 시작하겠네요. 

1. **P=B, C=A**

    **BA가 테이블에 없기때문에**

    - B를 출력
    - BA를 테이블에 추가
    - P=A
2. **P=A, C=B**

    **AB가 테이블에 없기때문에**

    - A를 출력
    - AB를 테이블에 추가
    - P=B

3. **P=B, C=A**

**BA가 테이블에 있기때문에**

- P=BA

4. **P=BA, C=A**

**BAA가 테이블에 없기때문에**

- BA를 출력
- BAA를 테이블에 추가
- P=A

요런식으로 반복해주시면 됩니다.

## 디코딩

![%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%204.png](%E2%85%A5%20Loss%20less%20Compression%2068ff712a0f704a839e3754c29b8a4f8b/Untitled%204.png)

```markup
* PSEUDOCODE
1  Initialize table with single character strings
2  OLD = first input code
3  output translation of OLD
4  WHILE not end of input stream
5      NEW = next input code
6      IF NEW is not in the string table
7          S = translation of OLD
8          S = S + C
9      ELSE
10         S = translation of NEW
11     output S
12     C = first character of S
13     OLD + C to the string table
14     OLD = NEW
15 END WHILE
```

역으로 하면 됩니다

주어진 인코딩 데이터가 `<66><65><256><257><65><260>` 이라고 할 때,

일단 모든 single 캐릭터로 구성된 테이블을 만들고,

OLD=66

66를 변환해 'B'를 출력합니다.

1. **OLD=66, NEW=65**

    **65가 테이블에 없기 때문에**

    - S = 'A' (65 변환)
    - S = 'A' + ''

    'A'를 출력

    C = 'A'

    'BA'를 테이블에 추가

    OLD = 65

2. **OLD=65, NEW = 256**

**256이 테이블에 있기 때문에**

- S = 'BA' (256 변환)

'BA'를 출력

C = 'B'

'AB'를 테이블에 추가

OLD = 256

잘 이해 안되시면 수도코드 따라서 이렇게 해보시는 것도 좋습니다.

### 수학적 모델

- 소스 코딩 이론 : 데이터 압축을 통해 데이터를 얼마나 줄일 수 있는가를 다루는 부분
- 채널 코딩 이론 : 데이터를 얼마나 안정적으로 보낼 수 있는가를 다루는 부분
- 부호율 - 변형 이론 : 손실 압축을 이용하여 얼마 만큼 압축할 수 있는가를 다루는 부분