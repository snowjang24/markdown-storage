

# Transport Layer (Reliable data transfer - Part 1)

* Transport layer : application이 메세지를 주거니 받거니 하도록 도와주는 기능을 하는 것

  * Sender : application이 메세지를 보내달라고 하면 세그먼트 크기로 잘라서 네트워크 레이어로 보내주라고 요청함

  * Receiver : 세그먼트를 다시 메세지로 조합하여 application 레이어로 전달

  * 컨텍스트와는 무관하게 자름, 이렇게 TL에서 분리하는 이유는 모든 AL에서 함수처럼 써야하기 때문에 TL에서 함

    ![image-20180420230034148](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420230034148.png)

  * TCP : 충실한 TL, 순서에 맞춰서 하나도 놓치지 않고 보내줌

    * Congestion control : sender가 데이터를 보내는데 있어서 네트워크에서 수용할 수 있을 만큼만 보내게 조절
    * Flow control : receiver가 받을 수 있는 만큼만 보내게 조절
    * Connection setup : 상대방이 준비되었는지 확인하고 보내는 역할을 함

  * UDP : 완전한 배달을 하진 않음, 순서대로가는지 빼먹은건 없는지 신경 X

    * 전송속도가 빨라서 필요한 상황에 씀

  * TL에서도 해주지 못하는 것 이 있음

    * send application에서 receive application까지 가는 시간을 보장 못함
    * 단위 시간당 보내는 양(Bandwidth)을 보장하지 못함
    * 위의 특징의 이유는 딜레이가 end호스트 보다는 라우터에 영향을 받음, 라우터는 NL까지 밖에없음(TL, AL없음)

    ![image-20180420235153719](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180420235153719.png)

* TL의 특징

  * Multiplexing /demultiplexing

    * Multiplexing : 여러 input을 받아서 하나의 output으로 내보내는 것

    * 여러 소켓에서 오는 input을 받아서 다른 하나의 소켓으로 보내는 것 

      ![image-20180421005250642](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421005250642.png)

    * Demultiplexing : 하나의 input으로 들어온 것을 여러개의 output으로 내보내는 것

    * 하나의 운영체제로 들어온 input을 해당하는 socket들에 분배

      ![image-20180421005309758](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421005309758.png)

  * Demultiplexing이 작동하는 방법

    ![image-20180421011458316](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421011458316.png)

  * Connectionless demultiplexing

    * UDP는 어느 프로세스로 가는지만 중요함, 여러 클라이언트가 보내는 메세지에 대해 하나의 문으로 그냥 받음 어느 클라이언트가 보냈는지에 대해 관심이 없음

    ![image-20180421011742238](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421011742238.png)

    * TCP는 꼼꼼함, 따라서 어떤 클라이언트가 보내는지 다 알고 있어야함, 개별적으로 state를 관리해야함, 각 클라이언트에 대해 별도의 소켓과 별도의 문을 가지고 있음, 따라서 제한된 자원에 따라 한정된 수용력을 가짐

      ![image-20180421012137447](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421012137447.png)

