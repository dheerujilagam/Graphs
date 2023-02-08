# Dijkstra's Algorithm

*Dijkstra's algorithm is a greedy algorithm used to find the shortest path between a source vertex and all other vertices in a weighted graph, where the edge weights are non-negative. It works by maintaining a priority queue of vertices, with the distance from the source vertex as the key, and repeatedly selecting the vertex with the smallest distance, updating the distances of its neighbors, and marking the selected vertex as processed. The algorithm terminates when all vertices have been processed, and the distances represent the shortest path from the source to each vertex. Dijkstra's algorithm has a time complexity of O(E + V log V), where V is the number of vertices and E is the number of edges in the graph.*


[Refer Link](https://takeuforward.org/data-structure/dijkstras-algorithm-using-priority-queue-g-32/)


```cpp
#include<bits/stdc++.h>
using namespace std;

void bfs(vector<pair<int,int>>adj[],int n, int src){

	priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>pq;
	vector<int>dis(n,INT_MAX);
	vector<int> path(n,-1);
	pq.push({0,src});
	dis[src]=0;
	while(!pq.empty()){
		int p=pq.top().second;
		pq.pop();
		for(auto it:adj[p]){
			if(dis[p]+it.second<dis[it.first]){
				path[it.first]=p;
				dis[it.first]=dis[p]+it.second;
				pq.push({dis[it.first],it.first});
			}
		}
	}
	for(int i=0;i<n;i++)
		cout<<path[i]<<" ";
	cout<<"\n";
	for(int i=0;i<n;i++)
		cout<<dis[i]<<" ";
}

int main(){
	int n,m; cin>>n>>m;
	vector<pair<int,int>>adj[n];
	int u,v,w;
	for(int i=0;i<m;i++){
		cin>>u>>v>>w;
		adj[u].push_back({v,w});
		adj[v].push_back({u,w});
	}
	int src; cin>>src;
	bfs(adj,n,src);
}
```

# Input

```
9 14
0 1 4
0 7 8
1 2 8
1 7 11
2 3 7
2 8 2
2 5 4
3 4 9
3 5 11
4 5 10
5 6 2
6 7 1
6 8 6
7 8 7
0
```

# Output

```
-1 0 1 2 5 6 7 0 2 
0 4 12 19 21 11 9 8 14 
```
