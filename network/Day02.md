# Introduction(Nodal Delay, Protocal Layers)

> 핵심 : 지연 시간과 프로토콜 레이어

* 노달 딜레이 : A에서 목표 라우터 까지 가는데 발생하는 총 딜레이

  ![image-20180413041142943](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413041142943.png)

  * 프로세싱 딜레이 : 링크를 따라오는 동안 문제가 없었나 체크, 목적지를 보고 어디로 내보낼지 결정하느라 딜레이가 생김

  ![image-20180413035740029](/Users/soonhojang/Documents/%E1%84%86%E1%85%A1%E1%84%8F%E1%85%B3%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB/%E1%84%82%E1%85%A6%E1%84%90%E1%85%B3%E1%84%8B%E1%85%AF%E1%84%8F%E1%85%B3/assets/image-20180413035740029.png)

  - 큐잉 딜레이 : 큐에서 기다리는 시간에 의해 발생하는 딜레이

  ![image-20180413035830283](/Users/soonhojang/Documents/%E1%84%86%E1%85%A1%E1%84%8F%E1%85%B3%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB/%E1%84%82%E1%85%A6%E1%84%90%E1%85%B3%E1%84%8B%E1%85%AF%E1%84%8F%E1%85%B3/assets/image-20180413035830283.png)

  - 트랜스미션 딜레이 : 네트워크 카드로부터 케이블로 신호가 변조되어서 나갈때 걸리는 딜레이,  각 매체마다 bandwith가 정해져 있는데 이 값은 불변이고, 패킷의 길이가 변함![image-20180413041642722](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413041642722.png)


  - 프로파게이션 딜레이 : 물리적 매체를 따라 나가는데 걸리는 딜레이, 값이 너무 작아서 영향 X

  ![image-20180413041848052](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413041848052.png)

  ![image-20180413042323896](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413042323896.png)

  * 이 넷 중 가장 가변적인 값은 큐잉 딜레이, 큐에 몇개가 대기하냐에 따라 값이 가변적임 

* 큐잉 딜레이

  * R : 단위시간당 처리할 수 있는 데이터 양

    L : 패킷의 크기

    a : 단위시간당 도착하는 패킷의 개수(진입하는 트래픽의 양)

  ![image-20180413042355095](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413042355095.png)

  * 들어오는 속도와 나가는 속도가 평균값이라고 하면 가장자리에 느리고 빠른것들의 영향을 받아 딜레이가 늘어나는 속도가 지수적으로 변하게 됨

* 패킷 로스

  * 큐의 버퍼는 한정적인 수용력을 지녀 큐가 꽉차면 그 뒤에 오는 패킷은 버려짐

  ![image-20180413042652018](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413042652018.png)

  * 라우터에는 패킷을 다시 보내달라는 것을 요청할 기능이 없기 때문에 end에서 데이터가 제대로 갔는지 확인하는 요청을 한 뒤 다시 재전송

* Throughput : sender와 reciever사이에서 실제로 얼마만큼의 데이터가 배달 되었는의 비율, band width(최대 전송 용적)와는 다름

  ![image-20180413043646512](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413043646512.png)

  ![image-20180413044001185](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413044001185.png)

  * 차이에 의해 bottleneck link가 생김

  ![image-20180413044046001](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413044046001.png)

  * Rc와 Rs와 R/10중 가장 작은 값이 성능을 결정함, 코어네트워크보단 엑세스 네트워크의 속도가 전체 성능을 좌우함

  ![image-20180413044342849](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413044342849.png)

  ​

* End-to-end delay 문제, Nodal delay 하나가 중요한게 아니라 노달 딜레이를 복합적으로 계산해서 전체 클라이언트와 서버사이에서 얼마나 시간이 걸리는지가 중요함

![image-20180413044504636](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413044504636.png)

>  di(distance), si(propagation speed), Ri(transmition rate)

![image-20180413045017761](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413045017761.png)

