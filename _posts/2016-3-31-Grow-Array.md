---
layout: post
category: [algorithm]
title: Grow Array Practice
tagline: by Jian
tags: [Grow Array, Array]
---

This is a naive implementation of Grow Array which mainly used to add or remove element from front or end side.

This implementaion only gives the general idea of how grow array data structure works inside the computer. This is not used for any real world problems.

<!--more-->

```cpp
#include<iostream>
using namespace std;
class growArray {
private:
  int * array;
  int used;
  int size;
  void grow() {
    int * temp = array;
    array = new int[size*2];
    for (int i = 0; i < size*2; i++) {
      if (i < size)
        array[i] = temp[i];
    }
    size *= 2;
    delete [] temp;
  }
public:
  growArray() :
    array(new int[1]), size(1), used(0) {}
  growArray(int capacity) :
    array(new int[capacity]), size(capacity), used(0) {}
  ~ growArray() { delete [] array; }
  int get(int i) {
    if (i < 0 || i > used) throw "Out of bound!";
    return array[i];
  }
  void set(int i, int v) {
    if (i < 0 || i > used) throw "Out of bound!";
    array[i] = v;
  }
  void addStart(int v) {
    if (used == size)
      grow();
    int * temp = array;
    array = new int[size];
    array[0] = v;
    used++;
    for (int i = 1; i < used; i++)
      array[i] = temp[i-1];
    delete [] temp;
  }
  void removeStart() {
    if (used == 0) return;
    used--;
    for (int i = 0; i < used; i++)
      array[i] = array[i+1];
  }
  void removeEnd() {
    if (used == 0) return;
    used--;
  }
  void addEnd(int v) {
    if (used == size)
      grow();
    array[used++] = v;
  }
  int getCapacity() {
    return size;
  }
  int getUsed() {
    return used;
  }
};

int main () {
  growArray arr;
  for (int i = 0; i < 65; i++) {
    arr.addStart(i);
  }
  for (int i = 0; i < arr.getUsed(); i++) {
    cout << arr.get(i) << " ";
  }
  cout << endl << arr.getCapacity()<<endl;
  return 0;
}

```

 Contribution

 [@jianw851](http://jianwang.info/)


---
