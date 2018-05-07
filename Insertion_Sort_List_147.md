# 147. Insertion Sort List 解题记录
## 题目描述：
Sort a linked list using insertion sort.  
  
![样例](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)  
  
A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.  
With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list  
  
  
**Algorithm of Insertion Sort:**  
  
1. Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.  
2. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.  
3. It repeats until no input elements remain.  
  
**Example 1:**  
  
```
Input: 4->2->1->3
Output: 1->2->3->4
```
  
**Example 2:**  
  
```
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```
## 解题思路：
思路题目都已经给我们了，没有什么好讲的，只要注意对链表的操作就行了。
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
    ListNode* insertionSortList(ListNode* head) {
        ListNode* nHead = new ListNode(0);
        nHead->next = head;
        while(head && head->next){
            ListNode* t = nHead;
            while(t->next != head->next){
                if(t->next->val > head->next->val){
                    ListNode* temp = head->next->next;
                    head->next->next = t->next;
                    t->next = head->next;
                    head->next = temp;
                    break;
                }
                t = t->next;
            }
            if(t == head)
                head = head->next;
        }
        return nHead->next;
    }
};
```