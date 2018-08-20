# 419. Battleships in a Board 解题记录
## 题目描述：
Given an 2D board, count how many battleships are in it. The battleships are represented with `'X'`s, empty slots are represented with `'.'`s. You may assume the following rules:   
- You receive a valid board, made of only battleships or empty slots.  
- Battleships can only be placed horizontally or vertically. In other words, they can only be made of the shape `1xN` (1 row, N columns) or `Nx1` (N rows, 1 column), where N can be of any size.  
- At least one horizontal or vertical cell separates between two battleships - there are no adjacent battleships.  
**Example:**  
```
X..X
...X
...X
```
In the above board there are 2 battleships.   
**Invalid Example:**
```
...X
XXXX
...X
```
This is an invalid board that you will not receive - as battleships will always have a cell separating between them.     

**Follow up:**  
Could you do it in **one-pass**, using only **O(1) extra memory** and **without modifying** the value of the board?  
## 解题思路：
根据Follow up的要求不能改变甲板的字符，一次遍历和只能使用固定的空间。可以从左上角依次遍历甲板，判断是否为`X`，若为`X`，则再进行下一步的判断，判断左边一个和右边一个是否为`X`，若不是则令计数+1；其余情况全当无效处理。
## 代码：
``` C
class Solution {
public:
    int countBattleships(vector<vector<char>>& board) {
        int row = board.size();
        if(row == 0) return 0;
        int col = board[0].size(), ret = 0;
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(board[i][j] == 'X'){
                    if(!i && !j){ 
                        ret++;
                        continue;
                    }
                    if(!i && board[i][j-1] != 'X') ret++;
                    if(!j && board[i-1][j] != 'X') ret++;
                    if(i && j && board[i-1][j] != 'X' && board[i][j-1] != 'X') ret++;
                }
            }
        }
        return ret;
    }
};
```
