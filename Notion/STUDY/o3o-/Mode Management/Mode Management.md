**Mode : ECU의 상태를 나타내는 집합**

역할에 따라 ==Requester, Managerm, User==로 나뉜다.

OSEK OS의 TASK는 basic, extended 두 가지의 형태가 있다. 이 중 basix task의 state diagram은 아래와 같![[image 35.png|image 35.png]].png]]

여기서 suspended, read, running은 TASK의 상태이다.  
activate, start, preempt, terminate와 같은 동작을 Mode라고 할 수 있다.  

  

Rqeuester : Manager에게 Mode를 요청한다.

Manager/User : Mode arbitration rule을 만족하면, Manager는 User에게 Mode 변경됨을 알린다.

Mode Manager, User는 요청 주체에 따라 어떤 SWC라도 사용할 수 있다.

  
![[image 1 12.png|image 1 12.png]]12.png![[image 2 11.png|image 2 11.png]]e 2 11.png|image 2 11.png]]

  

### Ecu State Sequence

부팅 이후부터 Off/Sleep 까지의 Ecu state flow는 아래와 같이 Startup/Run/Shutdown으로 나뉜다.

Application Inactive_Off/Sleep/Reset로 Mode ![[image 3 10.png|image 3 10.png]]
![[/image 3 10.png|image 3 10.png]]