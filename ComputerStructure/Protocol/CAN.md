>Controller Area Network
### CAN 통신 이란
- **Fault Tolerant system**  기능을 지원하는 Low Speed CAN과 High Speed CAN으로 두 가닥의 일반 전선으로 구성된다.
- 차량 내 각 ECU 장치들이 Host Computer 없이 서로 통신하기 위해 설계된 Message 기반 표준 Protocol

### CAN의 구성
![[Pasted image 20241217164411.png]]
##### #RS485 의 Twisted Pair Cable을 통해 Serial 통신으로 통신
- EMI(Electromagnetic Interface)에 덜 영향을 받고자 위와 같은 구조 채택
- CAN Bus의 양 끝에 Termination Resistor가 위치
##### 각 Node는 고유의 ID를 보유 : ID 값을 통해 통신 순위를 선택

### CAN의 특징
##### 메시지 지향성 프로토콜 
- 메시지의 우선순위에 따라 ID를 할당하고, 이 ID를 이용해 메시지를 구별하는 방식
##### Multi Master 통신
- 여러 ECU들이 통신 Bus를 공유하며 필요할 때마다 Bus를 사용 가능
##### Node의 ID Filtering을 통한 Message 우선 순위 지정으로 Node 간 통신 중재
- #CAN_Filtering 을 통해 ID 값을 수신하여 우선순위를 결정하여 버스 사용시 충돌 방지

### High Speed CAN vs Low Speed CAN
![[Pasted image 20241217165345.png]]

##### High Speed CAN
![[Pasted image 20241217165458.png]]
- Logic 1 전송 시 CAN_H, CAN_L가 모두 2.5V를 가짐
- Logic 0 전송 시 CAN_H는 3.5V, CAN_L는 1.5V를 가짐
	- Recessive(열성) Voltage : 1 bit
	- Dominatn(우성) Voltage : 0 bit
![[Pasted image 20241217165811.png]]
- Bus 구성의 Topology
- Termination은 양단 끝에서 처리
##### Low Speed CAN
![[Pasted image 20241217165639.png]]
- Logic 1 전송시 CAN_H는 최대 0.3V, CAN_L는 최소 4.7V를 가짐
- Logic 0 전송시 CAN_H는 최소 3.6V, CAN_L는 최소 1.4V를 가짐
	- Recessive(열성) Voltage : 1 bit
	- Dominatn(우성) Voltage : 0 bit
- Fault Tolerant라 불리는 이유 : 위의 두 선 하나가 끊어지더라고 충분히 통신이 가능함.
![[Pasted image 20241217165825.png]]
- 복잡한 Bus형태로 구성 가능

---
### CAN Frame
![[Pasted image 20241217174213.png]]
1. Data Frame : Data를 한 node에서 다른 node로 전송하기 위한 Frame
2. Remote Frame : 특정한 Data Frame의 전송을 다른 Node에 요청
   -> ID 값이 들어가는 Filed가 있어 표준형과 확장형으로 나뉨
3. Error Frame : 어떤 node에서 Error가 발견됐을 경우 주변 node들에게 Error가 났다는 사실을 알리기 위한 Frame
4. Overlaod Frame : 어떤 node가 remote frame을 받았는데,그 node가 이미 하던 일이 있어 바로 보낼 수 없게 되는 경우, 자신이 과부하 상태임을 알리는 Frame

![[Pasted image 20241217174537.png]]
### Data Frame
![[Pasted image 20241217174843.png]]

- **IFS (Inter Frame Space) :** Frame 간 3bit 정도의 간격 유지용. Idle Time 유지 역할
- **SOF (Start Of Frame) :** 모든 Frame이 기본적으로 보유하는1bit Data. Frame의 시작을 알림
- **ID (Identifier) :** Bus에 접근할 Node 설정 (통신할 장치 선택). 표준형은 11bit, 확장형은 29 bit
- **RTR (Remote Transmission Request) :** 이 Frame이 Data / Remote Frame인가를 알림  
    - 0 (Dominant) : Data Frame
    - 1 (Recessive) : Remote Frame
