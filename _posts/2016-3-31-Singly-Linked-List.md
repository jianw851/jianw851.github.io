---
layout: post
category: [algorithm]
title: Singly Linked List Practice
tagline: by Jian
tags: [Singly Linked List, List]
---

> This is a naive implementation of Singly Linked List which mainly used to add or remove element from front or end side.

> This implementation only shows the general idea of how grow array data structure works inside the computer. This is not used for any real world problems.

<!--more-->

```
#include<iostream>
using namespace std;
class Node {
public:
  int val;
  Node * next;
  Node() : val(0), next(NULL) {}
  Node(int v) : val(v), next(NULL) {}
};
class SinglyLinkedList {
private:
  Node * head;
  Node * tail;
public:
  SinglyLinkedList() : head(NULL), tail(NULL) { }
  SinglyLinkedList(int v) {
    head = tail = new Node(v);
  }
  ~ SinglyLinkedList() {
    Node * temp;
    while (head != NULL) {
      temp = head;
      head = head->next;
      temp->next = NULL;
      delete temp;
    }
    temp = NULL;
    tail = NULL;
  }
  void firstAdd(int v) {
    head = tail = new Node(v);
  }
  void addStart(int v) {
    if (head == NULL) {
      firstAdd(v);
    } else {
    Node * temp = head;
    head = new Node(v);
    head->next = temp;
    temp = NULL;
    }
  }
  void addEnd(int v) {
    if (head == NULL) {
      firstAdd(v);
    } else {
      tail->next = new Node(v);
      tail = tail->next;
    }
  }
  void removeStart() {
    if (head != NULL) {
      Node * temp = head;
      head = head->next;
      temp->next = NULL;
      delete temp;
      temp = NULL;
    }
  }
  void display() {
    Node * curr = head;
    while (curr != NULL) {
      cout << curr->val << " ";
      curr = curr->next;
    }
    curr = NULL;
  }
};

int main() {
  SinglyLinkedList sll;
  for (int i = 0; i < 20; i++)
    sll.addEnd(i);
  for (int i = 0; i < 20; i++)
      sll.addStart(i);
  for (int i = 0; i < 10; i++)
    sll.removeStart();
  sll.display();
}

```

 Contribution

 [@jianw851](http://jianwang.info/)


---
