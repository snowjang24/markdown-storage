# Application Layer (P2P, Video streaming)

* DHT(Distributed Hash Table)

  * 주요한 키와 벨류 페어를 피어들 사이에서 나눠갖는 방식

  * 키값의 해쉬 func을 돌린것과 참여한 피어의 IP주소를 해쉬 func돌려서 나온 것과 비교하여 같으면  그 정보를 피어가 갖고 있게 함

  * 해쉬 테이블을 피어들이 나눠 갖고 있음

    ![image-20180420025303315](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420025303315.png)

    ![image-20180420025410387](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420025410387.png)

* DHT identifier

  * index숫자가 가질 수 있는 범위가 아이디가 됨

    ![image-20180420101846784](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420101846784.png)

  * 피어에게 키를 할당하는 방법

    * 만약 할당 할 때 정확히 맞는 피어가 없으면 가장 인접한 피어에 저장
    * 추가로 범위를 넘어가는 경우 다시 1로 시작

    ![image-20180420102256017](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420102256017.png)

    * 피어는 오로지 successor과 predecessor만 안다

      ![image-20180420102751076](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420102751076.png)

* Distributed Hash Table - File Sharing

  * 아래와 같이 피어의 정보와 갖고있는 파일의 정보를 담고 있는 해쉬 테이블을 나눔

    ![image-20180420102918389](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420102918389.png)

    ![image-20180420102933309](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420102933309.png)

  * 실제 찾아가는 과정

    * 임의의 피어를 알고자 할때 다음 친구에게 건너 건너 물어봄

      ![image-20180420124151514](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420124151514.png)

      ![image-20180420124227658](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420124227658.png)

    * 해당 키를 갖고있는 피어가 response를 요청 피어에게 보내줌

      ![image-20180420124304667](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420124304667.png)

      ![image-20180420141901111](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420142015199.png)

  * 실제 과정

    ![image-20180420143705766](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420143705766.png)

    * 만약 어떤 피어가 yena.mpg라는 파일을 공유하려고 할때

      ![image-20180420152115209](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420152115209.png)

  * 이런 과정을 좀 더 개선하기 위해 Shortcuts이라는 기능을 추가함

    * 반대편에 대한 포인터를 부여하여 큰 인덱스를 갈 때 쉽게 갈 수 있음

      ![image-20180420152814786](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420152814786.png)

  * $2^n$만큼 떨어진 피어들의 정보를 담은 finger table을 통해 개선

    ![image-20180420153014116](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420153014116.png)

* Peer churn

  * 피어가 나가는 경우 앞과 전을 넘겨주고 이어줌

    ![image-20180420155436713](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420155436713.png)

---

* Video streaming 

  * 특징

    * 인터넷 대역폭(bandwidth)의 주요 소비자
    * Content Distribution Network를 만들어 서버를 여러 지역에 분산함

  * 저장된 영상을 스트리밍함

  * 동영상을 받아오는데 HTTP 프로토콜을 사용함

    * Dynamic, Adaptive Streaming over HTTP : 네트워크의 트래픽에 동적으로 적응하는 HTTP

    * 서버에서는 영상을 다양한 단위로 잘라두고 인코딩 해둠, 그렇게 둔 것을 manifest file이라는 메뉴판으로 만들어서 클라이언트에게 보여줌

      ![image-20180420183919159](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420183919159.png)

    * 그 메뉴판에서 어떤 메뉴를 택하는 것은 client가 하는 것

      ![image-20180420194723881](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420194723881.png)

  * 유튜브의 업로드 다운로드 과정

    ![image-20180420194806709](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420194806709.png)

* CDN(Content Distribution Networks)

  * 처음 시작은 넷플릭스서버에서 시작하지만 파일이 어딨는지의 힌트는 사용자 가까이에 있는 카피본을 갖고있는 서버에 알려줘서 중앙서버에서 데이터를 주진 않음

    ![image-20180420195830441](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420195830441.png)

  * CDN이 컨텐츠에 접근하는 방법, closer look

    * 클라이언트가 시네마 사이트에 컨텐츠가 있다는 사실을 인지

      ![image-20180420200321528](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420200321528.png)

    * Netcinema.com의 주소를 알아내기 위해 local DNS서버에 물어봄

      ![image-20180420201657057](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420201657057.png)

    * 결국 netcinema의 authoratative DNS에 물어봄

      ![image-20180420201806201](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420201806201.png)

    * 우리가 아는 DNS와는 다르게 IP를 보고 클라이언트와 다른 클라이언트와 가까운 DNS를 확인해서 로컬 DNS에 알려주고, 이를 클라이언트에게 보내줌

      ![image-20180420201923444](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420201923444.png)

    * 가장 적절한 사이트에서 데이터를 받음
      ![image-20180420202209525](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420202209525.png)

    * Netflix의 예

      ![image-20180420202525555](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420202525555.png)

  **Application layer 키워드**

  > * CDN를 위해 DNS를 변경한것, DASH, DHT, p2p가 clientserver보다 중요한 이유 
  > * DNS는 쿼리 어떻게 처리하는지가 중요, 구조
  > * 프로토콜끼리 서로 연동할 때 어떻게 동작하는가 이메일 - DNS / HTTP - DNS 
  > * 캐시 중요, 쿠키는 상식으로 알고 있기, persistent connection, pipline 왜좋아지는지 뭐가 좋아하는지
  > * principle과 SMTP는 상식

  ​

  ​