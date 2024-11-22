**자료구조** **[[링크]](https://bnzn2426.tistory.com/115)**

- [ ] **Array**
- [ ] **Stack**
- [ ] **Queue**
- [ ] **Singly-Linked List**
- [ ] **Doubble-Linked List**
- [ ] **Skip List**
- [ ] **Hash Table**
- [ ] **Binary Search Tree**
- [ ] **Cartesiuan Tree**
- [ ] **B - Tree**
- [ ] **Red-Black tree**
- [ ] **Splay tgree**
- [ ] **AVL Tree**
- [ ] **KD Tree**

  

[[Linked-List]]

  

  

### Array

> **Array는 연관된 데이터를** ==**메모리상에 연속적**==**이며 순차적으로** ==**미리 할당된 크기**==**만큼 저장하는 자료구조**

특징 : 고정된 저장공간 ( fixed-size ), 순차적인 데이터 저장 (order)

Operation :

|   |   |   |   |
|---|---|---|---|
|**조회**|**O(1)**|**삽입**|**O(n)**|
|**추가**|**O(1)**|**삭제**|**O(n)**|
|**삭제**|**O(1)**|**탐색**|**O(n)**|

**장점 : 조회, 추가가 빠르다. → 조회를 자주 해야되는 작업에서는 Array를 자주 쓴다.**

**단점 : fixed-size 특성상 선언시 미리 크기를 정해야한다. → 메모리 낭비나 추가적인 overhead가 발생할수 있다.**

**vs Linked List**

- **메모리에 저장되는 방식과 이에 따른 operation의 연산속도(complexity)가 다르다.**

  

### Dynamic Array → Vector

> ==**Array의 fixed-size의 한계점을 보완**==**하고자 고안된 자료구조**

**resize 방법:**

**C ++ - Vector : Double ( 기존 사이즈의 2배를 할당 ) ⇒ O(n)**

  

> **분할상환 시간 복잡도 : Amortized time complexity**

- **데이터를 추가할때 resize는 자주 발생하지 않으므로 결론적으로 O(1)임**

  

**vs Linked List**

**장점 : 접근(O(1)으로 빠르다.**

**단점 : 중간에 insert or remove 할때 느리다, 연속적으로 저장되어 있기때문에**

**resize를 해야할때 예상치 못하게 현저히 낮은 performance가 발생한다.**

**필요 이상의 memory 공간을 할당 받는다**

  

### Linked List

> **Linked List는** ==**Node라는 구조체**==**로 이루어져 있는데, Node는 데이터 값과 다음 Node의 address를 저장합니다. Linked List는** ==**물리적인 메모리상에서는 비연속적**==**으로 저장되지만 Linked List를 구성하는 각각의 Node가 다음** ==**Node의 address를 가리킴으로 논리적인 연속성**==**을 가진 자료구조**

- **Tree, graph등 다른 자료구조를 구현할 때 자주 쓰이는 자료구조, 추가할때 메모리를 할당하기 때문에 메모리 관리 Good**

|   |   |   |   |
|---|---|---|---|
|**조회**|O(n)|**삽입**|O(1)|
|**추가**|O(n)|**삭제**|O(1)|
|**삭제**|O(n)|**탐색**|O(n)|

  

### Queue

> **선입선출 FIFO(FIrst In First Out)의 자료구조. 삽입, 삭제의 시간복잡도가 O(1) 활용 예시는 Cache구현, 프로세스 관리, 너비우선탐색**

**구현방식**

- **Array-Base queue : enqueue, dequeue 과정에서 남는 메모리가 생긴다. 따라서 메모리 낭비를 줄이기 위해 주로 Circular queue형식으로 구현한다.**
- **List-Baseed : 재할당이나 메모리 낭비의 걱정을 할 필요가 없다.**

  

**확장 → deque, priority queue**

**활용예시 → 공유 프린터, Cpu task scheduling, Cache 구현, BFS**

  

### Stack

> **후입선출 LIFO(Last In First Out)의 자료구조, 삽입, 삭제의 시간복잡도가 O(1), 활용 예시는 call stack,후위 표기법 연산, 괄효 유호성 검사, 웹 브라우저 방문기록(뒤로 가기), DFS**

  

  

### Stack → Queue

### Stack → Queue

```Python
class Queue(object):
	def __init__(self):
		self.instak=[]
		self.outstack=[]
	
	def enqueue(self,element):
		self.instack.append(elemnet)
	
	def dqeue(self):
		if not self.outstack:
			while self.instack:
				self.outstack.append(self.instack.pop())
		return self.outstack.pop()
```

- **enqueue() : instack.push()를 한번만 하면 되기 때문에 O(1)입니다.**
- **dequeue() : 두 가지 경우를 따져봐야 합니다. worst case는 outstack이 비어있는 경우 입니다. 이 때는 instack에 있는 n개의 데이터를 instack.pop()을 한 이후에 outstack.push()를 해줘야 합니다. 따라서 총 2*n번의 operation이 실행되어야 하므로 O(n)입니다.  
    하지만 outstack이 비어있지 않은 경우에는 outstack.pop()만해주면 됩니다. 이는 O(1)의 시간복도를 가지므로 amortized O(1)의 시간복잡도를 갖습니다.  
    **

  

### Queue → Stack

**Stack → Queue와 유사하다**