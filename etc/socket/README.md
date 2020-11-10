# Socket Programming

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled.png)

소켓 : 통신 접속점. 소켓을 통해 통신망으로 데이터를 송수신함 

- 윈도우 소켓은 DLL을 통해 기능이 제공됨

소켓 프로그래밍 : 소켓을 이용한 TCP/IP 프로그래밍 (보통 유닉스 환경을 가리킴)

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%201.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%201.png)

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%202.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%202.png)

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%203.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%203.png)

무작정 연결을 시도하는 것이 아니라, 미리 등록해놓은 요청(포트 번호)에 따라 처리함.

- 클라이언트 소켓 : 요청을 보내는 소켓
- 서버 소켓 : 요청을 받아들이는소켓

**두 소켓은 데이터를 주고받는 역할을 하는게 아니라 요청과 수락만을 담당함!**

## 소켓 API 실행 흐름

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%204.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%204.png)

### 클라이언트 소켓

1. 클라이언트 소켓을 **생성(create)**
2. 서버 소켓에 **연결(connect)**
3. 연결이 되면 데이터를 **송수신(send/recv)**
4. 처리 완료 후 소켓을 **종료(close)**

### 서버 소켓

1. 서버 소켓을 **생성(create)**
2. 사용할 IP 주소와 포트번호를 소켓에 **결합(bind)**
3. 연결 요청이 오는지 **주시(listen)**
4. 요청이 오면 **허가(accept)** 후 데이터 소켓 생성
5. 데이터를 **송수신(send/recv)**
6. 처리 완료 후 소켓을 **종료(close)**

## 클라이언트 소켓 프로그래밍

1. 클라이언트 소켓 생성( socket() ) : 빈 소켓을 생성

   - TCP 소켓 : Stream 타입, 세션 연결 후 데이터전송(안정,느림)
   - UDP 소켓 : Datagram, 세션 연결하지 않고 전송(불안정,빠름)

2. 연결 요청( connect() ) : IP 주소와 포트 번호로 연결 요청을 보냄

   블럭 방식으로 동작함(결과가 나오기 전까지 실행이 끝나지 않음)

   호출이 성공하면 데이터를 주고받을 준비가 됬다는 뜻임

3. 데이터 송수신( send() / recv() )

   마찬가지로 블럭 방식으로 동작함

   얼마나 수신할 지 모르므로 새로운 스레드 생성 후 데이터 수신

4. 소켓 닫기( close() ) : 재사용 불가능. 추가연결은 새로운 소켓에서 가능

## 서버 소켓 프로그래밍

1. 서버 소켓 생성( socket() ) : 빈 소켓을 생성
2. 서버 소켓 바인딩( bind() ) : 소켓+(IP주소, 포트번호)
   - 소켓이 중복된 포트 번호를 사용하지 않도록 내부적으로 관리
3. 클라이언트 연결 요청 대기( listen() ) :  요청이 수신되면 대기상태 종료 후 리턴
   - 값이 리턴되는게 아니라 수신됬는지(Success) 실패했는지(Fail)을 리턴
   - 연결 요청에 대한 정보는 시스템 큐(Queue)에 쌓임
4. 클라이언트 연결 수립( accept() ) : 새로운 소켓을 생성 후 Dequeue된 연결과 매핑
5. 데이터 송수신( send() / recv() )
6. 소켓 닫기( close() )

[소켓 프로그래밍. (Socket Programming)](https://recipes4dev.tistory.com/153)

[게임 네트워킹의 이해 10 - Socket Programming](https://www.youtube.com/watch?v=aWq9C7RARJI&t=784s)

1.5배로 보는걸 추천

# 실전

## C++ ↔ C++

소켓의 구조를 직접 확인해보자

cmd창에서 `netstat -an`을 실행시켜보면 자신의 PC에 연결된 소켓 정보가 나열된다.

[윈도우 기반 서버, 클라이언트 예제](https://jaimemin.tistory.com/6)

기본적인 코드는 위의 블로그를 보면서 따라가면 된다.

근데 이 블로그는 Visual Studio 2013버전에 최적화되있는듯해서 그냥 돌리면 안돌아갈꺼다. 조금 설정을 건들여줘보자

- 솔루션 탐색기 → 프로젝트 우클릭 → 속성 → 구성 속성 → C/C++ → 일반 → SDL 검사 → 아니요
- 솔루션 탐색기 → 프로젝트 우클릭 → 속성 → 구성 속성 → C/C++ → 언어 → 준수 모드 → 아니요
- 코드에서 `#inlcude` 밑에 `#define _WINSOCK_DEPRECATED_NO_WARNINGS` 추가

1. 비주얼 스튜디오 창을 2개 열고 server용과 client용 프로젝트를 각각 생성해준다. 

2. server.cpp, client.cpp를 생성해주고 코드를 작성한다.

3. 솔루션 탐색기 → 프로젝트 우클릭 → 속성 → 구성 속성 → 링커 → 입력 → 추가 종속성에 ws2_32.lib을 추가한다.

4. 로컬 Windows 디버거를 실행하여 .exe 파일을 생성하고 cmd창을 두개 연다.

5. 각각의 .exe파일이 생성된 경로에 접근하여 

   `server.exe 포트번호` 를 서버 cmd창에 입력한뒤

   `client.exe 내IP 포트번호`  를 클라이언트 cmd창에 입력하면

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%205.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%205.png)

요렇게 Hello World를 주고받는다.

server.exe, client.exe는 프로젝트이름에 따라 달라질 수 있으니 생성된 .exe파일을 보고 입력하면 된다.

## Python ↔ Python

파이썬은 더 쉽다. 밑의 블로그를 따라가보자

[파이썬 소켓 프로그래밍 - 클라이언트 / 서버 예제](https://webnautes.tistory.com/1381)

사실 .py 파일을 생성해서 실행하는거지만 주피터 노트북을 사용하면 엄청 간단하게 결과를 확인할 수 있다.

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%206.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%206.png)

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%207.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%207.png)

## C++ ↔ Python

이 두놈을 같이 하면 어떻게 될까?

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%208.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%208.png)

