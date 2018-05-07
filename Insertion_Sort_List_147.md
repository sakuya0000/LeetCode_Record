# 147. Insertion Sort List �����¼
## ��Ŀ������
Sort a linked list using insertion sort.  
  
![����](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)  
  
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
## ����˼·��
˼·��Ŀ���Ѿ��������ˣ�û��ʲô�ý��ģ�ֻҪע�������Ĳ��������ˡ�
## ���룺
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