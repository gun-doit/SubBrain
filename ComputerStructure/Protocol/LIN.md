- **참조 링크**
    
    > [!info] LIN 통신의 개요  
    > 자동차는 점점 더 상품성이 증가하고, 안전해지고, 기능이 많아지는 방향으로 진화하고 있으며, 이에 따라 .  
    > [https://blog.naver.com/PostView.naver?blogId=lagrange0115&logNo=222657181251](https://blog.naver.com/PostView.naver?blogId=lagrange0115&logNo=222657181251)  
    
    > [!info] LIN통신 프로토콜 - Master Slave 통신, Schedule 테이블  
    > LIN 통신 프로토콜 임베디드 SW를 개발하면서 LIN 통신 모듈을 개발해야 하는 상황이라면 이번 글이 많은 도움이 될 것이라 생각합니다.  
    > [https://cookbook.tistory.com/60](https://cookbook.tistory.com/60)  
    

### 주요특징

① 단일 마스터 / 다중 슬레이브

② UART와 SCI 인터페이스 기반 저비용 실리콘

③ 셀프 동기화

④ 신호전송 지연시간 보장

⑤ 데이터 프레임의 가변길이 : 2, 4, 8 바이트

⑥ 데이터 체크섬 보안 및 오류 감지

⑦ 재구성 가능

⑧ 단일와이어 + 접지신호(VBAT, GND, LIN(9V - 18V))

⑨ 종료 : 마스터 1K옴 / 슬레이브 30k옴

  

## 1. LIN 네트워크 구성

![[image 28.png|image 28.png]]

  

## 2. LIN 통신 방식

![[image 1 7.png|image 1 7.png]]

### 규격

master 노드가 보내는 Heade놔 Slaver 노드가 보내는 Respons로 구성된다.

### 사용목적

데이터의 양이 적고 고속통신이 필요하지 않는 Unit간의 통신

![[image 2 7.png|image 2 7.png]]

### 형태

1. **Header만 보내는 경우 → Slave의 상태를 물어볼 때 주로 쓰임**
2. **Header와 Response를 같이 구성해서 전송하는 경우 → Slave에게 명령을 할 때 주로 쓰임**

==**⇒ LIN Frame의 Response 부분은 Master와 Slave노드가 둘 다 채울 수 있는 것이다.**==

  

### LIN Schedule 테이블

Schedule이란?  
  
**Master 노드가 Slave들에게 LIN Frame을 전송하기 위해서 LIN Frame 주기에 대해서 미리 지정한 테이블**

**⇒ 프레임 전송 충돌을 방지하기 위해서 전송 타이밍을 Schedule 테이블로 만든다.**

**⇒ 여러 개의 테이블이 있는 경우는 Slave 노드들이 각각의 시스템 측 제품일 수 있기 때문이다.**

### 특징

1. Single Master / Multi Slave
2. Common UART(SCI) Interface : 비동기 직렬 통신
3. 저가의 Single-wire, 최대 20kbps
4. 전송 byte의 선택
5. 타임트리거 방식

  

![[image 3 7.png|image 3 7.png]]

Break Filed - 새로운 프레임의 개시 신호로 사용, 적어도 13bit 이상의 도미넌트 값(0)이 연속하게 되어 있음

Sync Field - 값은 0x55, Slave node에서는 이 값을 가지고 Baud rate detecting

Id Field - 0~59는 신호를 운반하는 프레임에 사용, 60,61은 진단 데이터를 운반하기 위해 사용, 62,63은 Reserved

Data Field - 1~8 byte 전송 가능

CheckSum Field - Classic checksum : LIN1.3에서 사용, 데이터 부분만 All sum / Enhanced checksum : LIN 2.x에서 사용, PID + 데이터 부분 All sum

  

  

## 역할

- 현재 선택된 스케줄 실행 : ECU가 연결 된 LIN 버스에서 마스터 노드로서 선택된 스케줄을 실행합니다.
- 스케줄 테이블 전환 : 상위 계층에서 요청할 때 마스터 노드의 스케줄 테이블을 전환
- 프레임 전송 요청 처리 : 상위 계층에서 프레임 전송 요청을 수락하고, 적절한 LIN 프레임 내에서 응답
- 프레임 수신 알림 : 적절한 프레임 내에 해당 응답이 수신되면 상위 계층에 프레임 수신을 알림
- 슬립 모드 및 웨이크업 서비스 : LIN 네트워크가 슬립 모드에 들어가거나 웨이크업할 수 있도록 서비스 제공
- 에러 처리 : LIN 통신 과정에서 발생하는 에러를 관리하고 처리
- 진단 전송 계층 서비스 : 진단 목적으로 LIN 전송 계층 서비스를 제공
- 슬레이브 노드의 노드 구성 및 식별 서비스 : 각 슬레이브 노드의 구성 및 식별 서비스를 수행

  

- **약어 및 축약어**
    
    이 문서에서는 **ISO 17987 LIN** 규격에서 사용된 약어 및 축약어 외에도 아래와 같은 약어와 축약어를 사용합니다. 일부 용어는 문서에서 자주 사용되므로 이해를 돕기 위해 다시 정의되었습니다.

|                    |                                                                 |
| ------------------ | --------------------------------------------------------------- |
| 약어/축약어             | 설명                                                              |
| **CF**             | LIN TP에서의 연속 프레임 (Consecutive Frame)                            |
| **FF**             | LIN TP에서의 첫 번째 프레임 (First Frame)                                |
| **ID**             | 식별자 (Identifier)                                                |
| **LDF**            | LIN 설명 파일 (LIN Description File)                                |
| **LIN TP (LinTp)** | LIN 전송 프로토콜 (LIN 인터페이스의 일부)                                     |
| **MRF**            | 마스터 요청 프레임 (Master Request Frame)                               |
| **NAD**            | 노드 주소 (Node Address). LIN의 각 슬레이브는 고유 NAD를 가져야 함                |
| **NC**             | 노드 구성 (Node Configuration)                                      |
| **N_As**           | 송신 측에서 LIN 프레임(N-PDU) 전송 시간 (ISO 17987-2 참조)                    |
| **N_Cr**           | 다음 연속 프레임 N-PDU 수신까지의 시간 (ISO 17987-2 참조)                       |
| **N_Cs**           | 다음 연속 프레임 N-PDU 전송까지의 시간 (ISO 17987-2 참조)                       |
| **P2**             | LIN 버스에서 진단 요청의 마지막 프레임을 수신하고 슬레이브 노드가 응답 데이터를 제공할 수 있을 때까지의 시간 |
| **P2***            | 응답 대기 프레임(0x78)을 송신하고 LIN 슬레이브가 응답 데이터를 제공할 수 있을 때까지의 시간        |
| **PID**            | 보호된 ID (Protected ID)                                           |
| **RX**             | 수신 (Reception)                                                  |
| **SID**            | 서비스 식별자 (노드 구성 서비스의 식별자)                                        |
| **SF**             | LIN TP에서의 단일 프레임 (Single Frame)                                 |
| **SRF**            | 슬레이브 응답 프레임 (Slave Response Frame)                              |
| **SRS**            | 소프트웨어 요구 사항 명세서 (Software Requirement Specification)            |
| **TX**             | 송신 (Transmission)                                               |


  

  

> [!info] LIN통신 프로토콜 - Master Slave 통신, Schedule 테이블  
> LIN 통신 프로토콜 임베디드 SW를 개발하면서 LIN 통신 모듈을 개발해야 하는 상황이라면 이번 글이 많은 도움이 될 것이라 생각합니다.  
> [https://cookbook.tistory.com/60#google_vignette](https://cookbook.tistory.com/60#google_vignette)