* Principles of reliable data transfer(핵심)

  * Reliable data transfer : sender가 보낸 데이터를 온전히 다  receiver에게 배달하는것, but sender와 receiver은 서로 볼 수 없기 때문에 완전하게는 아직은 안됨

    * TL에서 sender가 보낸 데이터를 온전히 receiver에게 전달해주려함, 근데 현실적으로 NL에서 사용하는 IP라는 프로토콜은 Unreliable해서 그냥 다 받은대로 넘기고 잊어버림, 그래서 이마저도 TL에서 책임짐

      ![image-20180421013455615](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421013455615.png)

  * RDT, sender side

    * rdt_send() : AL에서 TL에게 데이터 전송을 요청하는 api

    * udt_sed() : TL가 NL에게 데이터 전송을 요청하는 api

      ![image-20180421013651473](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421013651473.png)

  * RDT, receiver side

    * deliver_data() : NL가 TL을 통지하는 api

    * rdt_rcv() : TL가 다 처리하고 AL에게 넘겨야할 것만 뽑아서 넘기는 api

      ![image-20180421013852397](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421013852397.png)

  * Reliable data transfer 과정

    * Finite state machine(FSM), 화살표는 state가 바뀜을 의미, 바 위는 state가 바뀌는 이유, 바 아래는 state가 바뀌면서 취하는 액션을 기록

      ![image-20180421014345028](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421014345028.png)

    * rdt1.0 : 네트워크에서 다 책임져서 아무 문제가 없이 진행된다고 전제

      ![image-20180421015550090](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421015550090.png)

    * rdt3.0 : 최악의 상황, 버려졌는지 안버려졌는지를 판단해야하며 누가 버려졌는지도 알고 있어야함, 따라서 TL에서 순서번호를 쫙 매겨서 빠졌는지 여부를 확인함, 순서 번호는 receiver만 확인 할 수 있음, 재전송은 sender가 해야함 결국 receiver가 sender의 재전송을 유도해야함, feedback해야함 -> 이를 ACK이라고 함

    * 데이터가 바뀌었는지 여부를 확인하기 위한 방법

      * Checksum : UDP와 TCP에서 사용되는 방법, 보내지는 데이터의 값을 합함, receiver는 확인 후 값이 다르면 sender에게 feedback을 보냄

        ![image-20180421020603313](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421021202254.png)

    * Sender는 정상적으로 갔으면 응답이 올 시간을 예측하고 만약 시간안에 ACK가 오지 않으면 문제가 생겼을 것이라고 판단하고 재전송함

    * 실제 버려진게 아니라 좀 늦어져서 재전송 하여 sender가 똑같은 패킷을 두번 보내는 상황이 생길 수 있음

      * 이때 또 보낸걸 식별하기 위해서 순서가 필요함

    * sender은 네가지 state를 가질 수 있음

      *  AL에서 데이터를 보내달라 요청하면 0번 순서를 붙여서 보내려고 대기하는 상태, 요청하기 준비 한 다음 타이머를 가동(start_timer)

        ![image-20180421022317270](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421022317270.png)

      * 0번을 보낸상태에서 receiver로 부터 ACK를 받을거라고 기대하며 대기하는 상태, 내가 기다리던 것이 왔기 때문에 stop_timer

        ![image-20180421022405715](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421022405715.png)

      * AL에서 데이터를 보내달라 요청하면 1번 순서를 붙여서 보내려고 대기하는 상태

        ![image-20180421022443075](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421022443075.png)

      * 1번을 보낸상태에서 receiver로 부터 ACK를 받을거라고 기대하며 대기하는 상태, 이후 다시 사이클을 뺑뻉 돔

        ![image-20180421022537052](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421022537052.png)

      * 1번을 보냈고, 다되었다 생각했는데 받았다는 ACK이 또오니 아무런 조치를 취하지 않음

        ![image-20180421022855626](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421022855626.png)

      * ACK을 기다리는데 망가져서 도착, 혹은 0을 기다리는데 1이 옴 역시 무시, 혹은 타이머가 지나버림

        ![image-20180421022944270](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421022944270.png)

        sender는 단순하게 타이머가 expire되면 무조건 재전송함

        ![image-20180421023527954](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421023527954.png)

    * Receiver는 두가지를 가짐

      *  0번 패킷이 올거라 기다렸고, 별 문제가 없음

        ![image-20180421023702993](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421023702993.png)

      * 1번 패킷 역시 별 탈없이 도착하여 1번 잘받았다고 네트워크에 배달

        ![image-20180421023738193](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421023738193.png)

      * 0번을 기다리다가 안망가졌지만 1번이 옴 : 1번은 재전송 되어서 온 것임, timer가 expire되었기 때문, 1번에 대한 ACK을 재전송함

        ![image-20180421023909916](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421023909916.png)

      * 1번을 기다리고 있는데 0번이 옴 : 0번에 대해 재전송 했기 때문에 받았다고 1번달라고 재전송함

        ![image-20180421023957038](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421023957038.png)

    * action상태

      * 문제 없을 때

        ![image-20180421030812810](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421030812810.png)

      * 문제가 있을 때

        * Packet이 손실 되었을 때

        ![image-20180421030830153](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421030830153.png)

        * ACK가 손실 되었을 때

        ![image-20180421030935639](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421030935639.png)

        * Premature timeout / delayed ACK

        ![image-20180421031038608](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421031038608.png)

  * Stop-and-wait operation(기본 개념)

    * sender가 처음 데이터를 보내기 시작한 시점부터 ACK를 받기 전까지 sender은 아무것도 안하고 기다림

    * RTT동안은 아무것도 안하게 됨

      ![image-20180421031316542](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421031316542.png)

    * 아래와 같이 효율이 너무 떨어짐

      ![image-20180421031840823](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421031840823.png)


* Pipelined protocols(SWO를 개선시킨 것) 혹은 Sliding Window protocol

  * 한번에 세개 보냄

    ![image-20180421032004085](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421032004085.png)

  * 패킷을 세개를 먼저 보냄, 윈도우가 허락하는 만큼

    ![image-20180421032155144](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421032155144.png)

  * 1번에 대한 ACK가 오면 옆으로 sliding함 sliding해서 4번을 보냄 뒤에는 계속

    ![image-20180421032247270](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421032247270.png)

  * sender가 계속 바쁘게 하려면 최소 창문 사이즈는 얼마가 되어야하는가 ? => 1+ RTT/(L/R) 하면 됨

    ![image-20180421033221480](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421033221480.png)

  * Pipelined protocolo에는 두가지가 있음

    * Go-back-N : sender는 윈도우 사이즈 만큼 ACK를 받지 않은 상태에서 연속적으로 전송, receiver는 cumulative ACK으로 응답함, 이는 내가 받은 패킷 중에 하나도 빈자리 없이 받은 것 중에 가장 순서번호가 큰 녀석을 알려줌

      ![image-20180421033708053](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421033708053.png)

      ![image-20180421033713350](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421033713350.png)

      * 4번에 연속된 가장 큰 숫자인 2를 부여 Ack2, 그런다음 4를 버림

      ![image-20180421033807776](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421033807776.png)

      ![image-20180421034228168](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421034228168.png)

      ![image-20180421034315600](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421034315600.png)

      * 타이머가 만기가 되면 받지 못한 패킷을 다시 보낸다

      ![image-20180421040126575](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421040126575.png)

    * Selective Repeat : sender는 윈도우 사이즈 만큼 ACK를 받지 않은 상태에서 연속적으로 전송

      * 없음 없다고 고백함

        ![image-20180421034356047](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421034356047.png)

      * 개개마다 타이머가 있어 타이머가 끝나면 부족한거만 보냄

      ![image-20180421040209228](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421040209228.png)

  * Go-back-N : sender windows

    ![image-20180421040446957](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421040446957.png)

    ![image-20180421040500287](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421040647516.png)

    * receiver입장에서 일단 배달은 되었다고 가정하기 때문에 위와 같은 그림이 나옴 

    ![image-20180421040856094](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421040856094.png)

    ![image-20180421040902323](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421040902323.png)

  * Selective repeat : sender, receiver windows

    * sender는 여전히 receiver로 부터 받지 않았다고 생각 중

    ![image-20180421041141967](/Users/soonhojang/Documents/마크다운/네트워크/assets/image-20180421041141967.png)