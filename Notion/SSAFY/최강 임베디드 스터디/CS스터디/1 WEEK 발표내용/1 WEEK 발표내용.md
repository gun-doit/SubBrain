## 메모리 구조, 시간 복잡도, STL(vector, list)
![[Untitled 47.png|Untitled 47.png]]]]![[Untitled 1 21.png|Untitled 1 21.png]]ng]]

[**EIP 레지스터**](https://blog.naver.com/sthellfire/220639968366) **( Extended Instruction Pointer ) = 확장된 명령 지시자**==**계산밖에 할줄 모르는 순진한 CPU에게 해야 할 일이 어디 있는지 알려주는 하나의 빛줄기 같은 존재**==

**데이터 영역 - 전역변수와 정적 변수, 문자열 상수가 저장된다.**

**스택 영역 - 함수의 호출과 관계되는 지역변수, 매개변수, 리턴값이 저장되는 영역**

### 1. 텍스트(코드) 세그먼트

- **실행할 프로그램의 코드가 저장되는 영역, 명령 실행 순서는 순차적이지는 않다.  
    그 이유는 하이레벨의 언어 제어구조가 어셈블리어의 branch, jump, call 등으로 변형되기 때문에, 프로그램이 실행되면 EIP 레지스터는 텍스트세그먼트의 맨 처음 위치로 설정하게 된다.  
    CPU는 코드 영역에 저장된 명령어(  
    **==**주소**==**)를 하나씩 가져가서 처리하게 된다.**

### 2. 데이터 세그먼트

- **전역변수와 정적변수, 문자열 상수가 저장되는 데이터 공간**
    - **BSS ( Block Stated Symbol ) - 초기화 되지 않은 변수들이 저장되는 공간  
        통상적으로 컴파일 타임에는 메모리만 잡아놓고 초기화하지 않음, 프로그램 로더가 프로그램을 로드할 때 값이 초기화된다.  
        **
        - [**장점**](https://velog.io/@rlooo/%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%98%81%EC%97%AD-Code-Data-Heap-Stack)**  
            1. 메모리 사용 효율성 - Rom, Ram ??.. 아직 잘 모르겠숩니다..  
            2. 프로그램 실행 속도 향상  
            **
    - **rodata - 문자열 상수 저장 주소값이 같음 - 하지만 컴파일러 및 링커의 동작에 따라 다를수도 있다 by GPT**
    - **data - 0 이외의 값으로 초기화된 전역 변수 또는 정적변수**

```C++
int n;
int k = 10;

void foo(){
	return 0;
}

int main(){
	int num;
	const char s = "hello world";
	const char* s1 = "hello world";
	
	vector<int> v;
	vecotr<int> *v = new vector<int>;
	int *arr =![[Untitled 2 8.png|Untitled 2 8.png]] 0![[Untitled 3 5.png|Untitled 3 5.png]]led 2 8.png]]

![[/Untitled 3 5.png|Untitled 3 5.png]]

[**전역변수를 선언한다면, 초기화를 하지 않는 것이 좋다**](https://gusdnd852.tistory.com/16)

  

```C++
int arr[N];
int *arr = new arr[N];
```

### 동적할당이란? ( Dynamic Allocation )

- **입력되는 데이터에 맞게 기억공간을 확보 하는 것**

### 정적할당이란? ( Static Allocation )

- **프로그램을 작성하는 단계에서 기억공간의 크기를 결정하는 것**

  

  

## 시간 복잡도

**효율적인 방법을 고민한다는 것은 == 시간 복잡도를 고민한다는 것**

**Big-O(빅-오) ⇒ 상한 점근  
Big-Ω(빅-오메가) ⇒ 하한 점근  
Big-θ(빅-세타) ⇒ 그 둘의 평균  
**

[STL](https://modoocode.com/223)

스퀀스 컨테이너, 연관 컨테이너

  

## Iterator [[링크]](https://eehoeskrap.tistory.com/263)

- **포인터와 상당히 비슷하며, 컨테이너에 저장되어 있는 원소들을 참조할 때 사용한다.**

> **성질**

1. 컨테이너와 컨테이너 안의 있는 요소를 구별
2. 요소의 값 확인
3. 컨테이너 안에 있는 요소들 간에 이동할 수 있는 연산 제공
4. 컨테이너가 효과적으로 처리할 수 있는 방식으로 가용한 연산들을 한정

## **시퀀스 컨테이너 - vector, list, deque, forward_list**

- 데이터를 선형으로 저장하며, 특별한 제약이나 규칙이 없는 가장 일반적인 컨테이너. 정렬 X

> **iterator - 반복자**

- 포인터와 비슷하며, 컨테이너에 저장되어있는 원소들을 참조할 때 사용

### Vector

- 벡터는 포인터 세 개로 구현되어 있다.
    - 할당된 배열의 시작 주소를 가리키는 포인터 - begin, rend-1
    - 다음에 데이터가 삽입될 위치를 가리키는 포인터 - size , end-1, rbegin
    - 할당된 배열의 끝 주소를 가르키는 포인터 - capacity

> **사용법**

```C++
vector<int> v;
vector<int> v(5); // 0으로 초기화된 5개의 원소를 가짐
vector<int> v(5,2); // 2로 초기화된 5개의 원소를 가짐
vector<int> v2(v); // v를 복사한 v2

//참조
v.at(idx) vs v[i] // at은 outopbound 에러 발생

//추가
v.push_back(요소); O(1) or O(n)
v.insert(위치, 요소) or v.insert(위치, 갯수, 요소); O(n)

//제거 
v.pop_back(요소); O(1)
v.erase(iter); -> iter가 가리키는 원소를 제거 O(n)
v.clear() -> O(n)

//참조
v.front();
v.back();

v.begin() // iter와 사용
v.end(); //마지막의 다음
v.rbegin();
v.rend();



swap 등등..
```

```C++
2ㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈ
ㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈㅈ22222222222222222222222ㅈㅈㅈㅈㅈㅈ2ㅈ

\qㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂㅂ제가 생각하기엔 무조건 좋음
//empace_back, push_back
class Item {
public:

 Item(const int _n) : m_nx(_n) { cout << "일반 생성자 호출" << endl; }

 Item(const Item& rhs) : m_nx(rhs.m_nx) { cout << "복사 생성자 호출" << endl; }

 Item(const Item&& rhs) : m_nx(std::move(rhs.m_nx)) { cout << "이동 생성자 호출" << endl; }

 ~Item() { cout << "소멸자 호출" << endl; }
 
 private:
 int m_nx;
};

int main() {
 std::vector<Item> v;

 cout << "push_back 호출" << endl;
 v.push_back(Item(3));
 
 cout << "emplace_back 호출" << endl;
 v.emplace_back(3);

}

//push_back일 경우
//일반 생성자 호출
//이동 생성자 호출
//소멸자 호출
//소멸자 호출

//emplace_back인 경우
//일반 생성자 호출
//소멸자 호출
```

by GPT

> **장점**

1. 성능 최적화 : 객체를 직접 생성하므로 복사 생성자 호출을 피할 수 있음.
2. 객체 생성 시 복잡한 초기화 - 로직을 직업 전달하기에 간결함 but 이건 의미없는듯.

> **단점**

1. 직관성
2. 단순한 타입 - 성능차이 x
3. 초기화 리스트가 없는 경우 : emplace_back은 생성자의 매개변수를 통해 객체를 생성하는데 만약 객체를 생성하는데 객체가 초기화 리스트를 지원하지 않는 경우 사용할 수 없음.

[[링크]](https://openmynotepad.tistory.com/10)

## **삽입 주의사항**

push_back은 상수 시간복잡도를 가지지만 배열이 전부 찰경우 vector에 할당하는 reallocation이 발생해 시간이 많이 소요된다.

  

### list, forward_list

- Linked list
- random access 불가능.

> **차이점**

List는 더블 링크드 리스트 →  
forward_list는 싱글 링크드 리스트 → 맨 앞에 데이터를 삽입하는 건 빠르지만 맨 뒤는 느림  

```C++
//list
push_back O(1)
pop_back O(1)
push_front O(1)
pop_front O(1)

insert(iter, value) O(1)
erase(iter-first, iter-last) O(범위)
clear() O(n)
splice() O(1)


//forward_list
push_back O(1)
pop_back O(1)

insert_after(iter, value) O(1)
erase_after(iter) O(1)
erase_after(iter-first, iter-last) O(범위)
clear() O(n)
splice_after() O(1)

merge()
reverse() O(n)


//advance -> iter 반복자를 특정 거리만 큼 전진 후진 시키는 것
```

### Deque

> **사용법**

```C++
push_back O(1)
pop_back O(1)
push_front O(1)
pop_front O(1)

//O(1)
at()
[]
front()
back()
size()
empty()


//O(n)
clear()
insert(iter,value)
erase(iter)
erase(iter-first, iter-last)
resize(n)
```