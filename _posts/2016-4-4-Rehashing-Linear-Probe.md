---
layout: post
category: [algorithm]
title: Rehashing Linear Probe Practice
tagline: by Jian
tags: [Hashing, Linear Probe, Rehashing]
---

This is a implementation of Linear Probe Hashing and Rehashing, this code is based on Prof. Dov's code.

Just used to learn the general idea.


<!--more-->

### Source Code (C++)

```cpp

#include <iostream>
#include <string>
#include <stdio.h>
using namespace std;

class Hashmap {
private:
  string** table;
  int size;
  int used;
  int limit;
public:
  Hashmap() {
    size = 16;
    used = 0;
    limit = 8;
    table = new string*[16];
  }
  ~Hashmap() {
    for (int i = 0; i < size; i++)
      delete table[i];
    delete [] table;
  }
  void grow() {
    const Hashmap *old = new Hashmap(*this);
    size *= 2;
    limit *= 2;
    used = old->used;
    table = new string*[size];
    for (int i = 0; i < old->size; i++) {
      if ((old->table[i]) != nullptr) {
        add(*old->table[i]);
      }
    }
  }

  Hashmap(int init) {
    int i;
    for (i = 1; i < init; i *= 2);
    limit = i / 2;
    size = limit*2;
    table = new string*[size];
    for (int i = 0; i < size; i++)
      table[i] = nullptr;
    used = 0;
  }

  Hashmap(const Hashmap& orig)  {
    table = new string*[orig.size];
    size = orig.size;
    used = orig.used;
    limit = orig.limit;
    for (int i = 0; i < orig.size; i++)
      if (orig.table[i] == nullptr) {
        table[i] = nullptr;
      else
        table[i] = new string(*orig.table[i]);
      }
  }

  int hash1(const string &word) {
    int hashcode = 0;
    for (int i = 0; i < word.length(); i++)
      hashcode = hashcode * 32 + word[i];
    return hashcode;
  }
  int hash2(const string &word) {
    int hashcode = 0;
    for (int i = 0; i < word.length(); i++)
      hashcode = (hashcode << 13) + word[i] +(hashcode >> 17);
    return hashcode;
  }

  int hash(int v) {
    return v & (size - 1);
  }

  Hashmap& operator=(const Hashmap& orig) {
    if (this != &orig) {
      this->~Hashmap();
      table = new string*[orig.size];
      size = orig.size;
      used = orig.used;
      limit = orig.limit;
      for (int i = 0; i < orig.size; i++) {
        if (orig.table[i] == nullptr)
          table[i] = nullptr;
        else
          table[i] = new string(*orig.table[i]);
      }
    }
    return *this;
  }

  void add(const string &s) {
    used++;
    if (used > limit)
      this->grow();
    int bin = hash(stoi(s));
    int count = 0;
    while (table[bin] != nullptr) {
      bin = (bin+1) % size;
      count ++;
    }
    table[bin] = new string(s);
  }

  void display() {
    cout << used << " " << limit << " " << size<<endl;
    for (int i = 0; i < used; i++) {
     if (table[i] != nullptr)
      cout << *table[i] << "  ";
    }
    cout <<endl;
  }
};

int main() {
  Hashmap m(100);
  for (int i = 0; i < 1000; i++) {
    string s = to_string(i);
    m.add(s);
  }
  Hashmap m2 = m;
  m.display();
  m2.display();
  return 0;
}


```


### Contribution

 [@jianw851](http://jianwang.info/)


---
