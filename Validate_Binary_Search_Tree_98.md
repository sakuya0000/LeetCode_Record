# 98. Validate Binary Search Tree 解题记录
## 题目描述：
Given a binary tree, determine if it is a valid binary search tree (BST).  
Assume a BST is defined as follows:  
- The left subtree of a node contains only nodes with keys less than the node's key.  
- The right subtree of a node contains only nodes with keys greater than the node's key.  
- Both the left and right subtrees must also be binary search trees.  
**Example 1:**  
```
    2
   / \
  1   3
```
Binary tree `[2,1,3]`, return **true**.  
**Example 2:**  
```
    1
   / \
  2   3
```
Binary tree `[1,2,3]`, return **false**.  
## 解题思路：
这题是检验一个二叉树是否是BST，适合用递归来解决。  
- 首先我将递归终止条件设为节点为空;  
- 然后每次往下遍历的时候往下传一个区间`(minN, maxN)`，当下一个节点的数不在区间内返回false，在则继续遍历。  

而区间的传递规则为：  
1. 如果传入的节点是右节点，传入`(val, maxN)`;  
2. 如果传入的节点是左节点，传入`(minN, val)`;  
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
    bool judge(TreeNode* root, long long minN, long long maxN){
        if(!root)
        //终止条件
            return true;
        if(!(root->val>minN && root->val<maxN))
        //检验val是否在区间内
            return false;
        return judge(root->left, minN, root->val) && judge(root->right, root->val, maxN);  //向下遍历
    }
    bool isValidBST(TreeNode* root) {
        return judge(root, -21474836470, 21474836470);  //因为节点的数可能为INT_MAX和INT_MIN
    }
};
```