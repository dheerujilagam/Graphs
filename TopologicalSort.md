# Topological Sort

[Refer Link](https://takeuforward.org/data-structure/topological-sort-bfs/)

```cpp
#include<bits/stdc++.h> 
using namespace std; 


/*Topological sorting for Directed Acyclic Graph (DAG) is a linear ordering of vertices 
such that for every directed edge u v, vertex u comes before v in the ordering.*/

void topologicalSort(vector<int> adj[], int n){
    //computing indegree of vertices.
    vector<int>inDegree(n,0);
    for(int i=0;i<n;i++){
        for(int x:adj[i]){
            inDegree[x]++;
        }
    }

    //Pick all the vertices with in-degree as 0 and add them into a queue.
    queue<int>q;
    for(int i=0;i<n;i++){
        if(inDegree[i]==0)
            q.push(i);
    }

    while(!q.empty()){
        //remove vertex
        int node=q.front();
        q.pop();
        cout<<node<<" ";
        //decrease indegree of neighbouring nodes by 1.
        for(int x:adj[node]){
            --inDegree[x];
            //if indegree == 0 add them into a queue.
            if(inDegree[x]==0)
                q.push(x);
        }
        //repeat until queue is empty.
    }
}

int main() 
{ 
    int n,m; cin>>n>>m;
    vector<int>adj[n];
    int u,v;
    for(int i=0;i<m;i++){
        cin>>u>>v;
        adj[u].push_back(v);
    }

    cout<<"TopologicalSort Order: \n";
    topologicalSort(adj,n);
} 
```

# Input
```
6 6
5 2
5 0
4 0
4 1
2 3
3 1
```

# Output
```
TopologicalSort Order: 
4 5 2 0 3 1 
```
