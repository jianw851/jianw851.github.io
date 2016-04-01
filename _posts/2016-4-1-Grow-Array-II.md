---
layout: post
category: [algorithm]
title: Grow Array Practice II
tagline: by Jian
tags: [Grow Array, Array]
---

This is a naive implementation of Grow Array which mainly used to add or remove element from front or end side. This Grow Array distinguish the first one that using first and last pointer instead of used and size;

<!--more-->

```cpp
#include<iostream>

using std::cout;
using std::endl;

class GrowArray {
private:
  int * array;
  int first;
  int last;
  void grow() {
    int * temp = array;
    array = new int[(last + 1) * 2];
    for (int i = 0; i <= last; i++) {
      array[i] = temp[i];
    }
    first = last;
    delete [] temp;
  }
public:
  GrowArray() :
    array(new int[1]), first(0), last(-1) {}
  GrowArray(int size) :
    array(new int[size]), first(size / 2), last(-1) {}
  ~ GrowArray() {
    delete [] array;
  }
  void addStart(int v) {
    if ((first + 1) * 2 == (last + 1))
      grow();
    int * temp = array;
    array = new int[(first + 1) * 2];
    for (int i = 0; i <= last; i++) {
      array[i+1] = temp[i];
    }
    array[0] = v;
    last++;
    delete [] temp;
  }
  void addEnd(int v) {
    if ((first + 1) * 2 == (last + 1))
      grow();
    array[++last] = v;
  }
  void removeStart() {
    for (int i = 0; i <= last; i++) {
      array[i] = array[i+1];
    }
    last--;
  }
  void removeEnd() {
    last--;
  }
  int get(int i) {
    if (i < 0 || i > last) throw "Out of bound!";
    return array[i];
  }
  void set(int i, int v) {
    if (i < 0 || i > last) throw "Out of bound!";
    array[i] = v;
  }
  int getCapacity() {
    return (first + 1) * 2;
  }
  int getUsed() {
    return last + 1;
  }
};

int main () {
  GrowArray arr;
  for (int i = 0; i < 33; i++) {
    arr.addStart(i);
  }
  for (int i = 0; i < 33; i++) {
    arr.addEnd(i);
  }
  for (int i = 0; i < 20; i++) {
    arr.removeEnd();
  }
  for (int i = 0; i < 20; i++) {
    arr.removeStart();
  }
  arr.set(13, 99999);
  for (int i = 0; i < arr.getUsed(); i++) {
    cout << arr.get(i) << " ";
  }
  cout << endl << arr.getCapacity()<<endl;
  cout << arr.getUsed()<<endl;
  return 0;
}

```

 Contribution

 [@jianw851](http://jianwang.info/)


---
