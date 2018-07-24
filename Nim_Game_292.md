# 292. Nim Game �����¼
## ��Ŀ������
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
## ����˼·��
> ��ʯ����Ϊ1��ʱ��Aȡ1����A��ʤ��  
> ��ʯ����Ϊ2��ʱ��Aȡ2����A��ʤ��  
> ��ʯ����Ϊ3��ʱ��Aȡ3����A��ʤ��
> ��ʯ����Ϊ4��ʱ������Aȡ���ٸ���B����ȫ��ȡ�ꡣB��ʤ��
> ��ʯ����Ϊ5��ʱ��Aȡ1������B���ٵ����������A��ʤ��
> ��ʯ����Ϊ6��ʱ��Aȡ2����A��ʤ
> ����
�ɼ���ʯ����Ϊ4�ı�����ʱ��B��ʤ���������A��ʤ��
## ���룺
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