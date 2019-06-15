# Introduction(Access Network, Core Network)

> *Architecture가 핵심*

* 인터넷 = 구름, 구름의 가장자리(엣지) = 단말기(컴퓨터, 폰)
  * 단말들이 인터넷이라는 큰 네트워크에 붙어야함
  * Access network를 이용하여 단말을 네트워크에 붙임
  * 엣지에는 단말이 존재, 단말들은 AN으로 네트워크 코어에 붙임
  * 네트워크 코어의 종류는 스위치 라우터가 있음
  * 네트워크 코어는 고속도로로 길을 제공, 엑세스 네트워크는 진출로

![image-20180413025130229](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413025130229.png)

* 엑세스 네트워크의 종류는 Residential access N(집에 인터넷 서비스 제공), Institutional access N(학교나 회사에 인터넷 서비스 제공), Mobile access N(휴대폰 모바일 단말에 인터넷 서비스 제공)
  * 다양한 매체를 사용하기 때문에 단위 시간당 전송 단위가 다름
  * 무선 엑세스 네트워크에서 아래는 4G나 3G같은 광대역망, 집에서 쓰는 AP 공유기같은 것은 좀 더 간단한 연결을 통해 전달

![image-20180413025701708](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413025701708.png)

---

* 네트워크 코어

![image-20180413030030411](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413030030411.png)

* 네트워크 코어 내부 : 실제 여러 사업자들의 라우터를 거쳐서 이동

![image-20180413030046156](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413030046156.png)

* 패킷 스위칭 : 데이터를 패킷이라는 작은 단위로 조각을 내어 엑세스 네트워크를 거쳐 라우터로 넘기면 패킷에 적혀있는 목적지로 계속 넘겨 목적지 까지 배달 하는 것

  * ![image-20180413030541996](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413030541996.png)

    많은 데이터를 보내고 싶지만 그건 불가능

  * ![image-20180413030550021](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413030550021.png)

    전송 가능한 양만큼 데이터를 패킷단위로 쪼갬

  *  ![image-20180413030559287](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413030559287.png)

    그다음 store and forward함 쪼개진 패킷을 하나씩 전송하는게 아니라, 그 패킷을 라우터에서 모두 모은 다음 다시 전송

  * ![image-20180413031107133](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413031107133.png)

* 패킷 스위칭 단점 : Queueing delay, loss

  * 단위 시간당 내보낼 수 있는 양과 받아 들일 수 있는 양에 차이가 생김, 지체(delay)가 생김

  ![image-20180413031420188](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413031420188.png)

  *  컴퓨터는 제한된 리소스를 가짐, 따라서 버퍼(메모리)가 꽉차면 그 이후의 것들은 손실(loss)됨

  ![image-20180413031759093](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413031759093.png)

* 네트워크 코어들의 주된 기능

  * Forwarding : 라우터 input을 적절한 라우터 output으로 패킷을 넘기는것, 포워딩 테이블을 갖음

  ![image-20180413032046436](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413032046436.png)

  ![image-20180413032115289](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413032115289.png)

  * Routing : 포워딩 테이블을 만들기 위한 약속을 라우팅 알고리즘이라고 부름

  ![image-20180413032159410](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413032159410.png)

  * 각 라우터들은 포워딩 테이블을 가짐, 각 포워딩 테이블은 다 다름, 이는 각 라우터마다 연결이 다르기 때문, 헤더 벨류와 라우팅 알고리즘은 모두 같아야 함

  ![image-20180413032248450](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413032248450.png)

* Circuit Switching
  * 패킷 스위칭 이전 모델
  * 회로를 따라서 신호가 휙하고 흘러가게 만들어진 것, 초기에 전화망을 구성할 때 사용됨
  * 한정된 망에서 자원을 독점해버려서 다른 사용자가 자원을 쓰고싶더라도 쓸 수 없게 되어버리기 때문에 불편

  ![image-20180413032747474](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413032747474.png)

  * 서킷스위칭 실현 방법 : FDM(Frequency division multiplexing), TDM(Time division multiplexing)

  ![image-20180413033651287](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413033651287.png)

  * 서킷스위칭 대표 예 : 전화

  ![image-20180413033713892](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413033713892.png)

  ![image-20180413033807911](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413033807911.png)

  ![image-20180413033815733](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413033815733.png)

  ​	한 회선이 점유되면 다른데서는 접근을 못함

  ![image-20180413033854248](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413033854248.png)

  ​	자원이 회색처럼 놀게됨

  * 패킷스위칭

  ![image-20180413034005561](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034005561.png)

  중앙에 라우터가 각 목적지에 맞게 패킷을 보냄

  ![image-20180413034038795](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034038795.png)

  ![image-20180413034110096](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034110096.png)

  ​

* 인터넷 구조 : network of networks

![image-20180413034844307](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034844307.png)

![image-20180413034852777](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034852777.png)

![image-20180413034900243](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034900243.png)

![image-20180413034955575](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034955575.png)

* 인터넷은 계층 구조를 가지고 있다

![image-20180413034930786](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413034930786.png)

* 딜레이 발생 이유

  * 데이터가 나가는 것과 들어오는 양이 비슷하면 지연시간이 오히려 지연시간이 길어짐 이는 평균적인 시간으로 계산하기 때문

  ![image-20180413035241583](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180413035241583.png)

  ​

