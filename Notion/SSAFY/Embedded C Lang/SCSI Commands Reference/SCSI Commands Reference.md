> **스카시 / 스커지 커맨드**
> 
> **컴퓨터와 주변 장치 간에 데이터 전송을 위한 표준 인터페이스**

![[Untitled 36.png|Untitled 36.png]]

- ==**LBA**== **- Longical Block Address  
    데이터 시작 위치를 나타내는 논리 블럭 주소**

### 동작 방식

1. CPU가 주변 장치로 Read(6) Command를 보낸다.
2. 주변장치가 응답한다. ( 6Byte )
    1. 6 Byte에 대한 데이터가 들어오면, 다음과 같이 파싱 해야 한다.
        1. OPERATION CODE : 8 bit
        2. Reserved : 3 bit
        3. LBA ( Logical Block Address ) : 21 bit
            1. 1번 Byte ~ 3번 Byte 까지 분포
        4. Transfer Length : 8 bit
        5. CONTROL : 8 bit

```C++
\#pragma pack(1)
		union Node{
				uint8_t ori[6];
				
				struct{
						uint8_t opcode;
						
						//LBA -> Bit 파싱
						uint8_t lba_part1 : 5;
						uint8_t reserved : 3;
						
						//LBA
						uint8_t lba_part2;
						uint8_t lba_part3;
						
						uint8_t length;
						uint8_t control;
				}field;
		}node;
```