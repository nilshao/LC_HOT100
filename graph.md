# 基本概念：

## 入度表，出度表
    vector或array，第i个元素表示这个node被多少node射入（入度），射到多少node（出度）

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
    //输入的图格式是路径的向量,每个vector都是{出射,入射}
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        visited.resize(numCourses);                 //public定义部分没有size
        edges.resize(numCourses);
        //在这里转换成n个点n维向量，每个元素是与第i节点相连的所有节点，第i个向量：{被i节点射入的点，被i节点射入的点，被i节点射入的点...}
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

    关键词：入度

    思路：检查所有点，把没有被入射的点拿出来，存入queue挨个检查，检查射了谁，
    
    然后把被射的这个点入度-1，如果是0就也放入检查queue，直到queue被pop完，
    
    与此同时保持计数，看看检查了多少个点，和总node数是否相同。

```C++
class Solution {
private:
    vector<vector<int>> edges;
    vector<int> indeg;  //入度值表

public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        edges.resize(numCourses);
        indeg.resize(numCourses);

        for(auto& vec: prerequisites){
            edges[vec[0]].push_back(vec[1]);
            indeg[vec[1]]++;
        }
        
        queue<int> q;

        for(int i=0; i<edges.size(); ++i){          //把没有被入射的点放入queue
            if(indeg[i]==0){
                q.push(i);
                
            }
        }
        int visited = 0;                            //visited是用来计数检查过多少点
        visited = q.size();         
        while (!q.empty()){
            for(int i: edges[q.front()]){
                indeg[i]--;
                if(indeg[i]==0){
                    q.push(i);
                    visited++;
                }
                
            }
            q.pop();
        }
        return visited == numCourses;
    }
};

```