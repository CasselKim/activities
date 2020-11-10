# BeautifulSoup

[BeautifulSoup 공식문서](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

## 설치

`pip install beautifulsoup4`

`pip install bs4`

`conda install -c anaconda beautifulsoup4`

## 연습

op.gg 사이트의 동영상 리스트를 가져와보자

![BeautifulSoup%20be1cde265951473282384baebecf6069/Untitled.png](BeautifulSoup/Untitled.png)

(TMI) op.gg 사이트는 월평균 5억원의 수익을 낸다. 여러분도 이런걸 만들어보도록 하자.

(TMI2) op.gg 사이트는 다이나믹(반응형) 웹 페이지이다. 모바일로 들어가도 m.op.gg가 아니라 op.gg이다. 다이나믹 웹을 사용하면 개발 비용도 반으로 줄어들고 유지 보수도 굉장히 쉬워진다. 궁금하면 찾아볼 것.

![BeautifulSoup%20be1cde265951473282384baebecf6069/Untitled%201.png](BeautifulSoup/Untitled%201.png)

아이유를 검색해봤다. 최근에 게임이 잘 안풀렸나보다.

우리는 이 유저의 최근 전적 4개에서 플레이시간, 플레이 캐릭터, 그리고 KDA 데이터를 가져올 것이다.

```python
from urllib.request import urlopen
from bs4 import BeautifulSoup as bs
```

필요한 라이브러리를 임포트해준다

```python
page = urlopen("https://www.op.gg/summoner/userName=%EC%95%84%EC%9D%B4%EC%9C%A0")
document = page.read()
page.close()
```

urlopen 메소드에 주소를 기입하고 read 메소드로 스크립트를 가져온다.

```python
soup = bs(document, 'html.parser')
```

관습적으로 BeautifulSoup로의 변환은 soup 변수를 사용한다.

첫번째 인자(document)는 어떤 문서를,

두번째 인자('html.parser')는 어떤 parser를 이용해 파싱할 것인지 지정해준다.

BeautifulSoup에서 파싱을 하는 방법은 크게 두가지가 있는데,

**select 메소드**를 이용하는방법과 **find(find_all) 메소드**를 이용하는 방법이다.

[select 메소드](BeautifulSoup/select.md)

[find(find_all) 메소드](BeautifulSoup/find.md)

## 참고자료

[Beautifulsoup : Is there a difference between .find() and .select() - python 3.xx](https://stackoverflow.com/questions/38028384/beautifulsoup-is-there-a-difference-between-find-and-select-python-3-x#comment63497345_38028384)

[코.알.못. 마케터도 크롤링하기#4. BeautifulSoup으로 정보가져오기](https://m.blog.naver.com/PostView.nhn?blogId=kiddwannabe&logNo=221177292446&proxyReferer=https%3A%2F%2Fwww.google.com%2F)