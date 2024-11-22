> **그래프 상에서 특정 한 노드에서 모든 노드까지의 최단거리를 구하는 알고리즘  
> 가중 그래프에서 간선 가중치의 합이 최소가 되는 경로를 찾는 것.  
> **

![[Untitled 46.png|Untitled 46.png]]

  

> **구현_1 : 순차 탐색 O(N^2)**

```C++
int FindSmallestNode(){
		int min_dist = INF;
    int min_idx = -1;
    for (int i = 0; i<= N; i++)
    {
    	if (visited[i] == true)
        	continue;
        if (dist[i] < min_dist)
        {
        	min_dist = dist[i];
            min_idx = i;
        }
    }
    return min_idx;    
}


// 다익스트라
void Dijkstra(){
		for (int i = 1; i <= N; i++)
				dist[i] = map[start][i];  // 시작 노드와 인접한 정점에 대해 거리 계산
	    
	    dist[start] = 0;
	    visited[start] = true;
	    
	    for (int i = 0; i < N - 1; i++){
		    	int new_node = FindSmallestNode();
	        visited[new_node] = true;
	        
	        for(int j = 0; j <= N; j++){
		        	if (visited[j] == true)
		            	continue;
	            if (dist[j] > dist[new_node] + map[new_node][j])
	            	dist[j] = dist[new_node] + map[new_node][j];
	        }
	    }
}
```

  

  

> **구현_2 : 우선순위 큐**

```C++
vector<int> dijkstra(int start, int N, vector<pair<int, int>> graph[])
{
    vector<int> dist(N, INF);  // 거리를 저장할 리스트 초기화
    priority_queue<pair<int, int>> pq;  // 우선순위 큐 선언

    dist[start] = 0;  // 시작 노드 거리를 0으로 함
    pq.push({ 0, start });  // 우선순위 큐에 넣기

    while (!pq.empty())
    {
        int cur_dist = -pq.top().first; // 큐에서 꺼내 방문하고 있는 정점의 거리
        int cur_node = pq.top().second;  // 정점의 인덱스(번호)
        pq.pop();

        for (int i = 0; i < graph[cur_node].size(); i++)
        {
            int nxt_node = graph[cur_node][i].first;  // 인접 정점 번호
            int nxt_dist = cur_dist + graph[cur_node][i].second;  // 인접 정점까지 거리

            if (nxt_dist < dist[nxt_node])  // 지금 계산한 것이 기존 거리값보다 작다면
            {
                dist[nxt_node] = nxt_dist;  // 거리값 업데이트
                pq.push({ -nxt_dist, nxt_node });  // 우선순위 큐에 넣기
            }
        }
    }

    return dist;  // start 노드로부터 각 노드까지 최단거리를 담은 벡터 리턴
}
```