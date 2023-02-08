# Bellman Ford Algorithm

*The Bellman-Ford algorithm is a dynamic programming algorithm used to solve the single-source shortest path problem for a graph with negative edge weights, i.e. it finds the shortest path from a source vertex to all other vertices in the graph. It works by iteratively relaxing the distances of vertices from the source, until no further improvements can be made. The algorithm has a time complexity of O(VE) where V is the number of vertices and E is the number of edges in the graph.*

[Refer link](https://takeuforward.org/data-structure/bellman-ford-algorithm-g-41/)

```cpp
#include<bits/stdc++.h>
using namespace std;

vector<int> bellmanFord(int n, vector<vector<int>> &adj, int src){
	vector<int>dis(n,1e8);
	dis[src]=0;
	for(int i=0;i<n-1;i++){
		for(auto it:adj){
			int u=it[0],v=it[1],wt=it[2];
			if(dis[u]!=1e8 && dis[u]+wt<dis[v]){
				dis[v]=dis[u]+wt;
			}
		}
	}
	for(auto it:adj){
		int u=it[0],v=it[1],wt=it[2];
		if(dis[u]!=1e8 && dis[u]+wt<dis[v]){
			return {-1};
		}
	}
	return dis;
}

int main(){
	int n,m; cin>>n>>m;
	vector<vector<int>>adj(m,vector<int>(3));
	int u,v,wt;
	for(int i=0;i<m;i++){
		cin>>u>>v>>wt;
		adj[i][0]=u;
		adj[i][1]=v;
		adj[i][2]=wt;
		//cout<<adj[i][0]<<" "<<adj[i][1]<<" "<<adj[i][2]<<"\n";
	}
	int src; cin>>src;
	vector<int>ans=bellmanFord(n,adj,src);
	for(int i:ans)
		cout<<i<<" ";
}
```

# Input
```
6 7
3 2 6
5 3 1
0 1 5
1 5 -3
1 2 -2
3 4 -2
2 4 3
0
```

# output
```
0 5 3 3 1 2 
```
