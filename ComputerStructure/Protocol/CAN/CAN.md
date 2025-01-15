>Controller Area Network

[CAN통신의 Fault & Bus Off에 대하여 (작성중)](https://newbie-developer.tistory.com/240

D-Sub Connecter
![[Pasted image 20250115104859.png]]
Can low -2
Can high - 7

120옴 제한
통신을 통해 데이터를 보낸다는 것은 전기적인 신호를 통해 정보를 전달한다
CAN 통신은 버스 토폴로지로 정보가 버스엔에 올라간다는것
양끝단에서 신호를 반사시켜 정보 변환을 방지

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
##### 브로드캐스트 방식
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
	- Dominant(우성) Voltage : 0 bit

Dominant가 Recessive보다 우선순위가 높다.

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
### 
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
