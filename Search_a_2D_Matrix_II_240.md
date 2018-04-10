# 240. Search a 2D Matrix II 解题记录
## 题目描述：
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:  
- Integers in each row are sorted in ascending from left to right.  
- Integers in each column are sorted in ascending from top to bottom.

For example,  
Consider the following matrix: 
> 
[  
　 [1,   4,  7, 11, 15],  
　 [2,   5,  8, 12, 19],  
　 [3,   6,  9, 16, 22],  
　 [10, 13, 14, 17, 24],  
　 [18, 21, 23, 26, 30]  
]

Given `target = 5`, return `true`.  
Given `target = 20`, return `false`.  
## 解题思路:
若数`大于`target，那么就往`左`搜索，因为下方的数绝对大于当前数；  
若数`小于`target，那么就往`下`搜索，因为左方的数绝对小于当前数；  
若`等于`直接返回。
## 代码：
``` C
class Solution {
public:
    class Solution {
    public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int row = matrix.size();
        if(row == 0)
            return false;
        int col = matrix[0].size(), i = 0, j = col-1;
        while(i < row && j >= 0){
        //数组搜索完毕后跳出循环
            if(matrix[i][j] == target)
                return true;
            if(matrix[i][j] > target)
                j--;
            if(matrix[i][j] < target)
                i++;
        }
        return false;
    }
};
};
```