---
layout: post
category: [algorithm]
title: Queue by Grow Array
tagline: by Jian
tags: [Queue, Grow Array, Two Pointers]
---

This is a implementation of Queue using Grow Array with two pointers.

<!--more-->

```cpp
#include<iostream>

using std::cout;

class Queue {
private:
  int * array;
  int head;
  int tail;
  int capacity;
  void grow () {
    int * temp = array;
    array = new int[capacity * 2];
    int h = (head % capacity), t = (tail % capacity);
    if (h >= t) {
      for (int i = t; i <= h; i++) {
        array[i] = temp[i];
      }
    } else {
      int i;
      for ( i = t; i <= h + (capacity - t); i++) {
        if (i < capacity)
          array[i] = temp[i];
        else
          array[i] = temp[i - capacity];
      }
    }
    capacity *= 2;
    delete [] temp;
  }
public:
  Queue() : capacity(0), array(NULL), head(-1), tail(0) {}
  Queue(int v) {
    capacity = 1;
    array = new int[1];
    array[0] = v;
    tail = head = 0;
  }
  ~ Queue() {
    delete [] array;
  }
  void enqueue(int v) {
    if (capacity == 0) {
      capacity = 1;
      array = new int[1];
      array[0] = v;
      tail = head = 0;
    } else {
      if (head >= tail && (head + 1) % capacity == tail)
        grow();
      head++;
      array[head % capacity] = v;
    }
  }
  int dequeue() {
    if (capacity == 0 || tail > head) return -1;
    return array[tail++ % capacity];
  }
  int size() {
    return head - tail + 1;
  }
  int isEmpty() {
    return tail > head;
  }
  void display() {
    for (int i = tail; i <= head; i++) {
      cout << array[i % capacity] << " ";
    }
    cout << "\nhead = " << head << " tail = "<<tail<<" capacity="<<capacity<<"\n";
  }
};

int main() {
  Queue q;
  for (int i = 0; i < 300; i++) {
    q.enqueue(i);
  }
  for (int i = 0; i < 300; i++) {
    q.dequeue();
  }
  for (int i = 0; i < 105; i++) {
    if (i % 2 == 0)
      q.enqueue(i);
    else
      q.dequeue();
  }
  cout << "size = "<< q.size() << " empty?" << q.isEmpty() << "\n";
  q.display();
  return 0;
}


```

 Contribution

 [@jianw851](http://jianwang.info/)


---
