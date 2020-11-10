# Web Crawling

업무 자동화 프로세스를 해보자

# Web Crawling이란?

"Web scraping is a computer software technique of extracting information from websites."

Web Crawling(Web scraping)은 **인터넷의 페이지를 방문해서 자동으로 자료를 수집하는 과정**을 말한다. 거미줄(Web)을 돌아다니는(Crawling) 모습같다해서 웹 크롤링이라고 부른다.

현대는 기술의 발전과 함께 데이터 생산량이 폭발적으로 늘어나고 있다. 하루에 7억여개의 트위터가 올라오고, 4백만시간의 유튜브 컨텐츠가 업로드되며, 7천만여개의 게시글이 인스타그램에서 포스팅된다. 이미 인간이 일일이 구별할 수 있는 양을 넘어섰다는 뜻이다. 그래서 업무를 자동화시켜 사용자 대신 자료들을 모아줄 프로그램이 필요하다.

사실 데이터 사이언티스트(data scientist)들이 가장 시간을 할애하는 부분~~(가장 하기 싫어하는 부분)~~이 데이터 전처리(data preprocessing)인데, 데이터 전처리를 좀 더 쉽게하려면 웹 크롤링을 잘해서 깔끔한 데이터셋을 모아야한다. 

웹 크롤링을 수행할 수 있는 언어들은 다양하다. R, Go, Rails, Python, JS 등등 데이터 분석에 사용되는 언어들은 거의다 가능하지만 우리는 그중에서도 가장 쉬운 **파이썬**으로 해보려고 한다. 파이썬은 다양한 외부 라이브러리로 이루어져있다는 장점을 가진 강력한 언어이다. 당연히 웹 크롤링 관련 라이브러리도 존재하는데, **BeautifulSoup4**와 **Selenium**이 그것이다.

BeatifulSoup4는 HTML과 XML의 스크립트를 가져와서 파싱하는데 사용된다. 사용법이 간단하고 다양한 메소드들이 있지만, 사용자의 동적행동(사이트를 옮긴다던가)을 적용하지 못하고 특정 페이지의 스크립트만 가져올 수 있다.

Selenium은 실제로 브라우저가 동작하는 것 처럼 동작하면서 크롤링을 진행한다. JS/CSS와 DOM 형태 구조의 웹 데이터를 긁어올 수 있을 뿐만 아니라 active x, 팝업, 이미지 인식 등의 복잡한 동작들도 처리할 수 있다는 장점이 있지만, 사용법이 비교적 어렵고 느리다. 그래서 보통 Selenium과 BeautifulSoup를 같이 쓴다.

[BeautifulSoup](Web%20Crawling%2023f2f76b83b9459298a9819d679dda81/BeautifulSoup%20be1cde265951473282384baebecf6069.md)

[Selenium](Web%20Crawling%2023f2f76b83b9459298a9819d679dda81/Selenium%200c5b61217a07451e83ad495bf69c2b2e.md)

예전의 VBA를 활용한 엑셀 매크로는 더이상 독보적이지 않다. 마이크로소프트조차 파이썬을 엑셀에 적용하려고 고려중이라고 한다.

[Microsoft Considers Adding Python as an Official Scripting Language to Excel](https://www.bleepingcomputer.com/news/microsoft/microsoft-considers-adding-python-as-an-official-scripting-language-to-excel/)

BeautifulSoup와 Selenium을 적절하게 섞어서 사용해 중복된 프로세스를 자동화시키고, 생산성또한 비약적으로 상승시키도록 하자. 

하지만 티케팅 자동 매수, 마스크 자동 매수와 같은 비도덕적인 개발은 피하도록 주의해야할 것이다.

# 참고 사항

## Selenium과 BeatifulSoup4 속도 차이 비교

[파이썬 - 셀레니움 VS Requests 크롤링 시간 비교하기(로그인 과정)](http://blog.naver.com/PostView.nhn?blogId=popqser2&logNo=221430894929&categoryNo=0&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)