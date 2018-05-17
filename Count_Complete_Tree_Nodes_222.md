# 222. Count Complete Tree Nodes 解题记录
## 题目描述：
Given a complete binary tree, count the number of nodes.  
  
**Example:**  
```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```
## 解题思路：
完全二叉树必定包含一个完美二叉树和一个完全二叉树，所以可以利用递归来解决这题。
## 代码：
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
public:
    int countNodes(TreeNode* root) {
        if(!root) 
            return 0;
        int l = getLeft(root) + 1;
        int r = getRight(root) + 1;
        if(l==r) {
            return (2<<(l-1)) - 1;
        } 
        else {
            return countNodes(root->left) + countNodes(root->right) + 1;
        }
    }
    int getLeft(TreeNode* root) {
        int count = 0;
        while(root->left!=NULL) {
            root = root->left;
            ++count;
        }
        return count;
    }
    int getRight(TreeNode* root) {
        int count = 0;
        while(root->right!=NULL) {
            root = root->right;
            ++count;
        }
        return count;
    }
};
```