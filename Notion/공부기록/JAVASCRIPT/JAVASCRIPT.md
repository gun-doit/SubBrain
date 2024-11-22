> **싸피 강의  
>   
> **[https://velog.io/@saemileee/Javascript-호이스팅-클로져](https://velog.io/@saemileee/Javascript-호이스팅-클로져)  
>   
> [https://www.codeit.kr/topics/getting-started-with-javascript/lessons/3480](https://www.codeit.kr/topics/getting-started-with-javascript/lessons/3480)

**var : 재 할당 가능** `**함수 레벨 스코프**`

**let : 재 할당 가능** `**블록 레벨 스코프**`

**const : 재 할당 불가** `**블록 레벨 스코프**`

### 데이터 타입

**원시 자료형 : number, string, Boolean,** `**null**`**,** `**undefined**`

**참조 자료형 : Array, Object, Function**

`**null**` **: 값이 비어있다고 명시하는 것**

`**undefined**` **: 아무 값도 할당받지 않은 상태**

### **함수 레벨 스코프 vs 블록 레벨 스코프**

**함수 레벨 스코프 : 함수 내에서 선언된 함수는** ==**함수 내에서만 유효**==**하다.**

**블록 레벨 스코프 : 블록 { } 내에서 선언된 변수는 코드** ==**블록 내부에서만 유호**==**하다.**

  

### 호이스팅

> **인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다.**

**변수가 호이스팅 될 때에는** `**선언, 초기화**` **만 된채로 호이스팅 되고** `**할당**` **까지 호이스팅 되지 않는다. ⇒ var 변수**

**TDZ(Temporal Dead Zone) : let, const로 선언된 변수는 호이스팅 되었지만** ==**!접근만!**== **못하는 상태이다.**

  

### == vs ===

**== : Type이 달라도 True**

**=== : Type도 같아야만 True**

### Script의 위치에 따른 영향

**Head에 삽입 된 경우**

- **Script를 모두 로딩 후 브라우저 렌더링을 시작한다.**
- **페이지가 뜨는 속도가 느려 진다.**

**Body 맨 밑에 삽입 된 경우**

- **Dom Tree가 완성된 상태에서 Script가 실행된다**

  

  

### Promise

> **비동기 작업을 좀 더 편하게 할 수 있도록 ES6에서 도입  
> 콜백 방식의 콜백지옥을 보완  
> **

**new Promise((resolve, reject) ⇒ {});**

`**pending**`**상태 : 대기 상태, resolve나 reject가 실행되기 전의 상태**

`**fulfilled**`**상태 : 이행 상태, resolve 호출 시의 상태**

`**rejected**`**상태 : 실패 상태, reject 호출 시의 상태**

### Ajax (Asynchronous JavaScript and XML)

**서버와 통신하기 위해 XMLHttpRequest 객체 사용**

**비동기성으로 페이지를 새로고침을 하지 않고도 수행된다.**

  

![[Untitled 24.png|Untitled 24.png]]

  

### fetch API

> **XMLHttpRequest와 유사하나 더 발전된 API (es6 도입)  
> 객체를 Promise 형태로 반환 받는다  
> json의 타입별로 쉽게 적용 가능하다.  
> **

```JavaScript
const url = "https://jsonplaceholder.typicode.com/todos/";

fetch(url)
	.then((res) => res.json())
	.then((res) => console.log(res))
	.catch((err) => console.log(err));
```

  

### Axios

> **가장 널리 쓰이는 http 통신 라이브러리  
> Promise 형태 리턴  
> **