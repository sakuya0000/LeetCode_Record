# 109. Convert Sorted List to Binary Search Tree 解题记录
## 题目描述：
Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.  
  
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees 
of every node never differ by more than 1.  
  
**Example:**  
```
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```
## 解题思路：
这题可以先用递归遍历到左子树的最低端，添加左子树，添加根节点，在添加右节点，中序遍历添加的顺序创建BST。
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
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
    ListNode* cur = NULL;
public:
    TreeNode* build(int beg, int end){
        if(beg > end)
        //空节点条件
            return NULL;
        int mid = (beg + end)/2;
        TreeNode* left = build(beg, mid-1);  //遍历左子树
        TreeNode* root = new TreeNode(cur->val);  //添加根节点
        root->left = left;
        cur = cur->next;  //添加完成后到下一个节点
        root->right = build(mid+1, end);  //添加右节点
        return root;
    }
    TreeNode* sortedListToBST(ListNode* head) {
        cur = head;
        int len = 0;
        while(head){
            len++;
            head = head->next;
        }
        return build(0, len-1);
    }
};
```