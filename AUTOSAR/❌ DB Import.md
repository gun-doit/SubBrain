
출처 
[AUTOSAR CAN : DB Import, Configuration & Generation : 네이버 블로그](https://m.blog.naver.com/techref/222435476591)
[AUTOSAR CAN 통신 스택 : AUTOS.. : 네이버블로그](https://blog.naver.com/mdstec_auto/222070210412)
# DB Import란?
플랫폼에서 DB내에 저장된 각각의 메시지들을 프로젝트의 **각 객체로 파싱**해주는 작업을 말한다.  ARXML파일 뿐 아니라 CAN/LIN/Flexray/Ethernet등의 데이터베이스 혹은 엑셀 형식으로 저장된 파일을 drag-drop 방식으로 끌어와서 간편하게 ARXML 형태도 만들어주는 기능을 제공할 뿐 아니라, import한 데이터를 모듈들의 의존성을 고려해서 자동으로 설정해주는 기능도 제공한다.

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
#### 1. Rebuild
$에러가 없는 상태임을 확인한다. Build없이 진행하면 DCM, DEM 등 연결이 끊어지는 경우가 발생할 수 있다
#### 2. 기존 DB를 삭제 후 저장
#### 3. 새로운 DB를 Import
- Select ECU
- PNC 확인 - 1, 108, 122
- Diag 확인 - GST_ALL, GST_RCM, GST
- CAN Cluster
- ![[Pasted image 20241231104247.png]]
#### 4. BswM을 제외한 모든 모듈 Harmonize
#### 5. Mcal/Can/Hardware Object/Hw Object Count 1로 설정
#### 6. BswM을 제외한 모듈 모듈 Generation
- Ecud_BswM.arxml / Swcd_Bsw_bswM.arxml 내용 삭제
- Dummy BswM Harmonize
  BswM만 선택하여 Harmonize 한다
  ![[Pasted image 20241231104709.png]]
  ![[Pasted image 20241231104718.png]]
  각각 두번 진행
- BswM 제외하고 Generate
  Scons/RTSW/Generation/BswM/Used -> false로 하고 진행한다.
