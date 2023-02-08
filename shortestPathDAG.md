# ShortestPath in DAG 
*The shortest path in a Directed Acyclic Graph (DAG) can be found using the Topological Sort algorithm. We initialize distances to all vertices as infinite and distance to source as 0, then we find a topological sorting of the graph. Topological Sorting of a graph represents a linear ordering of the graph. Once we have topological order (or linear representation), we one by one process all vertices in topological order. For every vertex being processed, we update distances of its adjacent using distance of current vertex.*


*Following is complete algorithm for finding shortest distances. 

Initialize dist[] = {INF, INF, ....} and dist[s] = 0 where s is the source vertex. 

Create a topological order of all vertices. 

Do following for every vertex u in topological order. 

...........Do following for every adjacent vertex v of u 

..................if (dist[v] > dist[u] + weight(u, v)) 

...........................dist[v] = dist[u] + weight(u, v) *



```cpp
#include<bits/stdc++.h>
using namespace std;

void topoSort(int node, vector<pair<int,int>> adj[], vector<int> &vis, stack<int> &st){
    vis[node]=1;
    for(auto it:adj[node]){
        int v=it.first;
        if(!vis[v])
            topoSort(v,adj,vis,st);
    }
    st.push(node);
}

vector<int> shortestPath(int n, vector<pair<int,int>> adj[]){

    vector<int>vis(n,0);
    stack<int>st;
    for(int i=0;i<n;i++){
        if(!vis[i])
            topoSort(i,adj,vis,st);
    }

    vector<int>dist(n,INT_MAX);
    dist[0]=0;
    while(!st.empty()){
        int node=st.top();
        st.pop();
        for(auto it:adj[node]){
            int v=it.first;
            int wt=it.second;
            if(dist[node]+wt<dist[v]) {
                dist[v]=wt+dist[node];
              }
        }
    }
    for(int i=0;i<n;i++){
        if(dist[i]==INT_MAX)
            dist[i]=-1;
    }
    return dist;
}

int main(){
    int n,m; cin>>n>>m;

    vector<pair<int,int>>adj[n];
    for(int i=0;i<m;i++){
        int u,v,dis; cin>>u>>v>>dis;
        //cout<<u<<" "<<v<<" "<<dis<<"\n";
        adj[u].push_back({v,dis});
    }

    vector<int>ans=shortestPath(n,adj);
    for(int i:ans)
        cout<<i<<" ";
}
```

# Input
```
6 7
0 1 2
0 4 1
1 2 3
2 3 6
4 2 2
4 5 4
5 3 1
```
# Output
```
0 2 3 6 1 5 
```
