# 143. Reorder List 解题记录 
## 题目描述：
Given a singly linked list L: L0→L1→…→Ln-1→Ln,  
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…  
  
You may **not** modify the values in the list's nodes, only nodes itself may be changed.'  
  
**Example 1:**
  
> Given 1->2->3->4, reorder it to 1->4->2->3.  
  
**Exmaple 2:**
  
> Given 1->2->3->4->5, reorder it to 1->5->2->4->3.  
  
## 解题思路：
从题目的描述中可以看到，Ln被插入L0和L1之间，Ln-1被插入L1和L2之间……  
所以我们可以用递归来得到最后一个节点，把这个节点插入到对应位置。  
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
    int level = 0;
    ListNode* cur;
    int changeList(ListNode* root){
        if(!root->next)
            return 0;
        level++;
        int curLevel = changeList(root->next)+1;
        if(curLevel > level/2)
            return curLevel;
        root->next->next = cur->next;
        cur->next = root->next;
        root->next = NULL;
        cur = cur->next->next;
        return curLevel;
    }
    void reorderList(ListNode* head) {
        if(!head)
            return;
        cur = head;
        changeList(head);
    }
};
```
