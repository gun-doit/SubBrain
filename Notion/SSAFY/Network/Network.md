> **Goal : Socket 통신을 이용해서 멀티 채팅이 가능한 서버 프로그램 제작**

### **Socket 통신**

- **Socket을 이용해 서버-클라이언트 간 데이터를 주고 받는 양방향 연결 지향성 통신**
- **TCP**
- **Full-Duplex**

  

### Port - 동시 다발적 통신을 위한 가상의 문

### **Socket**

**TCP/IP 기반 네트워크 통신에서 데이터 송수신의 마지막 접점**

**인터페이스 이다 → 내부 구조를 몰라도 통신이 가능하다.**

  

### IP : Internet Protocol

- **패킷 혹은 데이터그램이라고 하는 덩어리로 나뉘어 전송**
- **주소와 전송 방식 지정**
- **특징 : 비 신뢰성, 비 연결성**

  

### TCP : Transmission Control Protocol

- **전송 제어 프로토콜**
- **IP의 핵심 프로토콜 중 하나, IP의 단점을 해결**
- **연결 지향 : 3번 검증  
    SYN : 준비됨?  
    SYN-ACK : ㅇㅇ  
    ACK : 받아라!  
    **
- **특징 : 데이터 전달 보증, 순서 보증, 신뢰할 수 있는 프로토콜, 느리다.**

![[Untitled 11.png|Untitled 11.png]]

  

### 통신 방식

1. Simplex - 데이터 전송이 한 방향 ( TV )
2. Duplex - 데이터 전송이 양 방향
    
    1. Half-Duplex - 데이터가 전송될 때, 송/수신이 별도로 발생
    2. Full-Duplex - 데이터가 전송될 때, 송/수신이 함께 발생
    
      
    

### Server - Client 동작 방식

1. socket() - 소켓 생성
2. bind() - 소켓에 주소 할당
3. listen() - 클라이언트 연결 요청 대기
4. accept() - 클라이언트 연결 승인
5. read() / write() - 통신
6. close() - 소켓 닫기

  

![[Untitled 1 4.png|Untitled 1 4.png]]

  

  

## 4주차

**라우터 - 논리적, 또는 물리적 분리된 망 사이를 지나는 패킷의 위치에 따라 최적화된 루트를 지정하는 기능을 수행하는 장비**

**스위치 - 네트워크 내의 장치를 연결하고 해당 장치와 데이터 패킷을 주고 받는다.** ==**라우터와 달리 스위치는 여러 장치의 네트워크가 아닌 의도된 단일 장치로만 데이터를 전송한다.**==

  

  

### ARP : Address Resolution Protocol

- 일반적으로 LAN 환경에서는 MAC주소를 기반으로 통신한다.
- 만약 상대방의 IP주소만 알고 있고, MAC주소를 모른다면? → 이더넷 통신을 할 수 가없다. 따라서 ARP 프로토콜을 통해 IP주소로 MAC주소를 알아내야 한다.
- **동작방식**
    1. 데이터를 보내고자 하는 노드에서 전체 브로드캐스팅
    2. 만약, Target이 나를 찾는 다는 것을 알게 되면 Target Node는 MAC 주소를 담아 응답한다.
    3. 이제 그 IP주소와 MAC주소를 테이블화 해서 데이터 전달
- **단점**

> **ARP를 받으면 NIC가 아닌 CPU가 처리한다.**
> 
> 1. ARP Request 발생 시
>     1. 각 NIC들이 해당 MAC주소를 받는다
>     2. Interrupt 발생
>     3. 자신의 IP주소와 일치하는 지 확인한다.
>     4. 자신의 IP주소와 일치하면 Response을 한다.
> 2. 스위치를 써서 막을 수 있는 것 → ==**콜리젼**== 차단
> 3. 스위치를 써도 못 막는 것 → ARP로 인한 PC들의 성능 저하
> 4. ARP ==**스푸핑**== 공격 → ARP 패킷을 조작하여, 데이터 가로채기

  

### Router의 필요성

**PC가 많을수록 브로드캐스팅이 자주 발생**

- 브로드 캐스팅 신호 끼리 콜리젼 발생 가능성 높아짐
- 콜리젼이 많이 발생할 수록 통신 지연 발생
- ARP Request가 많아짐 → 잦은 Interrupt로 PC도 느려진다.

**네트워크 분할 필요**

- 브로드캣흐트 영역을 라우터를 이용하여 분할한다.

**스위치와 달리 라우터는 복합한 Firmware (OS Level)로 동작한다.**

  

**라우터의 역할**

1. Gateway : 서로 다른 네트워크 통신 목적
2. 브로드캐스트 영역을 나누기 위함
3. 라우터끼리 연결 되어 있을 때, 지능적으로 배정 가능
4. WAN을 통해 외부 인터넷 연결