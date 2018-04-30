# 142. Linked List Cycle II 解题记录
## 题目描述：
Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.  
  
**Note:** Do not modify the linked list. 
## 解题思路：
先用两个指针fast和slow来遍历链表（fast指针的速度为slow速度的两倍）
，因此经过计算第一次相遇它们的位置距离环开始的位置和head指针到环开始的位置相差节点的个数相同。
然后让slow指针为head，再次遍历后第二次相遇就是环开始的位置。
## 代码：
``` C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head, *slow = head;
        while(fast){
            if(!fast->next || !fast->next->next)
	    //环不存在
                return NULL;
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow)  //第一次相遇
                break;
        }
        slow = head;
        while(slow != fast){
        //第二次相遇
            slow = slow->next;
            fast = fast->next;
        }
        return slow;
    }
};
```