- **IDE (IDentifier Extension)** : 이 Data Frame이 표준형 / 확장형 Data Frame인가를 구별하는 기준
    - 0 : Standard Frame 
    - 1 : Extended Frame
    - 확장형의 경우 IDE 뒤에 확장되는 ID가 따라옴(18bit)  
          
        
    - **SRR (Substitute Remote Request)** : 현재 Data Frame이 확장형인 경우, RTR은 확장된 ID 뒤로 이동하고  
        원래 RTR의 자리를 대체하는 1bit
    - ID 값이 끝난 후에 RTR bit를 표시할 수 있도록 RTR을 임시적으로 대체해주는 역할
- **DLC (Data Length Code)** : 0~8 byte의 크기를 나타냄 
- **Data :** 
- **CRC (CycleRedundancy Check) :** Serial 통신시 Noise가 많이 발생하므로, 통신 Data의 검증을 위해 사용
    - 송신 Node에서 **Bit pattern**을 보내며 그에 대한 **CRC** 값을 계산하고 뒤에 붙여서 보냄
    - 수신 Node에서는 받은 Bit pattern으로 **CRC를 직접 계산**하고, 송신단에서 **보낸 CRC값과 비교**하여 같은지 확인
    - 둘이 다르면 수신한 **Bit pattern** 중에 **Error가 발생**한 것
- **ACK(Acknowledge) :** Receiver로부터의 Acknowledge
    - 송신 Node에서 이 bit를 1로 보냄
    - 수신 Node에서 Message를 받고 Error 없이 잘 받았음을 표시하기 위해 ACK Bit에 1을 Overwrite  
        0이 Dominant Bit이므로 0이 쓰임
    - 즉 **수신단에서 Message를 정상적으로 받았다면 ACK 값이 0으로 변함**
- **EOF (End Of Frame) :**
##### Detail of Data Frame
![[Pasted image 20241217174858.png]]
- CAN Rx : MCU로 입력되는 Data Line
- stuff bit : CAN Bus에 문제가 있는지 확인하는 bit
- ACK Delimeter, CRC Delimeter, EOF Bit은 CAN Frame에서 1로 고정
### Retmote Frame
![[Pasted image 20241217175058.png]]
- DLC와 CRC 사이에 Data Field가 없다는 것과 RTR bit의 값을 제외하고 Data Frame과 동일
	- Data를 요청하는 Frame이기 때문에 Data Field 필요 X
![[Pasted image 20241217175142.png]]
##### Remote Frame의 사용
Node A에서 Remote Frame 전송
- A에서 보내는 Message는 Remote Frame이므로 Data Field가 없음
- ID Field 내에 있는 값을 갖는 Message를 Node B에 요청
Node B는 위에서 요청된 ID를 갖는 Message를 생성할 수 있는 Node
- 이 요청을 받아들여 해당 ID를 포함하는 Data Frame을 생성해 전송 
- 어떤 Node에서 이 Message를 받는지는 모름
위처럼 Data Frame과 Remote Frame은 한 쌍으로 주고 받아지며, 두 Frame의 ID 값은 같아야 한다
![[Pasted image 20241217175306.png]]

### Error Frame
![[Pasted image 20241217175328.png]]
- Error 발생 시 상태를 알려주기 위한 부분
    - 위의 Error Flag - Error Delimiter 까지가 Error Frame
    - Error Flag (무조건 6 bit)
    - Error Flag (Secondary) : 올 수도 있고 안올 수도 있음 (0~6 bit)
    - Error Delimiter : Error 구분자. 8개의 Logic '1'의 값을 가짐
