> **“모든 정점”에서 “모든 정점”으로의 최단 경로**

[[Dijkstra]] - 가장 적은 비용을 하나씩 선택 but 거쳐가는 정점을 기준으로 알고리즘 수행

  

- **시간복잡도 : O(n^3)**

> **설명**

1. 2차원 인접 행렬을 구성

![[Untitled 45.png|Untitled 45.png]]

![[Untitled 1 20.png|Untitled 1 20.png]]

1. 라운드마다 각 경로에서 새로운 중간 노드로 사용할 수 있는 노드를 선택하고, 더 짧은 길이를 선택하여 줄이는 과정을 반복
2. **위 와같을때 라운드는 5라운드**

  

> **CODE**

```C++
// adj의 인접 행렬 값을 이용하여 dist 배열 생성
for(int i = 1; i<=n; i++){
	for(int j = 1; i<=n; j++){
		if(i == j) dist[i][j] = 0;
		else if(adj[i][j]) dist[i][j] = adj[i][j];
		else dist[i][j] = INF; // 큰값
  }
}




//Floyd Warshall
for(int k = 1; k<=n; k++){         // k번의 노드를 중간노드로 설정
	for(int i = 1; i<=n; i++){
		for(int j = 1; i<=n; j++){
			dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
	  }
	}
}
```

  

---

[**1) 알고리즘 - 플로이드 워셜**](https://chanhuiseok.github.io/posts/algo-50/)