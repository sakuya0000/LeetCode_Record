# 445. Add Two Numbers II 解题记录
## 题目描述：
You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.    
**Follow up:**  
What if you cannot modify the input lists? In other words, reversing the lists is not allowed. 
**Example:**
``` 
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```
## 解题思路：
这题要求是用两个链表进行加法操作，先计算两个链表的层数差，然后用递归进行加法操作。
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
    int func(ListNode* l1, ListNode* l2, int &count){
        if(!l2) return 0;
        int num = 0;
        if(count){
            count--;
            num = func(l1->next, l2, count) + l1->val;
        }
        else
            num = func(l1->next, l2->next, count) + l1->val + l2->val;
        l1->val = num % 10;
        return num / 10;
    }
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int count = 0;
        ListNode* t1 = l1, *t2 = l2;
        bool flag = 0;
        while(t1 || t2){
            if(!t1 || !t2) count++, flag = t1?1:0;
            if(t1) t1 = t1->next;
            if(t2) t2 = t2->next;
        }
        ListNode* ret = flag?l1:l2;
        int t = func(ret, flag?l2:l1, count);
        if(t){
            ListNode* temp = new ListNode(t);
            temp->next = ret;
            ret = temp;
        }
        return ret;
    }
};
```