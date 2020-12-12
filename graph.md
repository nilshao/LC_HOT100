# 有向图中寻找环

## 207.课程表，寻找有没有前置课程
解法一：深度优先搜索
```C++
// 
class Solution {
private:
    vector<vector<int>> edges;
    vector<int> visited;
    bool valid =1;
public:
    void dfs(int u){
        //每个节点有三个状态，0未遍历，1正在遍历，2已遍历
        visited[u] =1;
        for(auto& i: edges[u]){
            if(visited[i]==1){
                //如果状态是正在遍历，则说明有环，为什么已遍历状态ok？
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
    //输入的图格式是路径的向量
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        visited.resize(numCourses);
        edges.resize(numCourses);
        //在这里转换成n个点n维向量，每个元素是与第i节点相连的所有节点
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

解法二：广度优先搜索

```C++


```