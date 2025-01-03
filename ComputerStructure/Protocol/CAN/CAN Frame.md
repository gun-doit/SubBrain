총 4가지 프레임 유형이 정의 되어 있다. 각 프레임은 특정 목적과 기능을 수행하며, 네트워크 내에서 필요한 정보를 교환하거나 통신 상태를 관리한다.

## CAN FD란
CAN FD는 CAN 통신에 "Flexible Data" 기능이 추가된 버전이다. ECU는 "flexible"하게 메시지의 크기와 전송 속도를 실시간으로 바꿀 수 있어 결과적으로 더 많은 양의 데이터를 빠르게 전송할 수 있다는 장점이 있다.

![[Pasted image 20241217174537.png]]
# Data Frame
![[Pasted image 20241218105833.png]]
**Data를 한 node에서 다른 node로 전송하기 위한 Frame**
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
## CAN FD Data Frame
![[Pasted image 20241218105851.png]]
일반 CAN과 Data Field크기의 차이가 있다. 기존 CAN Frame에서 8byte크기의 Data Field가 64byte로 증가했다.
## Detail of Data Frame
![[Pasted image 20241217174858.png]]
- CAN Rx : MCU로 입력되는 Data Line
- stuff bit : CAN Bus에 문제가 있는지 확인하는 bit
- ACK Delimeter, CRC Delimeter, EOF Bit은 CAN Frame에서 1로 고정
# Retmote Frame
특정한 Data Frame의 전송을 다른 Node에 요청하는 프레임
   -> ID 값이 들어가는 Filed가 있어 표준형과 확장형으로 나뉨![[Pasted image 20241217175058.png]]
- DLC와 CRC 사이에 Data Field가 없다는 것과 RTR bit의 값을 제외하고 Data Frame과 동일
	- Data를 요청하는 Frame이기 때문에 Data Field 필요 X
![[Pasted image 20241217175142.png]]
## Remote Frame의 사용
Node A에서 Remote Frame 전송
- A에서 보내는 Message는 Remote Frame이므로 Data Field가 없음
- ID Field 내에 있는 값을 갖는 Message를 Node B에 요청
Node B는 위에서 요청된 ID를 갖는 Message를 생성할 수 있는 Node
- 이 요청을 받아들여 해당 ID를 포함하는 Data Frame을 생성해 전송 
- 어떤 Node에서 이 Message를 받는지는 모름
위처럼 Data Frame과 Remote Frame은 한 쌍으로 주고 받아지며, 두 Frame의 ID 값은 같아야 한다
![[Pasted image 20241217175306.png]]

# Error Frame
어떤 node에서 Error가 발견됐을 경우 주변 node들에게 Error가 났다는 사실을 알리기 위한 Frame
![[Pasted image 20241217175328.png]]
- Error 발생 시 상태를 알려주기 위한 부분
    - 위의 Error Flag - Error Delimiter 까지가 Error Frame
    - Error Flag (무조건 6 bit)
    - Error Flag (Secondary) : 올 수도 있고 안올 수도 있다 (0~6 bit)
    - Error Delimiter : Error 구분자. 8개의 Logic '1'의 값을 가짐
- Error Flag는 Error의 상태에 따라 능동 / 수동 Error Frame으로 나뉨
    - CAN Node는 자체적으로 Error Counter를 가짐 (Error 발생 시 +1, 정상 동작 시 -1 방식?)
    - 이 Error Counter가 일정 값 이상이 되면 Error가 많이 발생했음을 인지하고 
    - Error가 별로 없으면 능동, 많으면 수동 Error Frame 사용
    - 능동 Error Flag는 6~12개의 '0', 수동은 6개의 '1'이 들어감
- 즉 Node의 Error 상태에 따라 Error Flag의 값이 달라짐
# Overload Frame

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
