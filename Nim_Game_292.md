# 292. Nim Game 解题记录
## 题目描述：
You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.    
Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.    
**Example:**
```
Input: 4
Output: false 
Explanation: If there are 4 stones in the heap, then you will never win the game;
             No matter 1, 2, or 3 stones you remove, the last stone will always be 
             removed by your friend.
```
## 解题思路：
> 当石子数为1的时候：A取1个。A必胜。  
> 当石子数为2的时候：A取2个。A必胜。  
> 当石子数为3的时候：A取3个。A必胜。
> 当石子数为4的时候：无论A取多少个，B可以全部取完。B必胜。
> 当石子数为5的时候：A取1个，让B面临第四中情况。A必胜。
> 当石子数为6的时候：A取2个。A必胜
> ……
可见当石子数为4的倍数的时候B必胜，其他情况A必胜。
## 代码：
``` C
class Solution {
public:
    bool canWinNim(int n) {
        if(n%4 == 0)
            return false;
        return true;
    }
};
```