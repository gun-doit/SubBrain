### **문자열**

1. **const char *v = “ABCD”** `==**읽기전용**==`
2. **char v[10] = “ABCDE”**

### **다중 문자열**

1. **const char *vs[3] = { “ABCDE”, “BTS”, “KK”};** `==**읽기전용**==`
2. **char vs[3][10] = { “ABCDE”, “BTS”, “KK”};**

  

- `**Size_t**` **자료형**
    
    **Size_t는 해당 시스템에서 어떤 객체나 값이 포함할 수 있는 최대 크기의 데이터를 표현하는 타입으로 반드시** `**unsigned**` **형으로 나타낸다.**
    
    > [!important]  
    > size_t can store the maximum size of a theoretically possible object of any type [C99 원문]→ size_t는 어떤 유형의 이론적으로 가능한 객체의 최대 크기를 저장할 수 있습니다  
    
    **명세에 따르면 x86은 32비트, x64는 64비트 변수가 된다.**
    

  

> `==**Size_t**==` **strlen(const char* str);**
> 
> - **문자열의 길이를 반환한다.**
> - **널문자를 만날 때까지 진행.**

  

> `**char***` **strcpy(char *dest, const char *src);**

- **문자열을 복사 ⇒ dest에 src값 복사**

  

> **`char*`** **strncpy(char *dest, const char *src, size_t n);**
> 
> - **문자열 n개 복사한다 ⇒ dest에 src값 n개 복사**

  

> `**char***` **strcat(char *dest, char, const char *src);**
> 
> - **문자열을 이어 붙인다 ⇒ dest에 src이어 붙이기**

  

> **`char*`** **strncat(char** **_dest, const char_** **src, size_t n);**
> 
> - **문자열 n개 이어 붙인다 ⇒ dest에 src n개 이어 붙이기**

  

> **`int`** **strcmp(const char* str1, const char* str2);**
> 
> - **두 문자열을 비교한다⇒ str1, str2를 비교**
> - **같으면 0, 앞서면 -1, 뒤라면 1**

  

> **`int`** **strncmp(const char* str1, const char* str2, size_t n);**
> 
> - **두 문자열 n개 비교한다.**

  

> **`int`** **sscanf(const char* str, const char* format, …);**
> 
> - **문자열에서 형식화된 데이터를 읽어온다.**

  

> **`int`** **sprintf(char *str, const char *format…);**
> 
> - **형식화된 데이터를 문자열로 저장한다.**

  

> **`int`** **atoi(const char * str)**
> 
> - **문자열을 정수로 변환한다.**

  

> **`char*`** **strtok(char *str, const char* delim)**
> 
> - **문자열을 지정된 구분자을 토큰으로 분리한다. split**
> - **return : 찾은 토큰을 가르키는 포인터를 반환, 토큰이 없으면 NULL**
> 
> ```C++
> char temp[30] = "AA\#BB\#CC";
> 
> char *p = strtok(temp, "#");
> p = strtok(NULL, "#");
> p = strtok(NULL, "#");
> ```

  

> **`char *`** **strchr(const char* str, int c)**
> 
> - **문자열에서 문자 찾기**
> - **int c : ASCII 코드값**
> - **return : 그 위치의 포인터, 없으면 NULL**

  

> **`char*`** **strstr(const char* str1, const char* str2)**
> 
> - **문자열에서 문자열 찾기**
> - **대소문자 구분**
> - **return : 그 위치의 포인터, 없으면 NULL**