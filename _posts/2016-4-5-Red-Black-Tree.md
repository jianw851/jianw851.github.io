---
layout: post
category: [algorithm]
title: Red Black Tree implementation
tagline: by Jian
tags: [RBTree, Red Black Tree]
---

This is a simple implementation of Red Black Tree.


<!--more-->

### Source Code (C++)

```cpp

#include <iostream>
#include <vector>
using namespace std;

class RBTree {
private:
  class Node {
  public:
    bool isred;
    int val;
    Node * left;
    Node * right;
    Node() : val(0), isred(true), left(NULL), right(NULL) {}
    Node(int v) : val(v), isred(true), left(NULL), right(NULL) {}
  };
  Node *root;
  vector<Node *> array;
public:
  RBTree() : root(NULL) {}
  RBTree(int v) : root(new Node(v)) {}
  ~RBTree() {
    if (root != NULL) {
      destruct(root);
      delete root;
    }
    array.clear();
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

  bool isRed(Node *node) {
    if (node == NULL)
      return false;
    else
      return node->isred;
  }
  void rotate_left(Node * &node) {
    Node * temp = node -> right;
    node -> right = temp -> left;
    temp -> left = node;
    temp -> isred = node -> isred;
    node = temp;
  }
  void rotate_right(Node * &node) {
    Node * temp = node -> left;
    node -> left = temp -> right;
    temp -> right = node;
    temp->isred = node->isred;
    node->isred = true;
    node = temp;
  }
  void flip_color(Node * &node) {
    node -> isred = true;
    node -> left -> isred = false;
    node -> right -> isred = false;
  }
  void buildTree() {
    int arr[10] = {3,4,7,1,2,9,8,6,5,10};
    for (int i = 0; i < 10; i++) {
      array.push_back(new Node(arr[i]));
      insert(root, array[i]);
    }
   display(root);
 }

  void insert(Node * &node, Node * &vnode) {
    if (node == NULL) node = vnode;
    // divide
    if (node -> val > vnode->val)
      insert(node -> left, vnode);
    else if (node -> val < vnode->val)
      insert(node -> right, vnode);
    // Conquer
    if (isRed(node->right) && !isRed(node->left)) rotate_left(node);
    if (isRed(node->left) && isRed(node->left->left)) rotate_right(node);
    if (isRed(node->left) && isRed(node->right)) flip_color(node);
  }

  void display(Node * node) {
    if (node == NULL) return;
    display(node -> left);
    cout << node->val << "  ";
    display(node -> right);
  }
};

int main() {
  RBTree rbtree;
  rbtree.buildTree();
  return 0;
}


```


### Contribution

 [@jianw851](http://jianwang.info/)


---
