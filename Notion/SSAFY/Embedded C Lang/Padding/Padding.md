  

```C++
struct Node{
		int a;
		char b;
}c;

printf("%d\n", sizeof(c)); //8
```

### CPU는 4byte 단위로 데이터를 읽는다

![[Untitled 37.png|Untitled 37.png]]

  

**→ 컴파일러마다 Padding을 붙이는 방식이 다르다.**

  

**패딩을 없애는 명령어**

**\#pragma pack(1)**