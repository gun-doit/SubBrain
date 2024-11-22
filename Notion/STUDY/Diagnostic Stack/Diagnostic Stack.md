**AUTOSAR 진단 기능을 담당하는 모듈은 Dcm, Dem, Det으로 구성되어 있다.**

## Autosar

![[image 12.png|image 12.png]]

### DcmGeneral

![[image 1 5.png|image 1 5.png]]

1. 진단 메시지의 송수신 결과를 App 에 알려준다. Fail Safty에 대한 처리를 위해 사용
2. 진단 모듈이 동작하는 주기
3. 진단 Standard를 설정
4. User Defined Services 사용시 User의 Application Symbol 정보가 담긴 Header File을 추가한다.
5. Autron에서 제공하는 FBL과 포함된 보안 알고리즘 인증서 공개키 사용 여부를 결정한다.

### Dcm - Diagnostic Communication Manager

Communication Services Layer에 속하며 진단 서비스 Request에 대한 서비스 처리 및 Response 담당

![[image 2 5.png|image 2 5.png]]

**진단 통신의 Data Flow와 State를 관리하며 진단기의 진단 요청 수행  
Reset, Session 등 상태 변경을 BswM에 요청  
Full-, Silent-, No-Communication 상태 등을 ComM에 요청  
DTC정보를 Dem에 요청  
PduR을 통해 진단 데이터를 전송  
**

### DCM Behavior

![[image 3 5.png|image 3 5.png]]

### DCM Call Stack

![[image 4 4.png|image 4 4.png]]

  

## Protocol Definitions

|Communication Layer|Contents|
|---|---|
|Physical Layer|CAN Protocol|
|Datalink Layer|USD Protocol|
|Network Layer|Addressing Mode|
||Data Stream|
||CAN Message Structure , Example|
||Network Layer Timing Parameters|
|Application Layer|Request Message : SuppressPosRspMsgIndicationBit|
||Response Message  <br>(Physical Addressed Request Message 인 경우)|
||Response Message  <br>(Functional Addressed Request Message 인 경우)|
||Application Layer Timing Parameters|
||Session Layer Timing Parameter|

### Datalink Layer

**UDS Protocol ( Unified Diagnostic Services )**

|Service|Identifier|Description|
|---|---|---|
|DiagnosticSessionControl|SID10|Session 변경을 요청|
|ECUReset|SID11|ECU Reset을 요청|
|SecurityAccess|SID27|Security Level 획득을 요청|
|CommunicationControl|SID28|Normal Message를 허용하거나 억제|
|EnableNormalMsgTransmission|SID29|Normal Message를 허용|
|TesterPresent|SID3E|Tester기가 현재 진단 상태를 유지하기 위해 요청|
|ControlDTCSetting|SID85|고장 코드의 기록 유무를 조절|
|StopDiagnosticSession|SID20|(현재 Session이 Programming Session이 아닐 경우 ) 진단 상태를 초기화|
|ReadDataByIdentifier|SID22|Did를 기반으로 Data를 읽어온다.|
|ReadMemoryByAddress|SID23|Address를 기반으로 Memory 영역을 읽어온다.|
|WriteDataByIdentifier|SID2E|Did를 기반으로 Data에 값을 쓴다.|
|WirteMemoryByAddress|SID3D|Address를 기반으로 Memory 영역에 값을 쓴다.|
|ReadDTCInformation|SID19|고장 코드 정보를 읽어온다.|
|ClearDiagnosticInformation|SID14|고장 코드 정보를 초기화|
|InputOutputControlByIdentifier|SID2F|내부 로직의 input, output signal을 강제 변경|
|RoutineControl|SID31|정의된 로직을 수행하고 결과를 얻는다.|

## Network Layer

### **Addressing Mode  
두 종류의 Addressing Mode가 있다.  
**

Functional Addressing ( 1-to-n Communication ) : Single Frame 메시지에만 적용, Dcm은 Functional Rx Address는 7DF로 고정된 값을 가진다.  
Physical Addressing ( 1-to-1 Communication ) : 모든 타입의 메시지에 적용  

![[image 5 4.png|image 5 4.png]]

### Data Stream

