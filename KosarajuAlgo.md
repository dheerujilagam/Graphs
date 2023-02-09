# Kosaraju's Algorithm

*The Kosaraju's algorithm is a linear-time algorithm used to find the strongly connected components (SCCs) of a directed graph. A strongly connected component of a directed graph is a subgraph where there is a directed path from any vertex to any other vertex.
The algorithm works by using two passes of Depth-First Search (DFS). In the first pass, the DFS is performed on the original graph in a way that the order of nodes processed by the DFS is reversed in each strongly connected component. In the second pass, a DFS is performed on the reverse graph, using the order of nodes from the first pass as a guide, so that strongly connected components are processed as a single DFS tree. The strongly connected components are identified by keeping track of the start and end times of the nodes in the DFS.
Kosaraju's algorithm is considered to be a very efficient algorithm for finding SCCs, with a time complexity of O(n + m), where n is the number of vertices and m is the number of edges in the graph. This makes it a popular choice for solving problems that require finding SCCs in large graphs.*


[Refer Link](https://takeuforward.org/graph/strongly-connected-components-kosarajus-algorithm-g-54/)


```cpp
#include<bits/stdc++.h>
using namespace std;

class Solution{

	void dfs(int node, vector<int> adj[], vector<int> &vis, stack<int> &st){
        vis[node]=1;
        for(int it:adj[node]){
            if(!vis[it]){
                dfs(it,adj,vis,st);
            }
        }
        st.push(node);
    }
    
    void dfsT(int node, vector<int> adjT[], vector<int> &vis){
        vis[node]=1;
        for(int it:adjT[node]){
            if(!vis[it]){
                dfsT(it,adjT,vis);
            }
        }
    }

	public :
	int kosaraju(int n, vector<int> adj[]){
        stack<int>st;
        vector<int>vis(n,0);
        for(int i=0;i<n;i++){
            if(!vis[i]){
                dfs(i,adj,vis,st);
            }
        }
        
        vector<int>adjT[n];
        for(int i=0;i<n;i++){
            vis[i]=0;
            for(int it:adj[i]){
                adjT[it].push_back(i);
            }
        }
        
        int connected=0;
        while(!st.empty()){
            int node=st.top();
            st.pop();
            if(!vis[node]){
                connected++;
                dfsT(node,adjT,vis);
            }
        }
        
        return connected;
    }
};

int main(){
	int n,m; cin>>n>>m;
	vector<int>adj[n];
	int u,v;
	for(int i=0;i<m;i++){
		cin>>u>>v;
		adj[u].push_back(v);
	}
	Solution ob;
	cout<<"Strongly connected components :"<<ob.kosaraju(n,adj)<<endl;
}
```
# Graph

![img](https://takeuforward.org/wp-content/uploads/2022/12/Screenshot-2022-12-26-143658.png)


![img](https://takeuforward.org/wp-content/uploads/2022/12/Screenshot-2022-12-26-143943-1.png)

# Input
```
8 9
2 0
0 1
1 2
2 3
3 4
4 7
4 5
5 6
6 4
```

# Output
```
Strongly connected components :4
```
