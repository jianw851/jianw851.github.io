---
layout: post
category: [algorithm]
title: Naive Trie Implementation
tagline: by Jian
tags: [Trie]
---

This is a naive  trie practise.

<!--more-->

```
#include<iostream>
#include<fstream>
#include<string>

using namespace std;

class TrieNode {
public:
  bool isWord;
  TrieNode * subTrie[26];
  TrieNode() {
    isWord = false;
    for (int i = 0; i < 26; i++)
      subTrie[i] = NULL;
  }
};

class Trie {

private:
  TrieNode * root;

public:
  Trie() {
    root = new TrieNode();
  }

  ~Trie() {
    deconstruct(root);
  }
  void deconstruct (TrieNode * node) {
    if (node == NULL) return;
    for (int i = 0; i < 26; i++) {
      if (node->subTrie[i] == NULL)
        delete [] node->subTrie[i];
      else
        deconstruct (node->subTrie[i]);
    }
  }
  void addWord(string word) {
    TrieNode * curr = root;
    for (int i = 0; i < word.length(); i++) {
      int idx = word[i] - 97;
      if (idx < 0 || idx >25) continue;
      if (curr->subTrie[idx] == NULL) {
        curr->subTrie[idx] = new TrieNode();
      }
      curr = curr->subTrie[idx];
    }
    curr->isWord = true;
  }

  void buildTrie(string filename) {
    ifstream infile;
    infile.open(filename);
    if (infile.fail()) {
        cout << "open "<< filename <<" failed"<<endl;
        return;
    }
    string word = "";
    while (infile >> word) {
      addWord(word);
    }
    infile.close();
  }

  bool searchWord(string word) {
    TrieNode * curr = root;
    for (int i = 0; i < word.length(); i++) {
      int idx = word[i] - 97;
      if (idx < 0 || idx >25) return false;
      if (curr->subTrie[idx] == NULL) {
        return false;
      }
      curr = curr->subTrie[idx];
    }
    return curr->isWord;
  }

  void find(string filename) {
    ifstream infile;
    infile.open(filename);
    if (infile.fail()) {
        cout << "open "<< filename <<" failed"<<endl;
        return;
    }
    string word = "";
    while (infile >> word) {
      if (searchWord(word))
        cout << word << " : True" <<endl;
      else
        cout << word << " : False" <<endl;
    }
    infile.close();
  }
};

int main() {
  Trie trie;
  trie.buildTrie("dict.txt");
  trie.find("hw8.dat");
  return 0;
}

```

 Contribution

 [@jianw851](http://jianwang.info/)


---
