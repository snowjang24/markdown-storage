# Transport Layer (GBN, Selective Repeat, Congestion Control)

* Principles of Congestion control

  * Congestion : 네트워크에 연결되어 있는 여러 컴퓨터가 존재하는데 너무 많은 데이터를 보내서 중간에 있는 라우터가 이를 처리 할 수 있는 범위를 벗어나는 상황을 뜻함

  * Congestion control : end system에서 너무 많은 데이터를 보내서 라우터의 큐가 꽉차는 상황이 발생하지 않게 하는 것

    * 문제는 NL에서 발생하고, 문제 해결은 TL에서 해야함
    * 이를 해결하기 위해서는 원인과 해결자가 다른 layer에 해당하기 때문에 해결이 어려움

  * Flow control : sender가 보내는 데이터로 인해 receiver가 저장할 수 있는 공간을 초과해서 보내지 않게 조절하는 것

  * 발생하는 문제

    ![image-20180421054836274](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421054836274.png)

  *  Causes of congestion: 시나리오 1

    * 두 연결이 하나의 라우터를 공유

    * buffer가 무한대

    * 나가는 링크의 데이터의 수용력은 R

    * 람다in : sender application이 단위 시간당 보내는 데이터의 양

    * 람다out : receiver application이 단위 시간당 수신하는 데이터의 양

      ![image-20180421055331331](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421055331331.png)

  * Causes of congestion: 시나리오 2(1)

    * 한개의 라우터, 유한한 buffer
    * 운이 좋아서 안버려지면 같고, 버려지는게 생기면 람다 프라임 인이 람다 인보다 큼
    * TL에서 보내는 양이 증가하더라도 람다 out에서 받는 양은 변하지 않음

    ![image-20180421055653271](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421055653271.png)

  * Causes of congestion: 시나리오 2(2)

    * sender의 눈치가 빨라서 buffer에 공간이 생길 때만 보냄

    * 이런 경우 loss가 발생X

    * 람다in 과 람다 프라임 in 이 같음

      ![image-20180421060347171](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421060347171.png)

  * Causes of congestion: 시나리오 2(3)

    * 라우터에서 패킷이 버려질때가 확인 될 때만 패킷이 재전송 되는 상황

    * receiver입장에서는 중복되는 것 없이 늘 새로운 것 만 옴

    * 일을 많이 했지만, 실제로는 일을 많이 한것은 아님

      ![image-20180421060936657](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421060936657.png)

  * Causes of congestion: 시나리오 2'(2) 현실

    * 타이머가 짧게 설정되어 잘 배달이 되었지만 또 보내는 상황들 발생

    * sender가 불필요한 것 까지 보내게 되니깐 이번엔 중복된 것 까지 발생함

      ![image-20180421061446549](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421061446549.png)

  * Causes of congestion: 시나리오 3

    * 한 sender가 열심히 한 덕분에 다른 sender에게 피해가 가는 경우

    * A가 보낸 데이터와 D가 보낸 데이터가 한 라우터에서 Queue에 쌓임, 이때 D 가 보내는 패킷이 라우터에 도착했지만 A가 너무 열일해서 D의 패킷이 버려짐 

      ![image-20180421062216099](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421062216099.png)

      ![image-20180421062128684](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421062128684.png)

  * Congestion control하는 두종류의 방법

    ![image-20180421062303680](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421062303680.png)