- Error Flag는 Error의 상태에 따라 능동 / 수동 Error Frame으로 나뉨
    - CAN Node는 자체적으로 Error Counter를 가짐 (Error 발생 시 +1, 정상 동작 시 -1 방식?)
    - 이 Error Counter가 일정 값 이상이 되면 Error가 많이 발생했음을 인지하고 
    - Error가 별로 없으면 능동, 많으면 수동 Error Frame 사용
    - 능동 Error Flag는 6~12개의 '0', 수동은 6개의 '1'이 들어감
- 즉 Node의 Error 상태에 따라 Error Flag의 값이 달라짐
### Overload Frame

![](https://blog.kakaocdn.net/dn/qLEdx/btsHz8O2IsL/xdP42QeZKgfqhCBurUMSZ1/img.png)

- Error Frame과 비슷한 형태
    - Overload Flag에는 6개의 '0'이 들어감
    - Overload Delimiter에는 8개의 '1'이 들어감

![](https://blog.kakaocdn.net/dn/F8qdL/btsHyUEesLJ/658F9cmcfN2Oxo6nD7IZK1/img.png)

- 위의 Overload Frame은 Active Error Frame과 같은 값을 가짐
- 위를 어떻게 구분? -> 모양은 똑같으나 CAN Node는 이 둘을 구분할 수 있음
    - Error Frame은 Data / Remote Frame을 전송하는 도중에 Error가 발생해서 그 즉시 Error Frame이 나오게 됨
    - Overload Frame은 한 Frame의 전송이 완료된 후 전송됨
    - 따라서 둘의 시점에 따라 Frame을 구분함 : Data / Remote Frame 도중에 검출되면 Error Frame, Data / Remote Frame 의 전송이 끝난 후에 검출되면 Overload Frame

### FullCAN vs BasicCAN
**FullCAN** : 수신되는 메시지를 종류별로 메시지 버퍼에 채운다. 만약 같은 종류의 메시지가 연속해서 수신 되면, 비록 다른 메시지 버퍼가 비어 있다고 하더라도 해당 메시지의 전용 버퍼에만 메시지를 채운다.
-> 이전의 메시지가 덮어 써 지지 않도록 CPU는 이전에 수신된 아직 처리되지 못한 데이터를 메시지 버퍼가 아닌 다른 곳으로 옮겨야 한다.

**BasicCAN** : 메시지 큐를 사용하여 선입선출의 방식으로 처리한다. 새로 수신된 메시는 종류에 상관없이 해당 큐에 채운다.


## CAN의 정의 및 구조
![[Pasted image 20241217154445.png]]
![[Pasted image 20241217161746.png]]



---
> Fault Tolerant system  : 결함 허용 시스템
> 시스템 내에서 오류나 결함이 발생하더라도 정상적으로 작동할 수 있도록 설계된 시스템을 말한다. 즉, 특정 부품의 고장, 소프트웨어 오류, 외부 환경 변화 등으로 인해 문제가 생기더라도 시스템 전체가 멈추지 않고 계속 기능을 수행할 수 있도록 하는 것이 목표이다.

1. 결함 감지(Fault Detection)
	- 시스템 내부에서 결함을 빠르게 감지하여 적절한 대처를 할 수 있도록 설계
2. 결함 격리(Fault Isolation)
	- 문제가 발생한 부분을 시스템에서 분리하여 나머지 부분의 정상 작동을 보장
3. 결함 복구(Fault Recovery)
	- 결함이 발생한 후에도 대체 경로, 예비 시스템, 또는 복구 매커니즘을 통해 시스템이 계속 운영
4. 중복성(Redundancy)
	- 동일한 기능을 수행할 수 있는 하드웨어나 소프트웨어를 추가로 제공하여 고장이 나더라도 대체할 수 있도록 한다.

[CAN 통신이란](https://youngseong.tistory.com/336)
[기술블로그 - INSIGHT - 페스카로(FESCARO) - 자동차 소프트웨어 전문기업(자동차 사이버보안, 제어기, V2X)](https://www.fescaro.com/ko/archives/249/)
