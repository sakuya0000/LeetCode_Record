# 230. Kth Smallest Element in a BST �����¼
## ��Ŀ������
Given a binary search tree, write a function `kthSmalles` to find the kth smallest element in it.  
  **Example 1:**  
```
Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
```  
**Example 2:**  
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
```
## ����˼·��
����û��ʲô�Ѷȣ����������BST���ɡ�
## ���룺
``` C
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
    void searchMinNum(TreeNode* root, int &k, int &ret){
        if(k == -1 || !root) return;
        searchMinNum(root->left, k, ret);
        k--;
        if(k == 0){
            ret = root->val;
            k = -1;
            return;
        }
        searchMinNum(root->right, k, ret);
    }
public:
    int kthSmallest(TreeNode* root, int k) {
        int ret;
        searchMinNum(root, k, ret);
        return ret;
    }
};
```