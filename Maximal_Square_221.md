# 221. Maximal Square 解题记录
## 题目描述：
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.  
  **Example:**  
```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```
## 解题思路：
本题可以用动态规划来解决，递推公式为**ret[i][j] = min(min(ret[i-1][j], ret[i][j-1]), ret[i-1][j-1]) + 1**。
## 代码：
``` C
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int row = matrix.size();
        if(row == 0) return 0;
        int col = matrix[0].size(), maxNum = 0;
        vector<vector<int> > ret(row, vector<int>(col, 0));
        for(int i = 0; i < col; i++){  //初始化第一行
            ret[0][i] = matrix[0][i] - 48;
            maxNum = max(ret[0][i], maxNum);
        }
        for(int i = 0; i < row; i++){  //初始化第一列
            ret[i][0] = matrix[i][0] - 48;
            maxNum = max(ret[i][0], maxNum);
        }
        for(int i = 1; i < row; i++){
            for(int j = 1; j < col; j++){
                if(matrix[i][j] == '1'){
                    ret[i][j] = min(min(ret[i-1][j], ret[i][j-1]), ret[i-1][j-1]) + 1;
                    maxNum = max(ret[i][j], maxNum);
                }
            }
        }
        return maxNum*maxNum;
    }
};
```