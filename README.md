# OA-QUes
Rat in a maze ( print all paths )

```
class Solution{
    vector<string> ans;
    void recursion(int i, int j, string path, vector<vector<int>> &matrix, int row, int column)
    {
        if(i < 0 or i >= row or j < 0 or j >= column) //checking out of bound conditions 
        {
            return;
        }
        if(matrix[i][j] == 0) //this is to avoide the recursive call on blocked or viditedd numbers
        {
            return;
        }
        
        if(i == row-1 and j == column-1 ) //this is for answer making
        {
            ans.push_back(path);
        }
        
        matrix[i][j] = 0;
        
        //up
        recursion(i-1,j,path+'U',matrix,row,column);
        //down
        recursion(i+1,j,path+'D',matrix,row,column);
        //left
        recursion(i,j-1,path+'L',matrix,row,column);
        //right
        recursion(i,j+1,path+'R',matrix,row,column);
        
        matrix[i][j] = 1;
        return;
    }
    
    public:
    vector<string> findPath(vector<vector<int>> &m, int n) 
    {
        string path;
        int visited = m[0][0];
        recursion(0,0,path,m,n,n);
        return ans;
    }
};
```

Problem Description :

You are given a maze with N cells. Each cell may have multiple entry points but not more than one exit (i.e. entry/exit points are unidirectional doors like valves). The cells are named with an integer from 0 to N-1.

You have to find :

Nearest meeting cell : Given any two cells - C1, C2, find the closest cell Cm that can be reached from both C1 and C2.

```
#include<bits/stdc++.h>
using namespace std;

    vector<int> shortPath(vector<int> adj[], int c1, int n){

            vector<int> dist(n, INT_MAX);
            queue<int> q;
            q.push(c1);
            dist[c1] = 0;

            while(!q.empty()){
                int u = q.front();
                q.pop();
                
                for(auto &v: adj[u]){
                    if(dist[v] > dist[u] + 1){
                        dist[v] = dist[u] + 1;
                        q.push(v);
                    }
                }
            }
            return dist;
    }

    int main()
    {
        int n;
        cin>>n;

        vector<int> edges(n);
        for(int i=0 ; i<n ; i++)
            cin >> edges[i];

        int c1, c2;
        cin>>c1>>c2;

        vector<int> adj[n];
        for(int i=0 ; i<n ; i++){
            if(edges[i] == -1) continue;
            adj[i].push_back(edges[i]);
        }
        vector<int> v1 = shortPath(adj, c1, n);
        vector<int> v2 = shortPath(adj, c2, n);

        int mn = INT_MAX, node = -1;
        for(int i=0 ; i<n ; i++){
            if(v1[i] == INT_MAX || v2[i] == INT_MAX)
                continue;
            if(v1[i] + v2[i] < mn){
                mn = v1[i] + v2[i];
                node = i;
            }
        }
        cout << node << endl;
        return 0;
    }
```

Problem Description : You are given a maze with N cells. Each cell may have multiple entry points but not more than one exit (i.e. entry/exit points are unidirectional doors like valves).

The cells are named with an integer from 0 to N-1.

You have to find : Find the node number of maximum weight node (Weight of a node is the sum of all nodes pointing to that node).

```
#include<bits/stdc++.h>
using namespace std;

    int solution(vector<int>arr){
            int ans=INT_MIN;
            int result=-1;
            vector<int>weight(arr.size(),0);
            for(int i=0;i<arr.size();i++){
                int source=i;
                int dest=arr[i];
                if(dest!=-1){
                    weight[dest]+=source;
                    if(ans<=weight[dest]){
                        ans=max(ans,weight[dest]);
                        result=dest;
                    }
                    
                }
            }
            if(ans!=INT_MIN)
                return result;
            return -1;
}

    int main()
    {
        int n;
        cin>>n;

        vector<int> edges(n);
        for(int i=0 ; i<n ; i++)
            cin >> edges[i];

        cout<<solution(edges)<<endl;
        
        return 0;
    }
```

2360. Longest Cycle in a Graph
Hard
2.1K
39
Companies
You are given a directed graph of n nodes numbered from 0 to n - 1, where each node has at most one outgoing edge.

The graph is represented with a given 0-indexed array edges of size n, indicating that there is a directed edge from node i to node edges[i]. If there is no outgoing edge from node i, then edges[i] == -1.

Return the length of the longest cycle in the graph. If no cycle exists, return -1.

A cycle is a path that starts and ends at the same node.

```
class Solution {
public:
    int mx=-1;
    void dfs(vector<int> &ed , vector<int> &pvis , vector<int> &vis , int i , int j){
        if(pvis[i]){
            mx = max(mx , j - pvis[i]);
            return;
        }
        if(!vis[i]){
            pvis[i] =j; j++; vis[i]=1;
            if(ed[i]!=-1) dfs(ed , pvis , vis , ed[i],j);
        }
        pvis[i] = 0;
        return;
    }

    int longestCycle(vector<int>& ed) {
        vector<int> vis(ed.size(),0) , pvis(ed.size(),0);
        mx = -1;
        for(int i=0;i<ed.size();i++){
            if(!vis[i]) dfs(ed,pvis,vis,i,1);
        }
        return mx;
    }
};
```