* Internet Protocol layers : 단일로는 처리가 어려워 인터넷 프로토콜은 계층적으로 나뉘어짐

  ![image-20180413045215647](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413045215647.png)

  * 어플리케이션 : 서비스들 자체만을 위해 개발된 프로토콜
  * 트랜스포트 : end에서 end 사이에 데이터가 전송되는데, 전송을 어떻게 정확하게 전달할지를 정의하는 역할을 함
  * 네트워크 : 코어 네트워크 상에서 요청을 보낸 컴퓨터와 요청을 처리해야할 컴퓨터에게 정확하게 배달하기 위해 코어 라우터가 해야할 것들을 정의하는 역할을 함
  * 링크 : 물리적으로 직접 연결된 장치들 사이에 신호가 온전하게 잘 배달 될 수 있도록 책임지는 역할을 함
  * 물리 : 매체가 무선일때, 유선일 때 신호를 어떻게 변조할지의 약속들을 정의하는 역할을 함 

* ISO에서 정의한 OSI 7Layer이 원조이지만 인터넷(TCP/IP)이 돌아가게 하는 프로토콜들을 배치하다보니 원조에 부합하지 않아 나온 것이 5 protocol layers

  ![image-20180413050006562](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413050006562.png)

  * 프레젠테이션 : 데이터를 표현하는 방법(형식)을 정의하는 역할을 함
  * 세션 : 연결을 만드는 과정을 정의하는 역할을 함

* 계층별 배워야할 것

![image-20180413050402548](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413050402548.png)

​	SCTP, DCCP는 다루지 않음, PIM-SM, DVMRP, IGMP는 다루지 않음, physical은 컴통에서 다룸

* Layering의 필요성 : 각 역할에 대해서만 알고있으면 되는거고, 상세 내용, 이유에 대해서는 관심을 가지지 않음 이를 통해 

   * 약속은 동등한 레벨끼리만 정의, 서로 다른 레벨 사이에서는 하위 레벨이 제공하는 서비스를 사용하기만 하면 됨, 다른 레벨에 요구하지 X

   ![image-20180413050819908](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413050819908.png)

![image-20180413051118494](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413051118494.png)


* Encapsulation


  * 각 계층의 역할에 해당하는 정보들을 메세지에 추가로 붙임

  ![image-20180413051645783](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413051645783.png)

  * 스위치를 통해 라우터로 가면 하나하나 다시 메세지를 벗김

  ![image-20180413051750529](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413051750529.png)

  ![image-20180413051822449](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413051822449.png)

  ​

  ![image-20180413051916601](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413051916601.png)

  ![image-20180413051927739](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413051927739.png)

  * 다시 아래에서부터 위로 벗겨가면서 처리함

![image-20180413052003232](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052003232.png)

* layer간의 intersaction

  * 어플리케이션에서는 우리가 보낸 메세지를 잘라서 보냄

  ![image-20180413052347591](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052347591.png)

  * 트랜스포트에서는 각 잘려진 메세지에 순서를 매김, 그리고 어플리케이션 어디가 어디에게 보내는지를 기재

  ![image-20180413052424996](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052424996.png)

  * 네트워크에서는 어느컴퓨터가 어느컴퓨터에게 보내는지를 기재

  ![image-20180413052633357](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052633357.png)

  * 링크에서는 R1으로 넘겨라고 적어줌

  ![image-20180413052715297](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052715297.png)

  * 피지컬에서는 신호가 변조되어 넘어감

  ![image-20180413052752550](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052752550.png)

  * R1피지컬에서 신호를 조합해서 받은 다음에 A,R1데이터를 삭제함

  ![image-20180413052827316](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052827316.png)

  ![image-20180413052901489](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052901489.png)

  * 링크에서 다시 R1 R2를 기재해줌

  ![image-20180413052945198](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413052945198.png)

  * 다시 R2로 전송

  ![image-20180413053002691](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413053002691.png)

  * 중간생략...
  * 중간에 라우터에서 손실나서 3번이 오지 않음

  ![image-20180413053137935](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413053137935.png)

  * 이때는 4번을 잠시 가지고 있다가 3번이 올때 까지 기다렸다가 데이터가 다 오면 묶어서 통합해서 저장함

  ![image-20180413053105866](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413053105866.png)