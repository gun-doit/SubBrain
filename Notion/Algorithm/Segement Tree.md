> **특정 구간 (합, 곱, 차, 나눗셈) 을 빠르게 구할 수 있는 방법t**

### 시간 복잡도 :$O(logN)$﻿

구간합을 구하는 알고리즘

구간합은 → 합배열 이 있는데 왜? → 데이터가 업데이트 되야한다.

단계

1. 트리 초기화하기

동작

1. 구간 합 트리 생성하기

```C++
int init(int start, int end, int node) {
		if(start == end) return tree[node] = a[start];
		int mid = (start + end) / 2;
		
		return tree[node] = init(start,mid, node*2) + init(mid+, end, node*2 + 1);
}
```

1. 구한 합을 구하는 함수

```C++
//start : 시작 인덱스, end : 끝 인덱스
// left, right : 구간 합을 구하고자 하는 범위
int sum(int start, int end, int node, int left, int right){
		if(left > end || right < start) return 0;
		if(left <= start && end <= right) return tree[node];
		int mid =(start + end ) / 2;
		return sum(start,mid,node*2, left, right) + sum(mid+1, end, node*2+1,left,right);
}
```

1. 특정 원소의 값을 수정하는 함수

```C++
void update(int start, int end, int node, int index, int dif){
		if(index < start || index > end ) return;

		tree[node] += dif;
		if(start == end) return;
		int mid = (start + end) /2;

		update(start, mid, node*2, index, dif);
		update(mid + 1, nend,node*2+1, index, dif);

}
```