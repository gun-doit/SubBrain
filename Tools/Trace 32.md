Symbol - 메모리 주소에 대한 기호적인 이름
F1 : Help
### T32 Start
![[Pasted image 20241216110237.png]]
## **기능창** 
### 1. **sYmbol.Browe**
디버그 심볼을 찾아 소스레벨로 디버깅 할 수 있다.![[Pasted image 20241125111959.png]]
**![[Pasted image 20241125112248.png]]**
A : ELF(\\⁕) ⇿ 소스파일(\\⁕\⁕) ⇿ 디버그 심볼 (\\⁕\⁕\⁕, 기본)의 단계로 변환할 수 있음
B : int, void 등 원하는 형식의 디버그 심볼만 볼 수 있음
C : 함수, 변수 등 원하는 종류의 디버그 심볼만 볼 수 있음.

### 2. List.auto
어셈블리, 소스레벨로 코드를 수행하여 디버깅할 수 있다.
![[Pasted image 20241125112557.png]]
![[Pasted image 20241125112926.png]]
addr/line : 소스라인과 타깃 어드레스를 매칭
code : 기계어 코드
label : 디버그 심볼에 포함된 레이블
mnemonic : 기계어를 어셈블러로 보여줌
comment : 디버그 심볼을 변수/함수와 매칭하여 보여줌

![[Pasted image 20241125112907.png]]
Step : 어셈블리 / C 레벨로 한 스텝 진행
Over : 함수 내부로 진입하지 않고 해당 함수를 수행
Diverge : while/for 등의 반복 문을 한번에 실행
Return : 함수의 마지막 라인까지 한번에 진행
Up : 수행중인 함수를 모두 마치고 빠져 나감
Go/Break : Program 수행을 시작/중지
Mode : 어셈블리/C모드를 변환
### 3. Data.dump
![[Pasted image 20241216133111.png]]
![[Pasted image 20241216133132.png]]

- Address를 입력하여 해당 주소의 값을 확인할 수 있음![[Pasted image 20241216133246.png]]
Find : 원하는 값을 찾을 수 있음
Modify : 메모리에 특정 값으로 채우거나, 쓰기 여부 판단 할 수 있음
Long ... : 설정한 데이터 폭으로 메모리 값을 읽어옴
E : Arm-Cortex, PowerPC-NEXUS와 같은 일부 코어의 경우, 런타임 중 메모리 값 변화를 볼 수 있음.
### 4. Register.view
![[Pasted image 20241216133659.png]]
![[Pasted image 20241216133748.png]]
**코어 종류에 따라서 다르다**

대부분의 코어 레지스터는 아래와 같은 두 가지 용도로 구성된다.
- 동작 상태, 코드 수행 위치, 스택 포인터 등의 특별한 레지스터
- 연산을 위해 사용되는 일반적인 레지스터
- 코어 별 레지스터의 특성을 알면 디버깅이 용이하다.

ARM 레지스터 구성
- R0 ~ R12 : 일반적인 연산을 위한 레지스터
- R13(스택 포인터) : 사용중인 스택 어드레스를 표시
- R14(링크 레지스터) : 함수 수행 후 돌아갈 어드레스 정보
- R15(프로그램 카운터) : 현재 수행중인 어드레스 정보
- CPSR/SPSR(Current/Saved Program Status Register) : 현재/과거의 상태정보를 가지고 있음

**코어는 메모리에서 값을 레지스터로 읽어 들여, 연산을 한 후, 그 결과를 다시 메모리에 적는 동작을 반복한다.**

### 5. Var.Watch
![[Pasted image 20241216140801.png]]![[Pasted image 20241216140940 1.png]]

A : 변수 이름을 입력하여, Var.Watch창에 추가
B : 변수 이름을 찾아, Var.Watch창에 추가
C : 변수 이름을 찾아, 별도의 Var.View창을 엽니다
D : 등록된 변수를 모두 지웁니다.

### 6. Frame.View
 함수의 호출 관계를 알 수 있다.
 ![[Pasted image 20241216142928.png]]
