# 173. Binary Search Tree Iterator 解题记录
## 题目描述：
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.  
  
Calling `next()` will return the next smallest number in the BST.  
  
Note: `next()` and `hasNext()` should run in average O(1) time and uses O(h) memory, where h is the height of the tree.   
## 解题思路：
将BST按升序存在一个队列中，然后对队列进行操作就行了。这个升序队列可以通过中序遍历得到。
## 代码：
``` C
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class BSTIterator {
private:
    queue<TreeNode *> inOrderNodes;

    void inOrder(TreeNode *root, queue<TreeNode *> &inOrderNodes)
    //中序遍历得到队列
    {
        if (!root)
            return;
        if (root->left)
            inOrder(root->left, inOrderNodes);

        inOrderNodes.push(root);

        if (root->right)
            inOrder(root->right, inOrderNodes);
    }
public:
    BSTIterator(TreeNode *root) {
        inOrder(root, inOrderNodes);
    }

    /** @return whether we have a next smallest number */
    bool hasNext() {
        if(inOrderNodes.empty())
            return false;
        return true;
    }

    /** @return the next smallest number */
    int next() {
        TreeNode *node = inOrderNodes.front();
        inOrderNodes.pop();
        return node->val;
    }

};

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
```