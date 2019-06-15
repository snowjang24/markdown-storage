# Application Layer (Web, Domain name system)

* DNS(Domain Name System or Service)

  * System으로 쓰일 때(훨씬 더 큰 개념) : 도메인 네임을 정할 때 원칙, 도메인 네임 서비스를 가능하게 하는 서버들의 구조
  * Service로 쓰일 때 : 메일을 보낼 때 주소값을 알아내는 것
  * 글자로 된 이름과 숫자 사이의 매핑 기능을 해주는 것이 service 그걸 가능하게 하는 것이 system

* Domain name rule

  ![image-20180419011225386](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419011225386.png)

  * 도메인 이름은 영어, 하이픈, 숫자로 이루어져 있음(기본 원칙)

* DNS services가 하는 일

  * Hostname에서 IP주소를 불러오는 것
  * 긴 호스트를 기억하지 않고, 짧은 이름을 매핑시켜 줌 
  * 어느 메일서버가 메일이 리퀘스트를 받아야하는 지 찾아줌
  * 동시 접속자가 많으면, 여러 호스트 컴퓨터 중 어떤 사람은 A호스트 컴퓨터에 다른 사람은 B호스트 컴퓨터에 이런식으로 
  * 아래가 진짜 호스트 컴퓨터에 부여된 이름

  ![image-20180419012451757](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419012451757.png)

  한국은 아직 IPv6가 많이 활성화 되어있지 않아 IPv4를 씀

  ![image-20180419012759171](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419012759171.png)

  * 이러한 일은 중앙에 있는 서버가 하지 않음
    * 딜레이가 엄청 발생하기 때문(서버에서 멀어 질 수록 프로파게이션 딜레이에 의해)
    * 하나의 중앙 DNS서버를 구축해서 할 경우 모든 일을 처리하기 힘듦, 그래서 나라별 필요한 곳에 가까운 곳에 DNS서버가 존재

* Hierarchical 도메인 이름 구조

  * 도메인 이름은 단계로 다양하게 존재
  * 맨 위는 국가 단위
  * 레벨에 대한 제한은 없음 레벨은 마음대로 만들 수 있음

  ![image-20180419013827418](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419013827418.png)

  * DNS도 아래와 같은 계층 구조를 가짐, 앞에 설명한 것처럼 중앙의 서버에서 모두 처리하지 않음

    * 루트 DNS server은 탑 레벨 단위의 도메인이 어떤게 있고, 각 도메인을 관리하는 네임 서버가 뭐가 있는지에 대한 정보를 담고 있음
    * 각 DNS server는 다음 단계의 정보를 담고 있음

    ![image-20180419014836820](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419014836820.png)

    * 아래는 주소를 입력하였을 때 이뤄지는 일의 일련의 과정

    ![image-20180419014914805](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419014914805.png)

    * 루트 서버는 하나만 존재하는 것이 아니라 여러개의 카피본이 존재함 (13개의 루트 서버 존재), 하지만 이래도 부족하기 때문에 카피본의 카피본이 존재

    ![image-20180419015013982](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419015013982.png)

    * Top level Domain(TLD)
      ![image-20180419015254006](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419015254006.png)

    * Authoritative DNS

      ![image-20180419015307147](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419015307147.png)

* Local DNS name Server

  * 여기 아래에서 임의로 설정해주는 DNS서버가 Local DNS 서버

    * 프로시 서버처럼, 사용자의 처음 요청을 받아서 처리해주는 것이 local DNS 서버

    * 매번 루트에 물어보면 복잡하기 때문에, local DNS서버가 캐시를 관리하여 사용자가 자주 물어보는 이름과 주소사이의 매핑 정보를 저장해둠

    ![image-20180419015548498](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419015548498.png)

    * 여기서 권한 없는 응답은, 이미 캐시에 있어 Local DNS 서버에서 처리를 하겠다는 뜻

    ![image-20180419015548498](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419015548498.png)

  *  Gaia.cs.umas.edu라는 컴퓨터에 cis.poly.edu를 사용하는 사용자가 접속하고 싶을 때(캐시에 없을때 위로 쭉쭉 올라감, root에 도달하면 주소를 기반으로 다시 아래로 내려감)

    * 이러한 과정을 Iterative query라고 함(같은 질문을 계속 반복 하는 것)

  ![image-20180419020414177](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419020414177.png)

  * 이러한 과정은 local DNS server가 버거워함 이런 피로를 덜어주기 위한 방법이 Recursive query

    ![image-20180419020614565](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419020614565.png)

  * 부분적으로 recursive와 iterative가 혼재되어 있을 수도 있음, DNS 서버마다 다름

  * 웹 캐시와 같은 문제가 발생하나, expired time이 존재하여 유효기간이 지난 캐시는 자동으로 삭제

