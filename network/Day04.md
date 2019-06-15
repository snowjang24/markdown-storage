#Application Layer (Web, HTTP)

* Web페이지는 기본적으로 HTML 파일임,

* HTML문서에서 어떤걸 가져와라 라고 적혀있는 대로 실행할 때 URL(Uniform Resource Locater)을 따라서 가져옴

  * http프로토컬을 씀

  ![image-20180413224458729](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413224458729.png)

* HTML(Hypertext Markup Language)

![image-20180413224631696](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413224631696.png)



* HTTP(HyperText Transfer Protocol)

  * HTML을 교환하기 위한 프로토콜

  * client : 브라우저

  * server : 웹서버

  * 각각에서 개발자가 다르지만 HTTP 를 쓴게 같아서 상호 작용하는데 아무 문제가 없음

    ![image-20180413224953223](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413224953223.png)

  * HTTP는 TCP를 사용함, file의 컨텐트를 하나도 잃어버려서는 안됨

  * HTTP에서 TCP에 요청, TCP는 서버에 요청하고 연결을 끊는 순으로 동작

  * HTTP는 stateless함(따라서 단순), 과거에 뭘했는지를 기억하지 않음

  * state를 유지하는 프로토콜은 복잡함(SMTP는 stateful함)

* HTTP의 종류

  * Non-persistent HTTP : 한 번 연결을 맺은 다음 오브젝트를 하나 받고 연결 끊음, 해당 사이트로부터 여러개의 이미지를 받아야하면 여러번 요청을 하거나 한번에 여러개 연결을 만들어서 받음
  * Persistent HTTP : 한 번 연결을 맺은다음에 여러개의 오브젝트를 연달아서 요청해서 받음


* 요즘 웹페이지가 페이지를 받아와서 그려주는데 걸리는 시간

  * 다양한 JS나 CSS, 이미지등을 불러오느라 페이지 불러오는데 시간이 오래 걸림

  ![image-20180413230119969](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413230119969.png)

* Non-persistent HTTP: response time

  * RTT(Round Trip Time) : 준비되었나요? 준비되었어요! 라고 요청이 돌아오기 까지의 시간, One way가아니고 왔다가 돌아오는데 걸리는 시간

  ![image-20180413230658344](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413230658344.png)

  * RTT를 줄이는게 웹페이지 로드 시간을 줄임
  * 만약 persistent 이면 한번의 RTT만으로 오브젝트들을 받을 수 있어서 빠름, 요즘은 다 그래서 persistent를 씀

  ![image-20180413230831218](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413230831218.png)

* HTTP로 요청하는 request 메세지

  ![image-20180418123848016](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418123848016.png)

  ![image-20180418125150580](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418125150580.png)

* Uploading form input

  * 주로는 GET 메서드를 자주 씀(서버에 업로드하는 컨텐트의 양이 적을 때 사용)

    ![image-20180418131113557](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418131113557.png)

  * POST 메서드 : 웹 페이지 중 input form 을 포함할 때가 있음(회원가입 할 때), 입력해야하는 내용이 많을 때 POST를 사용

    * 바디에 닮긴 모든 내용을 서버에 업로드함

    ![image-20180418130803402](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418130803402.png)


* 메서드 타입

  * PUT은 지원안함(보안상의 이유로), 아래의 메서드 외에도 다양한 메서드가 존재

  ![image-20180418131439335](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418131439335.png)

* HTTP로 응답하는 response 메세지

  ![image-20180418132259179](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418132259179.png)

* 서버 응답 상태 종류(외울 필요는 없음)

  * 200 : OK(연결 성공)
  * 301 : 오브젝트가 옮겨갔다는 뜻, 잠시 다른 URL로 옮겨갔으니 필요하면 새로운 Location에 있는걸 가져가라는 것
  * 400 : 잘못된 사용자 요청, request메세지가 잘못 작성된거 같다는 것
  * 404 : 없는 오브젝트를 요청을 했을때 
  * 505 : 서버문제로 실패, 버젼이 안맞거나 서버가 죽거나 했을 때

  ![image-20180418132802098](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418132802098.png)

* Cookies

  * 사용자에게 식별 번호를 부여, 추적하는 용도로 쓰임

  * 순서

    * 아마존 페이지에 접속, 사용자에게 번호표 부여하여 아마존 데이터 베이스에 저장

      ![image-20180418133611460](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418133611460.png)

    * 그거에 대한 응답으로 부여한 번호표(쿠키)를 알려줌, set-cookie는 헤더

    ![image-20180418133633436](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418133633436.png)

    * HTTP request를 요청할 때 헤더에 쿠키 번호를 함께 보냄, 서버는 쿠키를 통해 저장된 사용자의 행적에 따라 해당하는 서비스 제공

    ![image-20180418133922581](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418133922581.png)

    * 다음에 접속해도 맞춤형 서비스 제공

    ![image-20180418133940896](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418133940896.png)

* Proxy server(웹 캐시)

  * 과정

    * 처음에는 원 서버에서 데이터를 받아와 프록시에 저장함

    ![image-20180418134517476](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418134517476.png)

    * 그 다음 같은 요청을 받으면 원 서버에 갈 필요 없이 프록시에서 응답을 보내줌

    ![image-20180418134543820](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418134543820.png)

  * 단점 : 보안이 문제가됨, 가짜 컨텐츠를 집어 넣을 수 있음, 안씀에도 불구하고 컨텐츠를 계속 지니고 있어야 하거나, 컨텐츠가 자주 바뀔 경우 문제 발생

  * 그렇다 할지라도 장점이 더 클 때 사용됨

  * 자료를 보내기 전에 원 서버에 다시 자료가 바꼈는지 여부를 물어보고 보냄

* 캐싱

  * 엑세스 링크와 사용자의 인터넷 속도차이가 있어서 요청을 보내는데 문제가 없으나 서버에서 정보를 보낼 때 병목현상으로 문제가 발생, Queing delay가 많이 발생

  ![image-20180418232152801](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418232152801.png)

  * 엑세스 링크를 향상 시킴

  ![image-20180418232449735](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418232449735.png)

  * 서버를 좋은걸 사서 그걸 프록시 서버로 이용하여 캐싱함

  ![image-20180418232348913](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418232348913.png)

  웹캐시가 갖고 있는 효과가 중요함, 하지만 사용자의 요청이 다다를 때는 이 서버가 무의미함

  ![image-20180418232508492](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180418232508492.png)

  ​