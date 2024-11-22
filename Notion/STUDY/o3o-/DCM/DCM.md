> **Diagnostic Communication Manager**

**AUTOSAR 진단 기능을 담당하는 모듈은 Dcm, Dem, Det로 구성  
Dcm은 AUTOSAR Stack 중 Communication Services Layer에 속하며 진단 서비스의 Request에 대한 서비스 처리 및 Response를 담당한다.  
![[image 34.png|image 34.png]].png]]

### Dcm이란

- Data Flow와 State를 관리하며 진단기의 진단 요청 수행을 한다.
- Reset, Session 등 상태 변경을 BswM에 요청한다.
- Full-, Silent-, No-Communication 상태 등을 ComM에 요청한다.
- DTC (Diagnostic Trouble Code) 정보를 Dem에 요청한다.
- PduR을 통해 진단 데이터를 전송한다.

  

#![[image 1 11.png|image 1 11.png]]png|image 1 11.png]]

  

#![[image 2 10.png|image 2 10.png]] 2 10.png|image 2 10.png]]