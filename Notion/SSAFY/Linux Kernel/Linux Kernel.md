# **부트로더**

> **부팅 시 동작 되는 프로그램**

**==Disk에 저장되어 있는 운영체제를 실행==** **시키는 역할**

### **역할**

1. **다중 OS부팅**
2. **장치 제어 및 테스트**
3. **부팅 옵션 관리**
4. **하드웨어 초기화**

  

OS별 부트로더

Ubuntu : GRUB2 ( GNU GRand Unified Bootloader )

Window : Bootmgr

ARM : Opensource U-Boot

  

### GRUB의 기능

Low Level에서 메모리, 파일시스템 접근 가능

시스템에서 텟그트활 수 있는 다양한 기능

→ 실제 메모링 값 쓰고 읽기

  

  

## CMOS 와 BIO**S**

> **CMOS**

**CMOS Chipset, 비휘발성 메모리**

**컴퓨터의 설정 정보를 저장함( 메모리 크기, 부팅 순서, H/W 구성 정보 등)**

**베터리 전원을 사용한다**

**BIOS로 설정 정보를 수정할 수 있다**

  

> **BIOS**

**기본적인 I/O 를 위한 Firmware**

**컴퓨터 부팅 시 BIOS가 동작**

**BIOS는 CMOS에 저장된 부팅 설정 정보를 읽어와서 부팅한다.**

**CMOS는 설정 값들을 변경 가능하다.**

**요즘은 UEFI로 대체됨**

  

  

## **POST**

> **Power-on self-test**

**BIOS에서 Power를 켜자마자 주변장치를 검사하는 과정**

**BIOS가 POST를 하고 있을 떄, Log Message가 출력됨**

![[Untitled 14.png|Untitled 14.png]]

  

## UEFI

> **Unified Extensible Firmware Interface : 통일 확장 인터페이스**

BIOS를 대체하는 Firmware

화려한 그래픽, UI / 2.2TB이상 디스크 사용을 위한 GPT ( GUID Partition Table ) 지원

![[Untitled 1 6.png|Untitled 1 6.png]]

  

  

## U-Boot

> **Univarsal Boot Loader**

**임베디드 리눅스 개발에 가장 많이 쓰이는 Opensource Bootloader**

**리눅스 및 다른 운영 체제를 실행하는 임베 디드 시스템의 부팅 프로세스를 관리**

**USB, TCP/IP, Flash 제어 가능**

  

**특징**

1. **포팅 가능성**
2. **부트로더 역할**
3. **디버깅 및 테스트**
4. **네트워크 부팅 등등**

  

  

## PC계열과 ARM 차이

**x64_86**

0 단계 : ROM 로드

1 단계 : BIOS or UEFI

2 단계 : Bootloader (GRUB)

리눅스 커널 실행

  

**ARM**

0,1 단계 : 칩셋 사 제공

2 단계 : Bootloader ( u-boot )

리눅스 커널 실행

  

  

# **디바이스 드라이버**

H/W 장치를 추가하거나 수정, 교체 되면 app을 수정해야한다.

→ 커널 재 빌드 → 시간이 너무 오래 걸림

“커널 모듈 형식”의 디바이스 드라이버를 만들고 수정된 app과 디바이스 드라이버를 이용해 장치 테스트를 한다.

![[Untitled 2 3.png|Untitled 2 3.png]]

  

### Device File ( 장치 파일 )

c : character device file

b : block device file

  

**Major Number ( 주번호 )**

- 기기 종류를 나타냄
- 같은 기능을 하는 디바이스가 여러 개 있다면, 같은 주번호를 가짐

  

**Minor Number ( 부번호 )**

- 같은 종류 device 에서 구분 용도
- 개발자 마음대로 의미 부여 가능
- blkdev에서는 파티션 번호로 사용
- node 이름에서 숫자가 붙은 경우 부번호를 의미

  

[[모듈 프로그램]]