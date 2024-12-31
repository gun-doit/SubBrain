
출처 
[AUTOSAR CAN : DB Import, Configuration & Generation : 네이버 블로그](https://m.blog.naver.com/techref/222435476591)
# DB Import란?
플랫폼에서 DB내에 저장된 각각의 메시지들을 프로젝트의 각 객체로 파싱해주는 작업을 말한다. CAN DB파일인 DBC 파일을 AUTOSAR에서 사용 가능한 .arxml 형식으로 변환한다.


# ECU Configuration & Generation
**ARXML** 형태로 변환된 CAN DB 정보가 BSW 모듈에 자동으로 반영되는 모듈은 아래와 같다.
- Can : CAN 채널과 메시지, 시그널 설정
- CanIf : CAN 채널과 메시지, 시그널 설정
- CanSM : CAN 채널 설정
- CanTp : TP 채널과 Tp용 PDU설정
- PduR : CAN 메시지에 대응되는 PDU에 대한 Routing Table
- COM : PDU, 시그널 설정
- EcuC : PDU Reference 설정
- ComM : CAN 채널 설정
- Nm : Nm 채널 설정
- BswM : CAN 채널 제어에 대한 설정
![[Pasted image 20241231102904.png]]


1. 플랫폼에서 DB import란  DB내에 저장된 각각의 메시지들을 프로젝트의 각 객체로 파싱 해주는 작업
2. 관련파일
	1. Configuration > System > Composition > EcuExtgracct.axrml
	2. Configuration > ECU > ECUCD_EcucValueCollection.arxml
3. 기존 DB 삭제



## DB Import 연습 RCM_R440
**target 1129**
1. Rebuild
	1. 
2. 