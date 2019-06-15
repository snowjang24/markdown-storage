# Application Layer (DNS, P2P)

* DNS에 실제 저장되는 데이터 베이스 기록

  * 각 타입에 맞는 name과 value가 저장됨

    ![image-20180419225626941](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419225626941.png)

* DNS protocol, message

  * 쿼리 메세지(query와 reply 모두 형식이 같음)

    * Identification은 query와 reply를 대응시키기 위해 랜덤한 숫자를 부여
    * 깃발은 0과 1을 갖음, query인지 reply 인지 구분, recursive query를 해줄 수 있는지 없는지, 대답이 authoritative 한지 안한지(local dns가 응답해주는데 캐시에 있는걸 알려줄 때 authoritative 쓰임)

    ![image-20180419225959388](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419225959388.png)

    * Query

    ![image-20180419230403886](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230403886.png)

    * 응답

    ![image-20180419230439115](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230439115.png)

    ![image-20180419230533831](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230533831.png)

  * nslookup 

    ![image-20180419230702847](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230702847.png)

    ![image-20180419230715018](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230715018.png)

    AAAA는 IPv6주소

    ![image-20180419230724060](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230724060.png)

    ![image-20180419230753746](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230753746.png)

  * type: PTR

    * IP주소가 어느 도메인에 속해있는지 궁금할 때 사용됨

    * 아래처럼 아이피 주소를 뒤집어서 물어봐야 함

      ![image-20180419230916071](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419230916071.png)

* DNS에 기록을 넣는 방법(상식적으로 알고 있으면 됨)

  * .com DNS의 TLD서버에 새로운 내용을 저장을 함
    ![image-20180419231319577](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419231319577.png)

* 웹이 로딩되는 과정

  * 최악의 상황

    ![image-20180419231626021](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419231626021.png)

  * 최선의 상황

    ![image-20180419231807973](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419231807973.png)

---

* P2P : 모든 단말들이 동등한 자격으로 상호작용함

* 이전 세대 핵심 : 한 피어가 나에게 서비스를 해준 다는 점이 핵심

  * Napster : 중앙화된 디렉토리

    * 중앙에서 누가 어떤 파일을 갖고있는 지의 정보를 모두 갖고 있음

      ![image-20180419232111798](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419232111798.png)

  * Gnutella : 중앙X, 이웃

    * 중앙은 아무것도 모르고 내 주변의 이웃에 대해서만 정보를 가짐

    * 단점 : 쿼리가 기하급수적으로 커져서 퍼짐, 쿼리에 갯수를 제한을 둬서 해결함

      ![image-20180419232518274](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419232518274.png)

  * KaZaA

    * 그루핑을 하고 그 그룹의 리더를 뽑아서 클러스터 내의 피어들이 어떤 컨텐츠를 갖고 있는지의 정보를 갖고 있음

      ![image-20180419232646192](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419232646192.png)

* P2P와 Client-server의 차이(File distribution)

  ![image-20180419235855021](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180419235855021.png)

  * Client-server

    * 서버의 업로드 능력도 전체 시간을 좌우하지만 아주 느린 네트워크도 전체 시간을 좌우함

      ![image-20180420000040903](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420000152324.png)

  * P2P

    * 네트워크에는 N*Fbits만큼의 데이터가 업로드 되어야함(max의 마지막 요소 )

      ![image-20180420000824581](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420000824581.png)

  * 클라이언트의 증가에 따른 분산 시간

    ![image-20180420000930423](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420000930423.png)

* P2P : BitTorrent

  * 파일을 256KB chunk단위로 짜름

  * tracker는 누가 무엇을 갖고 있는지에 대한 정보를 갖고 있음

    ![image-20180420004729230](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420004729230.png)

  * 트래커는 누가 어떤 조각을 갖고있는지를 알고 있음

    ![image-20180420004757263](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420004757263.png)

    * 누가 이거 갖고있어? 라고 물어보면 대답해줌

      ![image-20180420004857044](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420004857044.png)

    * 파편적으로 받음

      ![image-20180420004916217](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420004916217.png)

    * 비트 토렌트는 받기만하면 안됨, 받음과 동시에 도움을 준 피어들 중에서 피어들이 갖지 않은 조각들을 줌(tit-for-tat)

      ![image-20180420005011981](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420005011981.png)

* Hash table

  * 어떤 텍스트를 넣고 그것을 인덱스로 하여 테이블에서 찾음

    ![image-20180420005141691](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420005141691.png)

    ​