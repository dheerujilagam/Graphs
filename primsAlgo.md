# Prims's Algorithm

*Approach: 
In order to implement Prim’s algorithm, we will be requiring an array(visited array) and a priority queue that will essentially represent a min-heap. We need another array(MST) as well if we wish to store the edge information of the minimum spanning tree.*

*Intution:
The intuition of this algorithm is the greedy technique used for every node. If we carefully observe, for every node, we are greedily selecting its unvisited adjacent node with the minimum edge weight(as the priority queue here is a min-heap and the topmost element is the node with the minimum edge weight). Doing so for every node, we can get the sum of all the edge weights of the minimum spanning tree and the spanning tree itself(if we wish to) as well.*

 ```cpp
 
 #include<bits/stdc++.h>
using namespace std;

void bfs(vector<pair<int,int>> adj[], int n){
	priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>>pq;
	vector<int>vis(n,0);
	int ans=0;
	pq.push({0,0});
	while(!pq.empty()){
		pair<int,int>p=pq.top();
		pq.pop();
		int wt=p.first;
		int node=p.second;
		if(!vis[node]){
			vis[node]=1;
			ans+=wt;
			for(auto it:adj[node]){
				int x=it.first;
				int y=it.second;
				if(!vis[x]){
					pq.push({y,x});
				}
			}
		}
	}
	cout<<"Minimum Cost: "<<ans<<endl;	
}

int main(){
	int n,m;
	cin>>n>>m;
	vector<pair<int,int>>adj[n];
	for(int i=0;i<m;i++){
		int u,v,d;
		cin>>u>>v>>d;
		adj[u].push_back({v,d});
		adj[v].push_back({u,d});
	}
	//BFS
	bfs(adj,n);
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
```

# Output
```
Minimum Cost: 37
```
