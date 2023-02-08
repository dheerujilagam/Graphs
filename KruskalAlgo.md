# Kruskal Algorithm

*Approach: 
We will be implementing Kruskal’s algorithm using the Disjoint Set data structure.*

[Refer link](https://takeuforward.org/data-structure/kruskals-algorithm-minimum-spanning-tree-g-47/)

```cpp
#include<bits/stdc++.h>
using namespace std;

struct node{
    int u,v,wt;
    node(int first , int second, int wight){
        u = first;
        v = second;
        wt = wight;
    }
    
};

bool comp(node a , node b){
    return a.wt < b.wt;
}

int parent[3001];
int Rank[3001];

void SetData(){
    for(int i = 0 ; i <= 3000 ; i++){
        parent[i]=i;
        Rank[i]=0;
    }
}

int FindParent(int node){
    if(parent[node]==node)return node;
    return parent[node]=FindParent(parent[node]);
}

void Union(int u , int v){
    u = FindParent(u);
    v = FindParent(v);
    if(Rank[u]<Rank[v]){
        parent[u]=v;
    }
    else if(Rank[u] > Rank[v]){
        parent[v]=u;
    }
    else{
        parent[v]=u;
        Rank[u]++;
    }   
}

int main(){
    SetData();
    int n , m;
    cin >> n >> m;
    vector<node>edges;
    int u , v, wt;
    for(int i = 0 ; i < m ; i++){
        cin >> u >> v >> wt;
        edges.push_back(node(u,v,wt));
    }
    sort(edges.begin(), edges.end(),comp);
    //vector<pair<int,int>>MST;
    int cost=0;
    for(auto it:edges){
        if(FindParent(it.v)!=FindParent(it.u)){
            cost+=it.wt;
            //MST.push_back({it.u,it.v});
            Union(it.v,it.u);
        }
    }
    cout<<cost<<"\n";   
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
cost: 37
```
