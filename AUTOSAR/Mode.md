Mode : ECU의 상태를 나타내는 집합
![[Pasted image 20241126152040.png]]

### Mode Management
역할에 따라 Requester, Manager, User로 나누어진다.
Requester : Manager에게 Mode를 요청
Manager/User : Mode arbitration rule을 만족하면, Manager는 User에게 Mode 변경됨을 알린다. Mode Manager, User는 요청 주체에 따라 어떤 SWC라도 될 수 있다.
![[Pasted image 20241126152432.png]]
![[Pasted image 20241126152445.png]]



## Ecu State Sequence
- 부팅 이후부터 Off / Sleep 까지의 Ecu state flow는 아래와 같이 Startup / Run / Shutdown으로 나눠진다.
- Application Inactive_Off/Sleep/Reset로 Mode 변경 시 각각의 Shutdown Sequence로 이행한다
![[Pasted image 20241126160036.png]]
![[Pasted image 20241126165434.png]]


# Mode Managment 동작
BswM ( Basic Software Mode Manager )
모드 변경 시 정의된 액션을 수행하도록 제공하는 모듈
![[Pasted image 20241126161510.png]]
**Application 모드 정의 및 전달 과정**
- **Mode Request 방식으로 Mode 변경 요청을 수행, Mode Switch 방식으로 Mode 변경**
- **Mode Request : SWC가 Mode 요청 → Mode manager가 조건 판단, 모드 변경**
- **Mode Switch : Mode manager가 모드를 관리/변경 후 변견된 모드를 User에게 알리는 방식, Mode switch Interface를 사용하므로 1:N Conncetion**