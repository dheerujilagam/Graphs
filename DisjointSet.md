# Disjoint set

*Approach:
Now, in order to solve this question we can use either the DFS or BFS traversal technique like if we traverse the components of the graph we can find that node 1 and node 5 are not in the same component. This is actually the brute force approach whose time complexity is O(N+E)(N = no. of nodes, E = no. of edges). But using a Disjoint Set data structure we can solve this same problem in constant time.The disjoint Set data structure is generally used for dynamic graphs.*

![Refer link](https://takeuforward.org/data-structure/disjoint-set-union-by-rank-union-by-size-path-compression-g-46/)

```cpp
#include<bits/stdc++.h>
using namespace std;

int parent[100000];
int Rank[100000];
void SetData(){
	for(int i=0;i<100000;i++){
		parent[i]=i;
		Rank[i]=0;
	}
}

int FindParent(int node){
	if(parent[node]==node) 
		return node;
	return parent[node]=FindParent(parent[node]);
}

void Union(int u, int v){
	u=FindParent(u);
	v=FindParent(v);
	if(Rank[u]<Rank[v]){
		parent[u]=v;
	}
	else if(Rank[u]>Rank[v]){
		parent[v]=u;
	}
	else{
		parent[v]=u;
		Rank[u]++;
	}
}

int main(){
	//int n,m; cin>>n>>m;
	SetData();
	Union(1,2);
	Union(2,3);
	Union(4,5);
	Union(6,7);
	Union(5,6);
	if(FindParent(3)!=FindParent(7)){
		cout<<1<<endl;
	}
	else
		cout<<0<<endl;
}
```
