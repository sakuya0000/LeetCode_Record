# 289. Game of Life 解题记录
## 题目描述：
According to the Wikipedia's article: "The **Game of Life**, also known simply as **Life**, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."    

Given a `board` with `m` by `n` cells, each cell has an initial state `live` (1) or `dead` (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):    

1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.  
2. Any live cell with two or three live neighbors lives on to the next generation.  
3. Any live cell with more than three live neighbors dies, as if by over-population.  
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.  

Write a function to compute the next state (after one update) of the board given its current state. The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously.    

**Example:**    
```
Input: 
[
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
Output: 
[
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```
## 解题思路：
先遍历得到所有活细胞邻居的个数，再根据条件筛选。
## 代码：
``` C
class Solution {
public:
    void gameOfLife(vector<vector<int>>& board) {
        int row = board.size();
        if(row == 0) return;
        int col = board[0].size();
        if(col == 0) return;
        vector<vector<int>> cells(row+2, vector<int>(col+2, 0));
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(board[i][j] == 1){
                    cells[i][j]++;
                    cells[i+1][j]++;
                    cells[i+2][j]++;
                    cells[i][j+1]++;
                    cells[i][j+2]++;
                    cells[i+1][j+2]++;
                    cells[i+2][j+1]++;
                    cells[i+2][j+2]++;
                }
            }
        }
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(cells[i+1][j+1]==3 && board[i][j]==0){
                    board[i][j] = 1;
                }
                else if(board[i][j]==1 && (cells[i+1][j+1]==2 || cells[i+1][j+1]==3)){
                    board[i][j] = 1;
                }
                else{
                    board[i][j] = 0;
                }
            }
        }
    }
};
```