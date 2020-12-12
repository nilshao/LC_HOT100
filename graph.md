## 有向图中寻找环

>207.课程表，寻找有没有前置课程

```C++
class Solution {
private:
    vector<vector<int>> edges;
    vector<int> visited;
    bool valid =1;
public:
    void dfs(int u){
        visited[u] =1;
        for(auto& i: edges[u]){
            if(visited[i]==1){
                valid = false;
                return;
            }
            else if(visited[i]==0){
                dfs(i);
                if(!valid){
                    return;
                }
            }
        }
        visited[u] = 2;
    }
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        visited.resize(numCourses);
        edges.resize(numCourses);
        for(auto&vec: prerequisites){
            edges[vec[0]].push_back(vec[1]);
        }
        for(int i=0; i<numCourses && valid; i++){
            dfs(i);
        }
        return valid;
    }
};
```
