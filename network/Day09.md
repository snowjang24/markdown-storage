# Transport layer (Reliable data transfer - Part 2)

* Window size문제 (1000bits -> 1000bytes)

  ![image-20180421042216655](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421042216655.png)

  ![image-20180421042510390](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421042510390.png)

* Piplined protocols

  * Go-back-N

    * 앞의 타이머가 expired 되면 파란색 앞에, 윈도우 안, 지금까지 보냈던 모든 패킷들을 다시 재전송 함 

      ![image-20180421043952079](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421043952079.png)

    * 근데 이렇게 하면 초록색에 already acked인데? 라는 의문이 생김, 하지만 reciver입장에서야 몇개의 패킷이 왔고를 아는데 sender입장에서는 몇개의 패킷이 잘 갔는지 모름

    * sender FSM

      * 초기 컨디션

        ![image-20180421044401039](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421044437710.png)

      * Application Layer가 rdt_send를 요청함

        ![image-20180421044623003](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421044623003.png)

      * NL가 TL을 콜함

        ![image-20180421044748856](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421044748856.png)

      * 2번에 순서번호를 매겨서 다음 걸 기다림

        ![image-20180421044851865](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421044851865.png)

      * 4번 다음 순서번호를 5번이라고 매기고 ack가 오기를 기다리느라 window는 멈춰있음

        ![image-20180421044927511](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421044927511.png)

      * 타임아웃이 되면 다시 2,3,4를 다시 보냄, 그리고 타이머를 다시 설정함

        ![image-20180421045110165](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421045110165.png)

    * 일련의 과정

      ![image-20180421045611614](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421045611614.png)

    * Receiver FSM

      ![image-20180421045721277](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421045721277.png)

    * Window size for Go-back-N 

      * 이 경우에는 크게 문제가 없지만

      ![image-20180421050311831](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421050311831.png)

      * 아래의 경우 문제가 발생, 마지막에 3번까지 보내고 다음에 만기가 되어버려서 다시 0을 재전송을 하려는데 순서번호로만 체크하기 때문에 이것을 구별 못함

        ![image-20180421050842849](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421050842849.png)

      * Go-Back-N을 설계할 때에는, 윈도우의 크기를 결정하든 순서번호의 개수를 결정하든, 순서번호의 개수가 윈도우의 크기보다는 커야함

  * Selective repeat

    * sender와 receiver모두 윈도우를 가지고 있음
    * rcvbase에 해당하는 패킷이 아직 받지 못하였으니 리시버가 멈추어져있음
    * 보면 앞에 두개가 아직 안보내졌음, receiver은 ACK을 다 보냈다고 생각하고 sender는 ACK을 못받았다고 생각하고 있음 -> 너무 늦게갔거나 ACK을 버렸거나

    ![image-20180421051820886](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421051820886.png)

    ​