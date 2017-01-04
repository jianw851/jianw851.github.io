---
layout: post
category: [algorithm]
title: Binary Tree order traversal implementation
tagline: by Jian
tags: [Tree, DFS, Divide and Conquer, Traverse, Pre-order, Post-order, In-order]
---

This is a implementation of Binary Tree which is used to test its pre-order, in-order and post-order traversal sequence.

I found a very interesting thing that test case 2 and test case 3 can let two different order has the same sequence.

<!--more-->

```cpp

#include<iostream>
#include<fstream>
#include<stack>
#include<string>
#include<queue>
#include<vector>
#include<unordered_set>

using std::cout;
using std::ifstream;
using std::stack;
using std::string;
using std::queue;
using std::vector;
using std::unordered_set;

class Node {
public:
  int val;
  Node * left;
  Node * right;
  Node() : val(0), left(NULL), right(NULL) {}
  Node(int v) : val(v), left(NULL), right(NULL) {}
};

class BinaryTree {
private:
  Node * root;
public:
  BinaryTree() : root(NULL) {}
  BinaryTree(int v) : root(new Node(v)) {}
  ~ BinaryTree() {
    if (root != NULL) {
      destruct(root);
      delete root;
    }
  }

  void destruct(Node * node) {
    if (node -> left != NULL) {
      destruct(node -> left);
      delete node -> left;
    }
    if (node -> right != NULL) {
      destruct(node -> right);
      delete node -> right;
    }
  }
  Node * getRoot() const {
    return root;
  }
  void buildPlainTree(string filename) {
    if (root != NULL) {
      destruct(root);
      delete root;
    }
    ifstream infile;
    infile.open(filename);
    if (infile.fail()) {
      cout << filename <<" open fail! \n";
      return;
    }
    string word = "";
    int num = 0, pos = 1;
    vector<Node*> array;
    while (infile >> word) {
      if (word != "#") {
        num = stoi(word);
        array.push_back(new Node(num));
      } else {
        array.push_back(NULL);
      }
    }

   for (int i = 0; i < array.size() && pos < array.size(); i++) {
     if (array[i] == NULL) continue;
       array[i]->left = array[pos++];
     if (pos < array.size())
       array[i]->right = array[pos++];
   }
   root = array[0];
   array.clear();
  }

  void doit(Node * node) {
    cout << node -> val << "  ";
  }

  // DC : Divide and Conquer
  void DC_preorder(Node * node) {
    if (node == NULL) return;
    doit(node);
    DC_preorder(node -> left);
    DC_preorder(node -> right);
  }
  void DC_postorder(Node * node) {
    if (node == NULL) return;
    DC_postorder(node -> left);
    DC_postorder(node -> right);
    doit(node);
  }
  void DC_inorder(Node * node) {
    if (node == NULL) return;
    DC_inorder(node -> left);
    doit(node);
    DC_inorder(node -> right);
  }

  // DFS : Depth First Search
  void DFS_preorder(Node * root) {
    Node * curr = root;
    stack<Node*> list;
    while (!list.empty() || curr != NULL) {
      while (curr != NULL) {
        doit(curr);
        list.push(curr);
        curr = curr->left;
      }
      if (!list.empty()) {
        curr = list.top()->right;
        list.pop();
      }
    }
  }

  void DFS_postorder(Node * root) {
    Node * curr = root;
    stack<Node*> list;
    unordered_set<Node*> set1;
    while (!list.empty() || curr != NULL) {
      while (curr != NULL) {
        list.push(curr);
        curr = curr->left;
      }
      if (!list.empty()) {
        if (set1.find(list.top()) != set1.end()) {
          doit(list.top());
          list.pop();
          curr = NULL;
          continue;
        }
        if (list.top()->right == NULL) {
          doit(list.top());
          curr = list.top()->right;
          list.pop();
          continue;
        }
        curr = list.top()->right;
        set1.emplace(list.top());
      }
    }
  }

  void DFS_inorder(Node * root) {
    Node * curr = root;
    stack<Node*> list;
    while (!list.empty() || curr != NULL) {
      while (curr != NULL) {
        list.push(curr);
        curr = curr->left;
      }
      if (!list.empty()) {
        doit(list.top());
        curr = list.top()->right;
        list.pop();
      }
    }
  }

  // BFS : Breadth First Search
  void BFS_levelorder(Node * root) {
     queue<Node*> q;
     q.push(root);
     while (!q.empty()) {
       if (q.front() -> left != NULL)
         q.push(q.front() -> left);
       if (q.front() -> right != NULL)
         q.push(q.front() -> right);
       doit(q.front());
       q.pop();
     }
  }
  void testAll(string filename) {
    buildPlainTree(filename);
    cout <<"*************level************\n";
    BFS_levelorder(root);
    cout <<"\n***********preorder***********\n";
    DC_preorder(root);
    cout <<"\n";
    DFS_preorder(root);
    cout <<"\n************inorder***********\n";
    DC_inorder(root);
    cout <<"\n";
    DFS_inorder(root);
    cout <<"\n***********postorder**********\n";
    DC_postorder(root);
    cout <<"\n";
    DFS_postorder(root);
    cout <<"\n";
    cout <<"\n***********end**********\n";
  }
};

int main () {
  BinaryTree tree;
  tree.testAll("inputTree.txt");
  tree.testAll("inputTree1.txt");
  tree.testAll("inputTree2.txt");
}


```


```
test case 1: 1 2 3 4 5 6 7 # 8 # 9 10 11 # 13 14 15 16 17
test case 2: 1 2 # 3 # 4 # 5 # 6 # 7 # 8
test case 3: 1 # 2 # 3 # 4 # 5 # 6 # 7 # 8
```

 Contribution

 [@jianw851](http://jianwang.info/)


---
