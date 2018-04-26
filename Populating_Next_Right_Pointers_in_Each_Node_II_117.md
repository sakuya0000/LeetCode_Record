# 117. Populating Next Right Pointers in Each Node II 解题记录
## 题目描述：
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
## 解题思路：
本题的思路和上一题的思路并没有多大的区别，还是在当前层连接下一层。  
不过相对于上一题的解题思路改进的是，在这一题中用了一个指针来记录下一层的最左指针，这样就不会局限于完美BST了，任一BST都可以用这个算法。
## 代码：
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
            //是否该层末尾
                root = beg->next;
                cur = beg;
                beg->next = NULL;
            }
        }
    }
};
```