Single Frame Transmission : 8-byte 이하 데이터 전송 방법  
Multi Frame Transmission : 8-byte 초과 데이터 전송 방법, Sender는 데이터를 First Frame과 Consecutive Frame으로 나누어 전송하고 Receiver는 Flow Control을 보낸다.  

![[image 6 4.png|image 6 4.png]]

### CAN Message Structure

![[image 7 3.png|image 7 3.png]]

`**N_PCI : Network Protocol Control Information**``**SF_DL : Single Frame Data Length**``**FF_DL : First Frame Data Length**``**SN : Sequence Number**``**FS : Flow Status**``**BS : Block Size**``**STmin : Separation Time Minimum**`

### CAN Message Example

==**STmin 2ms, BS = 4 기준 Multi Frame Transmission 예제**==

![[image 8 3.png|image 8 3.png]]

### Network Layer Timing Parameters

![[image 9 3.png|image 9 3.png]]

## Application Layer

### Request Message : SuppressPosRspMsgIndicationBit

Service Parameter에 따라 Subfunction을 지원하는 Service인 경우 다음 Byte는 Subfunction Parameter로 처리된다.

|Bit Position|Description|
|---|---|
|7|suppressPosRspMsgIndicationBit  <br>Subfunction Parameter Byte의 최상위 Bit는 긍정응답일 경우 응답이 금지(suppress) 됨을 의미한다.  <br>  <br>0 = FALSE, 긍정응답일 경우 서버가 긍정응답을 전송한다.  <br>1 = TRUE, 긍정응답일 경우 서버가 긍정응답을 전송하지 않는다.|
|6-0|Subfunction Parameter Value  <br>  <br>실질적인 Subfunction의 ID 값을 의미한다. 최상위 Bit를 제외하고 00 - 7F hex 범위의 Subfunction ID를 지정할 수 있다.|

### Response Message ( Physical Addressed Request Message인 경우 )

Subfunction이 지원되는 경우 SuppressPosRspMsgIndicationBit가 TRUE일 경우 No Response이다

![[image 10 2.png|image 10 2.png]]

### Response Message ( Functional Addressed Request Message인 경우 )

Subfunction이 지원되는 경우 SuppressPosRspMsgIndicationBit가 TRUE일 경우 No Response이다.  
serviceNotSupported, subfunctionNotSupported, requestOutOfRange 부정응답에 대해서 No Response 이다.  

![[image 11 2.png|image 11 2.png]]

### Application Layer Timing Parameters

P2CAN_SERVER : Request Reception 이후 Response를 처리할 떄까지의 시간

P2*CAN_SERVER : 0x78 ( Response Pending ) 처리 이후 다음 Response를 처리할 때 까지의 시간

![[image 12 2.png|image 12 2.png]]

![[image 13.png]]

### Session Layer Timing Parameter

S3SERVER : Diagnositc Session의 유지 시간

![[image 14.png]]

![[image 15.png]]

## Diagnostic Services

### DiagnosticSessionControl Sevice

진단 세션 변경을 요청하는 서비스 ( SID 10 )  
DefaultSession 이외의 세션에서 S3 time ( 5s ) 만료 이후 다시 DefaultSession으로 복귀한다.  

![[image 16.png]]

### Request Message

![[image 17.png]]

### Positive Response Message

![[image 18.png]]

### Negative Response Code

![[image 19.png]]

  

  

### SecurityAccess Service

보안, 안전상 이유로 접근이 제한된 데이터나 메모리 영역의 접근을 허가해주는 서비스 ( SID 27 )

requestSeed, sendKey 두 가지 절차를 거쳣허 보안 레벨을 획득

### Request Message

1. requestSeed : Client가 Server에 Seed를 요청한다. Server는 requestSeed를 요청 받으면 내부 알고리즘을 거쳐 Client에게 Seed를 요청한다.
    
    ![[image 20.png]]
    
2. sendKey : Client는 Server가 받은 Seed를 내부 알고리즘을 사용하여 암호화된 Key로 만들어 Server에 전송한다. Server는 해당 Key가 유효한 Key인지 검사하는 내부 알고리즘을 거쳐 Client에 보안 레벨 부여 유무를 결정한다.
    
    ![[image 21.png]]
    

### Positive Response Message

![[image 22.png]]

![[image 23.png]]

### Negative Response Code

![[image 24.png]]