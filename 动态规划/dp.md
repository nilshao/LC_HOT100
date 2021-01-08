## 双重背包

```
for 循环物品 i:（1~N）
    for 循环j: (0~C1) 第一维代价限制（0的个数，或者想象为重量代价）
        for 循环 k: (0~C2) 第二维代价限制（1的个数，或者想象为体积代价）
            dp[i][j][k] = max(dp[i - 1][j][k] /*不选i*/, dp[i - 1][j - cost0[i]][k - cost1[i]] + 1/*选i*/)

```
474. 一和零
     https://leetcode-cn.com/problems/ones-and-zeroes/
        
    给你一个二进制字符串数组 strs 和两个整数 m 和 n 。

    请你找出并返回strs的最大子集的大小，该子集中最多有m个0和n个1 。

    如果 x 的所有元素也是 y 的元素，集合 x 是集合 y 的 子集 。

```C++
class Solution {
public:
    int max(int a, int b){
        return (a>b)?a:b;
    }
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<vector<int>>> dp(strs.size()+1, vector<vector<int>>(m+1,vector(n+1,0)));

        for(int i=1; i<=strs.size(); ++i){
            int count0=0,count1=0;
            for(char ch:strs[i-1]){
                if(ch=='1') count1++;
                if(ch=='0') count0++;
            }
            for(int j=0; j<=m;++j){
                for(int k=0;k<=n;++k){
                    if (j >= count0 && k >= count1) {
                        dp[i][j][k] = max(dp[i-1][j][k],1+dp[i-1][j-count0][k-count1]);
                    }else{
                        dp[i][j][k] = dp[i - 1][j][k]; 
                    }
                }
            }
        }
        return dp[strs.size()][m][n];


    }
};
```