C++(Client) ↔ Python(Server)을 적용시켜보았다.

일단 원래의 코드를 쓰면 실행이 안될거다. 서로 다른 블로그에서 예제를 가져왔기 때문에 C++ 클라이언트, Python 서버가 모두 데이터를 받는 역할을 하기 때문에 아무 동작도 안하기 때문. 파이썬 Server 코드에서 recv를 지우고 Client 코드의 sendall 부분을 가져오자.

그대로 가져와서 실행해보면 받긴 받는데 이상한 문자가 섞일거다. 아마 파이썬 문자열이 \0 문법을 지원하지 않아서 C++이 문자열의 끝을 인식 못하는것 같다. "Hello World!\0"를 명시해주면 해결된다.

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%209.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%209.png)

Python(Client) ↔ C++(Server)도 잘된다.

C++ 코드는 그대로 놔두고 파이썬 코드만 고쳐보자(~~그게 더 쉬움~~)

별거 없다 sendall을 recv로 바꾸면된다(recv뒤에 1024는 전달받을 버퍼의 크기)

아까 말했던것처럼 C++은 문자열의 끝을 \0으로 찾기때문에 문자열에 \0이 붙어있는걸 확인할 수 있다. 나중에 쓸때는 적절하게 슬라이싱해서 사용하면 되겠다.

## UDP를 이용한 통신

SOCK_STREAM → SOCK_DGRAM으로 바꿔주고

listen(), accept() 과정을 삭제,

sendall() → sendto()

recv() → recvfrom() 으로 바꿔주는 등 몇개의 작업만 거치면 된다. TCP/IP보다 간단한 구성이다.

[2일차]파이선 환경 구성 및 UDP 통신](https://kimhyun2017.tistory.com/167)

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%2010.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%2010.png)

![Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%2011.png](Socket%20Programming%200569f5dce1b84298bd46bfee4fac2af7/Untitled%2011.png)

# 언리얼 엔진 플러그인

## Xsens - LiveLinkMvnPlugin

[Xsens Presents: 2019](https://www.youtube.com/watch?v=KeIM61gT5Ec)

[Xsens MVN tutorials: Preparing the MVN Link hardware](https://www.youtube.com/watch?v=laKbHOEJIoM)

분석해봅시다

에픽 게임즈 런쳐 → 언리얼엔진 → 마켓 플레이스 → LiveLinkMvnPlugin 검색 → 엔진에 설치

C++ 프로젝트 생성 → 편집 → 플러그인 → 설치됨 → LiveLinkMvnPlugin 활성화됨 체크 → 프로젝트 재시작

비주얼 스튜디오(프로젝트 생성할때 열린 창) → 솔루션 탐색기 → Engine → UE4 → Plugins → Marketplace → LiveLinkMVNPlugin의 코드들을 분석합니다.

[LiveLinkMVN 코드분석](https://www.notion.so/LiveLinkMVN-bb032e59b04c4db48db3449fea36c3b4)

LiveLinkMVN 플러그인은 컴파일러와 통신하는 Streamer, Datagram 설정, Datagram 내용 Rotate 및 scale, 리타겟팅 및 Datagram 전송으로 이루어져있다. 네트워크 부분을 살펴보면 Xsense에서 자체제작한 프로그램의 API이 Server, 이 플러그인이 Client로 되어있으며 다양한 프로그램에서도(MAYA, Unity) 사용될 수 있도록 General로 작성되어있다.


[언리얼엔진 Socket Networking](https://www.notion.so/Socket-Networking-d57f494c17bb40f1a6faefca1f26ddb8)