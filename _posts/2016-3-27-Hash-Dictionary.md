---
layout: post
category: [algorithm]
title: A Hash Function For English Dictionary 
tagline: by Jian
tags: [Hashmap]
---

This is a linear chain hash function for English dictionary (210 thousand words)

+ First serialize each word with a hash function
+ Then hash each word to a linear chain table with maxmium prime number of dictionary length
+ Output the histogram  operation steps needed when insert (conflict) 

<!--more-->

```
#include<iostream>
#include<fstream>
#include<string>
#include<vector>
#include<map>

using namespace std;

class hashNode {
public:
  unsigned long val;
  hashNode *next;
  hashNode() {
    val = 0;
    next = NULL;
  }
  hashNode (unsigned long v) {
    val = v;
    next = NULL;
  }
};

class hashTable {
public:
  vector<hashNode> hashtable;
  int hashLen;
  hashTable() {
  }
  hashTable(int size) {
    hashLen = size;
    hashtable.resize(size);
  }
  ~hashTable() {
    hashtable.clear();
  }
  unsigned long serilize(string str) {
    unsigned long hash = 5381;
    int len =  str.length();
    for (int i = 0; i < len; i++) {
        hash = ((hash<<5) + hash) + (str[len - i - 1] - 96);
    }
    return hash;
  }
  void buildHashTable(string filename, string ofilename) {
    ifstream infile;
    infile.open(filename);
    if (infile.fail()) {
        cout << "open "<< filename <<" failed"<<endl;
        return;
    }
    if (ifstream(ofilename)) {
      cout << ofilename << " already exists, delete it" << endl;
      remove(ofilename.c_str());
    }
    ofstream outfile;
    outfile.open(ofilename, ios::out | ios::app);
    if (outfile.fail()) {
        cout << ofilename <<" open failed" <<endl;
        return;
    }
    string line = "";
    while (getline(infile, line)) {
      unsigned long hash =  serilize(line);
      int idx = (hash % hashLen);
      int count = 1;
      if (hashtable[idx].val == 0) {
        hashtable[idx].val = hash;
      } else {
        hashNode newNode = hashNode(hash);
        hashNode * curr = &hashtable[idx];
        while (curr->next != NULL) {
          curr = curr->next;
          count++;
        }
        curr->next = &newNode;
      }
      outfile << count << endl;
    }
  }
  void findHashTable(string filename) {
    ifstream infile;
    infile.open(filename);
    if (infile.fail()) {
        cout << "open "<< filename <<" failed"<<endl;
        return;
    }
    string word = "";
    while (infile >> word) {
      bool canfind = false;
      unsigned long hash =  serilize(word);
      int idx = (hash % hashLen);
      if (hashtable[idx].val != 0) {
        hashNode * curr = &hashtable[idx];
        while (curr != NULL) {
          if (curr->val == hash) {
            canfind = true;
          }
          curr = curr->next;
        }
      }
      if (canfind)
       cout << word << " : true" <<endl;
      else
       cout << word << " : false" <<endl;
      word = "";
    }
  }
  void showHistogram(string filename) {
    ifstream infile;
    infile.open(filename);
    if (infile.fail()) {
        cout << "open "<< filename <<" failed"<<endl;
        return;
    }
    map<int, int> map1;
    string word = "";
    while (infile >> word) {
      int val = stoi(word);
      if (map1.find(val) != map1.end())
          map1[val]++;
      else
          map1[val] = 1;
    }
    cout <<endl<<"*******************************"<<endl;
    cout <<"         Histogram"<<endl;
    cout <<"*******************************"<<endl;
    cout << "insert      count "<<endl;
    map<int, int>::iterator itr = map1.begin();
    for (; itr != map1.end(); itr++) {
      cout << itr->first << "           " << itr->second <<endl;
    }
  }
};

int main() {
  hashTable hashtb(213557);
  hashtb.buildHashTable("dict.txt", "output3.txt");
  hashtb.findHashTable("hw8.dat");
  hashtb.showHistogram("output3.txt");
  return 0;
}

```

 Contribution

 [@jianw851](http://jianwang.info/)


---
