# 208. Implement Trie (Prefix Tree) 解题记录
## 题目描述：
Implement a trie with `insert`, `search`, and `startsWith` methods.   
  
**Note:**  
You may assume that all inputs are consist of lowercase letters `a-z`.  
## 解题思路：
创建一个节点类，里面有isWord代表`到该节点为止的字符串是否是个单词 `和26个子节点。  
## 代码：
``` C
class TrieNode{
public:
    bool isWord = false;
    TrieNode* children[26] = {NULL};
    TrieNode(){}
};
class Trie {
    TrieNode *root = new TrieNode();
public:
    /** Initialize your data structure here. */
    Trie() {
        
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode *tail = root;
        for(int i = 0; i < word.length(); i++){
            int index = word[i]-'a';
            if(tail->children[index]){
                tail = tail->children[index];
            }
            else{
                tail->children[index] = new TrieNode();
                tail = tail->children[index];
            }
        }
        tail->isWord = 1;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode *tail = root;
        for(int i = 0; i < word.length(); i++){
            tail = tail->children[word[i]-'a'];
            if(!tail)
                return 0;
        }
        return tail->isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        TrieNode *tail = root;
        for(int i = 0; i < prefix.length(); i++){
            int index = prefix[i]-'a';
            tail = tail->children[index];
            if(!tail)
                return 0;
        }
        return 1;
    }
    
    void freeTrieNode(TrieNode* pNode){  
        if (pNode == NULL)  
            return;  
        for (int i=0; i<26;i++)  
        {  
            TrieNode* pChild = pNode->children[i];  
            if (pChild != NULL)  
            {  
                freeTrieNode(pChild);  
            }  
        }  
        free(pNode);  
    } 
    
    ~Trie(){
        freeTrieNode(root);
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * bool param_2 = obj.search(word);
 * bool param_3 = obj.startsWith(prefix);
 */
```