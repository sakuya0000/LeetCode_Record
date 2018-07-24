# 304. Range Sum Query 2D - Immutable 解题记录
## 题目描述：
Given a 2D matrix matrix, find the sum of the elements inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).    
**Example:**
```
Given matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```
## 解题思路：
本题给我们一个数组，再给我们一个矩阵左上角和右下角的位置，返回矩阵中所有数的和。    
可以创建一个新的数组，存储从(0, 0)到其位置的矩阵和。这样给我们一个矩阵的位置的时候只要做3次加减法就行了。    
初始化新数组的时候可以用动态规划解决。
## 代码：
``` C
class NumMatrix {
    vector<vector<int>> newMatrix;
public:
    NumMatrix(vector<vector<int>> matrix) {
        int row = matrix.size();
        if(row == 0)
            return;
        int col = matrix[0].size();
        if(col == 0)
            return;
        vector<vector<int>> temp(row+1, vector<int>(col+1, 0));  //这里故意多加一行一列，返回的时候不用判断是否是第一行第一列的情况
        newMatrix = temp;
        int sum = 0;
        for(int i = 0; i < col; i++){  //初始化第一行
            sum += matrix[0][i];
            newMatrix[1][i+1] = sum;
        }
        for(int i = 1; i < row; i++){  //从第二行开始遍历
            sum = 0;
            for(int j = 0; j < col; j++){
                sum += matrix[i][j];
                newMatrix[i+1][j+1] = sum + newMatrix[i][j+1];
            }
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        return newMatrix[row2+1][col2+1]-newMatrix[row2+1][col1]-newMatrix[row1][col2+1]+newMatrix[row1][col1];  //返回时加减
    }
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * int param_1 = obj.sumRegion(row1,col1,row2,col2);
 */
```