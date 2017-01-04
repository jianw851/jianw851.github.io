---
layout: post
category: [algorithm]
title: Doubly Linked List Practice
tagline: by Jian
tags: [Doubly Linked List, List]
---

This is a naive implementation of Doubly Linked List which mainly used to add or remove element from front or end side.

This implementation only shows the general idea of how Doubly Linked List data structure works inside the computer. This is not used for any real world problems.

<!--more-->

```cpp
#include<iostream>
using namespace std;
class Node {
public:
  int val;
  Node * next;
  Node * prev;
  Node() : val(0), next(NULL), prev(NULL) {}
  Node(int v) : val(v), next(NULL), prev(NULL) {}
};
class DoublyLinkedList {
private:
  Node * head;
  Node * tail;
public:
  DoublyLinkedList() : head(NULL), tail(NULL) {}
  DoublyLinkedList(int v) {
    head = tail = new Node(v);
  }
  ~ DoublyLinkedList() {
    Node * temp;
    while (head != NULL) {
      temp = head;
      head = head->next;
      temp->next = NULL;
      temp->prev = NULL;
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
    head->next->prev = head;
    temp = NULL;
    }
  }
  void addEnd(int v) {
    if (head == NULL) {
      firstAdd(v);
    } else {
      tail->next = new Node(v);
      tail->next->prev = tail;
      tail = tail->next;
    }
  }
  void removeStart() {
    if (head != NULL) {
      Node * temp = head;
      head = head->next;
      temp->next = NULL;
      head->prev = NULL;
      delete temp;
      temp = NULL;
    }
  }
  void removeEnd() {
    if (tail != NULL) {
      Node * temp = tail;
      tail = tail->prev;
      if (tail != NULL)
       tail->next = NULL;
      temp->prev = NULL;
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
  void Reversedisplay() {
    Node * curr = tail;
    while (curr != NULL) {
      cout << curr->val << " ";
      curr = curr->prev;
    }
    curr = NULL;
  }
};

int main() {
  DoublyLinkedList dll;
  for (int i = 0; i < 20; i++)
    dll.addEnd(i);
  for (int i = 0; i < 20; i++)
    dll.addStart(i);
  for (int i = 0; i < 10; i++)
    dll.removeStart();
  dll.display();
  cout<<endl;
  dll.Reversedisplay();
  return 0;
}

```

 Contribution

 [@jianw851](http://jianwang.info/)


---
