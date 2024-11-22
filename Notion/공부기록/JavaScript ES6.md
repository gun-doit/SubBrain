### **ECMAScript6(ES6)**

**Ecma International이 기술 규격에 따라 정의하고 있는 표준화된 스크립트 프로그래밍 언어**

**큰 변화가 일어난 시기 2015년에 ECMAScript6 이하 ES6**

  

### Block Scope 블록스코프

```C++
<script>
var x = 1;
var x = 100;
console.log(x); => 100이라고 뜸

let y = 1;
let y = 100; => 동일 변수 생성 x 


var x = 1;
if(ture) {
	var x = 200;
	console.log(x); => 200
}
console.log(x); => 200

// let 변수의 유호범위 {}블록이다.
let z = 1;
if(true){
	let z= 100;
	console.log(z); => 100
}
console.log(z); 
</script>
```