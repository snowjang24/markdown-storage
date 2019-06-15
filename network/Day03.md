# Application Layer (Principles, E-mail)

> 

* OSI와 TCP/IP 비교

  ![image-20180413100250549](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413100250549.png)

* OSI 프로토콜의 철학은 많이 참고가 됨 그냥 이런게 있구나 하면 됨

  ![image-20180413100402235](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413100402235.png)

* TCP/IP프로토콜 

  ![image-20180413100422698](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413100422698.png)

  * 각 임플리멘테이션을 사용한다 : 제공된 API를 사용하여 임플리멘테이션을 콜하여 사용함

* 실제 데이터가 전달되는 과정

  * 계층간 주고받는 정보 = 헤더

  ![image-20180413101014926](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413101014926.png)

![image-20180413125544609](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413125544609.png)

* 애플리케이션 프로토콜 구현에는 두가지 컨셉이 있음

  * Client-server paradigm
  * Peer-to-peer paradigm

*  네트워크 앱 : 원격에 떨어져 있는 end 시스템에서 서로 상호작용하며 돌아가는 어플리케이션ex) 웹서버, 브라우저

  ![image-20180413141934322](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413141934322.png)

* Client-server : 서비스를 제공하는 녀석에게 서비스를 요청하는 클라이언트가 붙는 구조

  * 서버 : 항상 켜져있어야함, IP adress는 항상 일정해야함, 엄청난 데이터 센터가 필요함

* Peer-to-peer : 어플리케이션들이 다 동등한 자격으로 서로 상호작용하는 구조, 막상 구조를 까보면 결국 Client-server구조

  * 서버가 늘 켜져있지 않음
  * 피어들이 모두 책임감있게 서버를 켜두진 않음
  * 서비스를 사용하는 사용자 수를 늘리고 싶으면 새로운 피어가 등장하는 것 만으로도 서비스 제공가능 용량이 늘어남

![image-20180413142316900](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413142316900.png)

* 프로그램과 프로세스의 차이

  * 프로그램 : 아직 런하지 않은 코드
  * 프로세스 : 프로그램 코드가 CPU에 로드가 되고 실제 시피유가 프로그램을 실행하고 있는 것

* Processes communicating

  * client process : 커뮤니케이션을 요청하는 시점에서 시작됨
  * server process : 늘 먼저 On 된 상태에서 wait함

* 소켓(Sockets)

  * 하위에 구현된 층들을 이용하게 하려고 어플리케이션에게 제공하는 API를 Socket API이라 부름

  ![image-20180413191859082](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413191859082.png)

  * 목적지를 식별하는 방법은 IP와 port 로 구분함, ip주소는 globaly unique함, port 넘버는 각 컴퓨터 안에 있는 프로세스를 식별함
  * 약속 이 있음, 웹서버(HTTP server) 80, 메일서버 25는 고정(~~중간고사 뽀나스 문제로 좋음~~)

* 어플리케이션 레이어 프로토콜 = 규약

  * 어떤 식의 response와 request가 존재하고, 그 request에는 어떤 field들, 정보들이 들어가야하고, 각 각의 field에 적혀있는 값들은 어떤 의미를 가지는 것이고, 이러한 값이 왔을때 클라이언트나 서버는 어떻게 반응해야하는가 를 적은 규약, 제공하는 기능에 따라 프로토콜의 크기가 다름![image-20180413202812813](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413202812813.png)

* http같은 open protocol도 있고, skype처럼 회사끼리만 공유하는 protocol도 있음

* Data loss나 Throughput이나 Time sensitive는 각각의 어플리케이션마다 특징이 다름 ex) file transfer은 data loss이 있어서는 안되고 Throughput은 탄력적이며 time sesitive에 그렇게 민감하지 않음

![image-20180413203905502](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413203905502.png)

* 트랜스포트 프로토콜 서비스
  * TCP는 파일 교환, 웹페이지 다운 등 content가 온전히 배달되는 것들을 책임지는 기능들을 제공, 완벽한 전송
  * UDP는 시간안에 오는게 중요하지 모두가 다 도착하는게 중요한게 아닐때 사용, 보내기만 하면 되는 전송
*  SMTP는 요새 다 웹메일로 써서 지금은 의미가 잘 없음
* 메일은 유저, 메일서버, 메일을 전송하는 프로토콜 SMTP(Simple Mail Transfer Protocol), Mail access protocol으로 구성되어 있음

![image-20180413205610493](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413205610493.png)

* 메일은 중간에 글자 하나 날라가면 다른 내용이 되기 때문에 TCP를 사용
* 네이버든 구글이든 모든 메일 서비스를 제공하는 서버는 port 25로 보내면 SMTP서버가 받음
* SMTP프로토콜이 중요하다기 보단, 처음 메일을 만들 때는 영어로만 쓰다보니깐 ASCII코드로만 구성되었었음, 하지만 요즘은 Multipurpose internet mail extention으로 바뀜
* 막상 전송될때는 ASCII코드로 다시 바뀌어서 전송됨

![image-20180413210226648](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413210226648.png)

* 가끔 그래서 첨부파일의 용량 제한이 5MB인데 3MB를 보냈음에도 용량이 초과함
  * 바이너리를 아스키로 바꾸는 과정에서 파일이 1.5배까지 커지기도 함
  * 메일을 보내는 메카니즘은 7비트, 우리가 보내는 데이터는 8비트라 컨버젼시 용량이 초과