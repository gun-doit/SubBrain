> **풀이**

**노드(N)의 값이 최대 5000, 유사도의 값이 최대 1e9이므로 int를 사용해도 됨.**

**Q ( k, v ) v를 기준으로 k를 넘는 유사도를 가진 노드가 몇 개인지 구하는 것 → BFS**

  

  

> **풀이**

```C++
void solution(int K, int Vertex){
		// 방문 초기화
    int recommand_count = 0;
    bool visit[5001] = {false,};
	
		// bfs 초기화
    queue<pii> q;
    q.push({0,Vertex});
    visit[Vertex] = true;
		
		// BFS
    while(!q.empty()){
        pii cur = q.front();
        q.pop();

        int cur_cost = cur.first;
        int cur_vertex = cur.second;
        
        // 순회
        for(const auto next : v[cur_vertex]){
            int next_cost = next.first;
            int next_vertex = next.second;
            
            if(!visit[next_vertex] && next_cost >= K){
                visit[next_vertex] = true;
                recommand_count++;
                q.push({next_cost,next_vertex});
            }
        }
    }

    printf("%d\n", recommand_count);
}
```