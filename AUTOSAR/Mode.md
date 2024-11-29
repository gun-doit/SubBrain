#AUTOSAR
# Mode란?
> 일반적으로 특정 시스템의 상태(State)를 변경하는 것



Mode : ECU의 상태를 나타내는 집합
![[Pasted image 20241126152040.png]]

## Mode Management
역할에 따라 Requester, Manager, User로 나누어진다.
Requester : Manager에게 Mode를 요청
Manager/User : Mode arbitration rule을 만족하면, Manager는 User에게 Mode 변경됨을 알린다. Mode Manager, User는 요청 주체에 따라 어떤 SWC라도 될 수 있다.
![[Pasted image 20241126152432.png]]
![[Pasted image 20241126152445.png]]



# Ecu State Sequence
- 부팅 이후부터 Off / Sleep 까지의 Ecu state flow는 아래와 같이 Startup / Run / Shutdown으로 나눠진다.
- Application Inactive_Off/Sleep/Reset로 Mode 변경 시 각각의 Shutdown Sequence로 이행한다
![[Pasted image 20241126160036.png]]
![[Pasted image 20241126165434.png]]


# Mode Managment 동작
## BswM 동작
**BswM ( Basic Software Mode Manager )**
모드 변경 시 정의된 액션을 수행하도록 제공하는 모듈
![[Pasted image 20241126161510.png]]
Application 모드 정의 및 전달 과정
- **Mode Request** 방식으로 Mode 변경 요청을 수행, Mode Switch 방식으로 Mode 변경
- **Mode Request** : SWC가 Mode 요청 → Mode manager가 조건 판단, 모드 변경
- **Mode Switch** : Mode manager가 모드를 관리/변경 후 변견된 모드를 User에게 알리는 방식, Mode switch Interface를 사용하므로 1:N Conncetion

BswM Interaction
- BswM은 Rule에 기반하여 Mode Management 동작을 수행 한다. Rule은 다수의 if-else문으로 구성되어 있다고 보 수 있다.
![[Pasted image 20241129132817.png]]
- 타 SWC Mode 변경 요청 시, if 문과 같이 논리 연산자를 통해 Arbitration을 수행한다. 
![[Pasted image 20241129132856.png]]


### BswM Rute 구성 요소
- Mode Request Port : Mode Management 동작을 요구하는 주체 (if문의 변수), Immediate/Deffered 방식으로 설정 가능
- Mode Condition : Rule을 구성하는 각 논리 연산 단위 ( if문의 개별 조건 들)
- Logical Expresstion : Rule을 구성하는 논리 연산 묶음 ( if 문의 조건 묶음)
- Action List : Rule 조건 만족/불만족 시 실행하는 Action의 묶음 ( if 문의 True/False시 수행 내용),
  Condition/Trigger 방식으로 설정 가능
  Action : Action List 내의 Action들 ( if문 Ture/False시 수행하는 개별 행동)
![[Pasted image 20241129133116.png]]

### Mode Request Port 설정
- Mode Request Port 설정 시 Mode Request Processing 방식을 설정한다.
- BSW 모듈 및 SWC에서 BswM모드 변경 알림 시
	- 1. 즉시 Rule function 수행(Immediate)
	   → 같은 TASK내에서 Rule 및 Action List 수행
	-  다음 MainFunction에서 Rule function 수행한다(Deferred)
	   → 다른 TASK에서 Rule 및 ActionList 수행
### ACtionList
- Action List 설정 시 ActionList Execution 방식으로 설정한다.
- 이전 Rule의 결과를 반영할지 설정
![[Pasted image 20241129134206.png]]


Action