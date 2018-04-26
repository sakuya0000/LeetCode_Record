# 117. Populating Next Right Pointers in Each Node II �����¼
## ��Ŀ������
Given a binary tree
```
struct TreeLinkNode {
  TreeLinkNode *left;
  TreeLinkNode *right;
  TreeLinkNode *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.  
  
Initially, all next pointers are set to NULL.  
  
**Note:**  
  
- You may only use constant extra space.  
- Recursive approach is fine, implicit stack space does not count as extra space for this problem.  
  
**Example:**  
  
Given the following binary tree,  
```
     1
   /  \
  2    3
 / \    \
4   5    7
```
After calling your function, the tree should look like:  
```
     1 -> NULL
   /  \
  2 -> 3 -> NULL
 / \    \
4-> 5 -> 7 -> NULL
```
## ����˼·��
�����˼·����һ���˼·��û�ж������𣬻����ڵ�ǰ��������һ�㡣  
�����������һ��Ľ���˼·�Ľ����ǣ�����һ��������һ��ָ������¼��һ�������ָ�룬�����Ͳ������������BST�ˣ���һBST������������㷨��
## ���룺
``` C
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        TreeLinkNode* beg = new TreeLinkNode(0), *cur = beg;
        while(root){
            if(root->left){
                cur->next = root->left;
                cur = cur->next;
            }
            if(root->right){
                cur->next = root->right;
                cur = cur->next;
            }
            root = root->next;
            if(!root){
            //�Ƿ�ò�ĩβ
                root = beg->next;
                cur = beg;
                beg->next = NULL;
            }
        }
    }
};
```