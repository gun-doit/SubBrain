[참조 링크](https://blog.naver.com/mdstec_auto/222070210412)

[참조 링크_2](https://blog.naver.com/mdstec_auto/222070210412)

## AUTOSAR CAN 통신 개요

**송신** : Application Layer → Communication Services → Hardware Abstraction → Drivers  
**수신** : Driver → Hardware Abstraction → Communication Services → Application Layer  


![[image 27.png|image 27.png]]

![[image 1 6.png|image 1 6.png]]

### Overview of CAN Stack Architecture

Can Stack Architectur 는 5개의 기능 모듈로 구성된다.

|**모듈**|**기능 설명**|
|---|---|
|**  <br>Com  <br>**|**PDU Data를 signal 단위로 읽고 쓸 수 있는 Interface를 제공  <br>  <br>**==**주기적으로 PDU 송신**==**  <br>Signal별 Time Out, Data Received , Data Send 등의 이벤트를 ASW에 통지  <br>**|
|**PduR**|**Routing Table에 설정된 PDU Reference를 참조하여 Source와 Destination 모듈간에 PDU를 전달**|
|**  <br>  <br>CanIf  <br>**|**CAN Driver로 부터 수신한 CAN Frame을 PDU로 변환하여 상위 Layer로 전달  <br>상위 Layer가 송신한 PDU를 CAN Frame으로 변환하여 CAN Driver에 전달  <br>CAN Controller 및 Transceiver를 제어하는 Interface 제공  <br>Wakeup 상황 감지 후 유효성 검사  <br>BusOff발생을 MCAL Driver로 부터 통시 받아 CanSM에 전달  <br>**|
|**CanDriver**|**CAN Controller의 활성화 및 비활성화 제어  <br>CAN Interrupt Handler를 제공( Tx, Rx, WakeUp, BusOff 등)  <br>- Interrupt 대신 주기 Task를 이용한 Polling방식도 가능  <br>**|
|**CanTrcv**|**CAN Transceiver 하드웨어의 상태 제어 ( Sleep/Enable/Standby )  <br>WakeUp Pattern에 의한 WakeUp 기능제공  <br>**|

### Overview of CAN Status Stack Architecture

Bus-Off Recovery 기능과 Network Status 제어 기능을 포함한다

|**모듈**|**기능 설명**|
|---|---|
|**BswM**|**Rule에 따른 Action제어**|
|**  <br>ComM  <br>**|**통신 제어를 요청하는 Interface를 제공  <br>통신제어 기능 실행 시 하위 BusSM모듈에게 명령을 전송  <br>Nm Interface 모듈에게 Network Request/Release 명령 전송  <br>**|
|**  <br>CanSM  <br>**|**BusOff 발생 시 BusOff Recovery Process 실행  <br>CAN 통신 기능을 제어하여 활성화 또는 비활성화 시킴  <br>CAN 통신 기능 상태를 ComM에게 통지  <br>**|

### Overview of CAN Network Stack Architecture

Network 구성과 Sleep 제어 기능을 포함한다.

| **모듈**                            | **기능 설명**                                                                                                                                                                 |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **  <br>Nm  <br>Interface  <br>** | **ComM으로 부터 Network Request 또는 Release 명령을 받아 실행  <br>Network 요청 상태에 따라 하위 BusNm 모듈 제어  <br>전체 Network Cluster가 동기화 되어 SLEEP에 진입하도록 제어  <br>Network 상태를 ComM에게 통지  <br>** |
| **CanNM  <br>(OsekNm)  <br>**     | **NM PDU를 송수신 하여 Network의 상태를 감시  <br>Network상에 있는 모든 제어기들이 동시에 BUS SLEEP상태에 진입하도록 제어  <br>NM Interface모듈에게 Network 상태를  <br>**                                           |

  

## 통신 이벤트 경로

![[image 2 6.png|image 2 6.png]]

  

### CAN 통신 시작 과정

![[image 3 6.png|image 3 6.png]]

1. **SWC가 RTE C/S 통신을 통해 User ID와 함께 ComM 모듈에게 통신 시작 요청을 보낸다.**
2. **통신 시작 요청을 받은 ComM모듈은 전달된 User ID를 이용하여 내부 채널을 찾고 이와 연결된 CanSM 모듈의 채널로 통신 시작 요청**
3. **Nm 모듈이 있는 플랫폼의 경우 연결된 Nm 채널로 통신 시작 요청**
4. **CanSM 모듈은 해당 채널과 연결된 CanIf 모듈의 Controller ID를 검색하여 CAN Controller 시작 요청을 보낸다.**
5. **CanIf 모듈은 Controller ID와 함께 CAN Controller 시작 요청을 CAN Driver에게 전달한다.**
6. **CanIf 모듈은 CAN Controller 시작이 성공했는지를 확인한 후 결과를 CanSM 모듈에게 통지한다.**
7. **CanSM 모듈은 CanIf 모듈로부터 받은 결과를 ComM 모듈에게 전달한다.**

  

## Bus Off 처리 과정

![[image 4 5.png|image 4 5.png]]

  

  

  

  

  

  

  

## CAN통신 Sleep 과정

![[image 5 5.png|image 5 5.png]]

|   |
|---|
|**① ASW에서 통신 중지 명령을 보낸다.**|
|**② ComM가 NmI에게 Network Release 명령을 보낸다.**|
|**③ NmI는 하위 각 Bus Nm에게 Network Release 명령을 보낸다.**|
|**④ 각 Bus Nm들은 자신이 속한 Network가 SLEEP에 진입하면 NmI에게 통지**|
|**⑤ NmI는 모든 Cluster가 SLEEP에 진입한 것을 확인하고 ComM에게 통지**|
|**⑥ ComM는 통신 중지를 최종 승인, CanSM에게 통신 중지 명령**|
|**⑦ CanSM은 CanIf에게 통신 중지 명령**|
|**⑧ CanIf는 MCAL Can Driver에게 CAN Controller SLEEP/STOP 명령**|
|**⑨ CanIf는 CanTrcv에게 CAN transceiver SLEEP/STANDBY 명령**|

  

  

  

  

  

## CAN

### CAN Hardware Object

**CAN Controller의 내에 존재하는** ==**메모리 버퍼**== **/ 송신 or 수신용으로 사용될 수 있다.**

![[image 6 5.png|image 6 5.png]]

### CAN frame 수신 과정

1. CAN Controller가 버스 상의 CAN frame을 감지해서 지정된 Hardware Object에 저장
2. CAN frame이 수신된 Hardware Object의 Pending Flag가 1로 설정되며 인터럽트를 사용하는 경우에는 수신 인트럽트가 발생
3. 수신 인터럽트 또는 CAN Driver의 주기 함수에 의해 CAN Driver의 수신 함수가 실행된다.
4. CAN Driver는 수신된 CAN frame를 DPU로 변환하며 CANIF 모듈에게 넘겨준다.

### CAN frame 송신 과정

1. CAN IF에서 PDU를 송신하기 위해 PUD ID를 Hardware Object Handle로 변환하여 CAN Driver의 송신 함수를 호출
2. CAN Driver는 송신할 데이터를 Hardware Object에 복수한 후 Request Flag를 1로 설정한다.
3. CAN Controller는 송신 요청된 Hardware Object를 CAN frame으로 구성하여 버스 상으로 송출
4. 버스 상에서 ACK이 확인된 경우 Pending Flag가 1로 설정되며 인터럽트를 사용하는 경우는 송신 완료 인터럽트가 발생한다.
5. 송신 완료 인터럽트 또는 CAN Driver의 주기 함ㅅ후에 의해 CAN Driver가 송신이 완료되었음을 CANIF 모듈에게 통지
6. CAN IF에서 해당 PDU에 대해 송신 queue가 설정되어 있고 송신할 PDU가 저장되어 있는 경우 CAN Driver 송신 함수를 다시 호출
7. CAN IF에서 송신 완료에 대해 상위 모듈로 통지

  

![[image 7 4.png|image 7 4.png]]

- **차량 내** ==**호스트 컴퓨터 없이**== **마이크로 컨트롤러나 장치들이 서로 통신하기 위해 설계된  
      
    **==**표준 통신 규격**==
- `**CSMA/CD+AMP**`**, 차량 내에서 가장 많이 사용되는 통신방식**
- **저비용, 꼬인 2선 사용, 버스형 통신**

  

## 특징

1. **메시지 지향성 프로토콜 ( Message-Oriented Protocol )  
    노드의 주소에 의해 데이터가 교환되는 것이 아니라  
    **==**메시지의 우선순위에 따라 ID(IDentifier)를 할당하고, 이 ID를 이용해 메시지를 구별하는 방식**==**을 사용한다.  
    ⇒ 자신에게 필요하다면 받아들이고, 아니라면 무시한다.  
    **
2. **보완적인 에러 감지 메커니즘  
    다양한 에러 감지 메커니즘이 상호 보완적으로 에러를 감지하기 때문에 높은 안정성을 보장한다.  
      
    **==**메시지 전송 시, 에러가 감지되면 자동적으로 해당 메시지를 즉지 재전송**==**하는 기능이 있기에 다른 프로토콜에 비해 에러 회복 시간이 짧다.**
3. **멀티 마스터 능력  
    감독자 노드(Bus Master)의 필요가 없다. 즉 모든 노드가 버스 마스터가 되어  
    **==**버스가 비어 있을 때 (IDLE)이라면 언제든지 메시지 전송이 가능**==
4. **결점 있는 노드의 감지와 비활성화  
    버스의 상태를 항상 모니터링 하기에  
    **==**실시간으로 결함이 있는 노드를 감지해 해당 노드를 비활성화함으로 네트워크 신뢰성을 보장**==
5. **전기적 노이즈에 강함  
      
    **==**꼬인 2선(Twist Pair Wire, *CAN_H, CAN_L)**==**을 이용하여 전기적으로 차별되는 통신을 한다**

  

  

## 동작 원리

**다중통신망이며 CSMA/CD+AMP방식을 이용한다.  
어떠한 노드로부터 보내진 메시지  
**==**송신측이나 수신측의 주소를 포함하지 않는다.  
  
**==**대신 메시지의 처음부분에** ==**CAN네트워크상에서의 각각의 노드를 식별할 수 있도록 ID(11bits or 29bits)**==**를 가지고 있다.**

![[image 8 4.png|image 8 4.png]]

**이를 통해 네트워크상에 있는 메시지를 수신한 후 자신이 필요로 하는 식별자의 메시지인 경우에만 받아들이고, 그렇지 않은 경우의 메시지는 무시한다.**

  

## 포맷

**Dada frame, Remote frame, Error frame, Overload frame 의 4가지 프레임 타입을 정의하고 있다.  
데이터 프레임 - 일반적으로 데이터 전송에 사용  
리모트 프레임 - 수신할 노드에서 원하는 메시지를 전송할 수 있는 송신 노드에게 전송을 요청할 때  
에러 프레임 - 메시지의 에러가 감지되었을 때 시스템에 알릴 목적으로 사용  
오버로드 프레임 - 메시지의 동기화를 목적으로 사용  
  
  
**==**CAN통신에서의 데이터 송수신은 메시지 프레임을 사용하여 이루어진다.**==**  
[ 메시지 프레임 구조 ]  
**

![[image 9 4.png|image 9 4.png]]

**SOF (Start Of Frame) - 한 개의 dominant 비트로 구성, 메시지의 처음을 지시, 모든 노드를 동기화  
  
Arbitration Field - 11 or 29bits를 가진 ID와 1bit의 RTR(Remote Transmision Request) 비트로 구성, 이 영역은 둘 이상의 노드에서 메시지의 전송이 동시에 일어날 경우 발생하는 메시지 간의 충돌을 조정하는데 사용,  
**==**RTR의 값은 데이터 프레임이면 d, 리모트 프레임이면 r**== **를 결정  
  
Control Field - 2비트의 IDLE 비트, 4비트의 데이터 길이 코드(DLC, Data Length Code)로 구성, R0는 Reserved 비트(Extended CAN 2.0B R0, R1)이다.  
  
Data Field - 8bytes까지 사용 가능, 데이터를 저장하는 데 사용된다.  
  
CRC - SOF에서부터 데이터 필드까지의 비트열을 이용해 생성한 15비트의 CRC 시퀀스와 하나의 ‘r’비트의 CRC 델리미터로 구성,**==**메시지상의 에러 유무 검사  
  
  
**==**ACK - 한 비트의 ACK슬롯과 하나의 ACK 델리미터(’d’)로 구성, 임의의 노드에서 올바른 메시지를 수신하게 되면 ACK필드를 받는 순간 ACK 슬롯의 값을 ‘d’로 설정해 버스 상에서 계속 전송  
  
EOF - 7개의 ‘r’비트로 구성되어 메시지의 끝을 알리는 목적으로 사용  
**

## 규격

**표준 CAN(버전 2.0A) : 11비트 식별자**

**확장 CAN(버전 2.0B) : 29비트 식별자**

**⇒ ISO 규격에 따라 두 가지로 구변되며** ==**통신 속도에서 차이**==**가 있다.**

**ISO 11898 : 1Mbps 이상의 고속 통신 가능 [CAN 2.0C]  
ISO 11519 : 125Kbps 까지의 통신 가능 [CAN 2.0B]  
**

  

**대부분의** ==**CAN 2.0A 컨트롤러는 오진 표준 CAN 포맷의 메시지만 전송 및 수신이 가능하며, 확장 CAN 포맷(CAN 2.0B)의 메시지를 수신하더라도 그 메시지를 무시**==**해 버린다.  
그러나  
**==**CAN 2.0B는 양쪽 메시지 포맷에 대해 모두 송수신이 가능**==**하다.**

  

## **CAN 통신 3계층 구조**

- **응용/데이터 링크/물리 계층으로 구성**
- **ISO 11898에서 데이터 링크/물리 계층 표준을 정의**

![[image 10 3.png|image 10 3.png]]

### 물리 계층 [ 1계층 ]

**물리적 연결 방법 - 2개의 전송 라인 사용 [CAN_H, CAN_L]  
차동 신호  
정의 : 크기가 같고 부호가 반대인 두 신호의 차이  
{CAN_H - CAN_L} when CAN_H = -CAN_L  
  
**==**두 신호 라인에 동일하게 유입되는 노이즈 제거에 유리  
  
  
**==**꼬인 2선 구조[ w / 차동 신호 ]**

  

![[image 11 3.png|image 11 3.png]]

  

### 데이터 링크 계층 [ 2계층 ]

- **프레임 구조  
    물리 계층을 통해 전송될 데이터 포맷  
    프레임 길이는 가변 [ 제어 필드 값에 의해 결정 ]  
    **
- ==**필드 구성은 위 참조**==

  

- **중재 [ Arbitration ]  
    둘 이상의 노드가 동시에 송신을 요청하는 경우 → ID가 낮은 것만 송신됨  
    IDentifier를 전송하면서 피드백 확인  
    Recessive 전송 & Dominant 피드백 시 → 신호 전송 중지  
      
    **

![[image 12 3.png|image 12 3.png]]

- **비트스터핑 [ Bitstuffing ]  
    모든 제어기가 동일한 클락을 사용하지 않음 →  
    **==**동기화가 필요  
      
    **==**Falling edge [R→D] 발생시 동기화 수행  
    5 bit 이상 동일한 데이터 전송 시 추가 bit 삽입  
    **

![[image 13 2.png|image 13 2.png]]

# CAN FD

**데이터 전송 시간을 줄이고 CAN 네트워크 부하를 낮춤**

1. **데이터 길이 - 64Bytes로 확장**
2. **데이터 전송 속도  
    100Kbit/s ~ 5Mbit/s, CAN FD표준에서 최고 15Mbit/s까지 허용  
    High Speed CAN(1Mbit/s) 속도와 FlexRay(10Mbit/s) 전송속도의 사이  
    **
3. **데이터 보안  
    CRC Field 증가  
    확장된 데이터 길이에도 CAN 프로토콜과 동일한 요건 충족  
    **

![[image 14 2.png|image 14 2.png]]

**BRS 비트로 Control field와 Data field 부분의 비트 속도를 올려 동일 시간에 더 많은 데이터 전송  
Control Field는 6bis → 9bits로, Data field는 최대 8bits → 64bits로 확장  
Control Field에 추가된 비트는 EDL, BRS, ESI이며 DLC값에 따라 Data Filed의 길이 선택  
**

  

**FDF : CAN FD 프레임 여부 [ 비트가 1이면 FD ]**

![[image 15 2.png|image 15 2.png]]

  

  

  

# Q?

1. **CAN버스에는 하나의 데이터 프레임만 있는가?**
2. **CAN버스 선이 다른 제어기에 의해서 사용 중이다 라는 것은, 버스와 제어기의 연결 상태인가?**
3. **프레임의 ID는 받는 노드의 ID인가?**

---

**[ 용어 정리 ]**

[[CSMA-CD + AMP]]

[[STUDY/통신]]

  

---

**[LINK - 페스카로 기술블로그](https://www.fescaro.com/ko/archives/249/)**!
**[CAN FD 란?](https://m.blog.naver.com/suresofttech/221408852229)**

**[CAN Bus Off - 페스카로](https://www.fescaro.com/kr/insight/blog.php?code=blog&idx=15&bgu=view)**

[https://www.ni.com/ko/shop/seamlessly-connect-to-third-party-devices-and-supervisory-system/controller-area-network--can--overview.html#section--1725004742](https://www.ni.com/ko/shop/seamlessly-connect-to-third-party-devices-and-supervisory-system/controller-area-network--can--overview.html#section--1725004742)