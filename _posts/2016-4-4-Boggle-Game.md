---
layout: post
category: [algorithm]
title: Boggle Game
tagline: by Jian
tags: [DFS, Back Tracking, Boggle]
---

This is a implementation of Boggle game using Trie.


<!--more-->

### Source Code (C++)

```cpp
#include<iostream>
#include<fstream>
#include<string>
#include<vector>
#include<unordered_map>
#include<algorithm>

using std::cout;
using std::string;
using std::ifstream;
using std::ofstream;
using std::vector;
using std::unordered_map;
using std::count_if;
using std::for_each;
using std::ios;

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
    destruct(root);
    if (root != NULL)
      delete root;
  }
  void destruct (TrieNode * node) {
    if (node == NULL) return;
    for (int i = 0; i < 26; i++) {
      if (node->subTrie[i] != NULL) {
        destruct(node->subTrie[i]);
        delete node->subTrie[i];
      }
    }
  }
  TrieNode * getRoot() {
    return root;
  }
  char toLower(char c) {
    int num = c - 0;
    if (num > 64 && num < 91)
      return num + 32;
    else
      return c;
  }
  void add(string word) {
    TrieNode * curr = root;
    for (int i = 0; i < word.length(); i++) {
      int idx = toLower(word[i]) - 97;
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
        cout << "open "<< filename <<" failed\n";
        return;
    }
    string word = "";
    while (infile >> word) {
      add(word);
    }
    infile.close();
  }

  bool contains(string word) {
    TrieNode * curr = root;
    for (int i = 0; i < word.length(); i++) {
      int idx = toLower(word[i]) - 97;
      if (idx < 0 || idx >25) return false;
      if (curr->subTrie[idx] == NULL) {
        return false;
      }
      curr = curr->subTrie[idx];
    }
    return curr->isWord;
  }

  bool containsPrefix(string word) {
    TrieNode * curr = root;
    for (int i = 0; i < word.length(); i++) {
      int idx = toLower(word[i]) - 97;
      if (idx < 0 || idx >25) return false;
      if (curr->subTrie[idx] == NULL) {
        return false;
      }
      curr = curr->subTrie[idx];
    }
    return true;
  }
  TrieNode * containsPrefix_Faster(TrieNode * curr, char c) {
      int idx = toLower(c) - 97;
      if (idx < 0 || idx >25) return NULL;
      return curr->subTrie[idx];
  }
};
class Boggle {
private:
  int size;
  vector<char> board;
  Trie trie;
public:
  Boggle(){}
  ~ Boggle() {
    board.clear();
  }
  void init(string bogglefile, string triefile) {
    trie.buildTrie(triefile);
    ifstream infile;
    infile.open(bogglefile);
    if (infile.fail()) {
        cout << "open "<< bogglefile <<" failed\n";
        return;
    }
    infile >> size;
    board = vector<char>(size * size, '#');
    int i = 0;
    char letter;
    while (infile >> letter) {
      board[i++] = letter;
    }
    infile.close();
  }
  void play(string outputfile) {
    unordered_map<string, int> hashmap;
    vector<int> visited;
    vector<int> x = {-1, -1, -1, 0, 1, 1, 1, 0};
    vector<int> y = {-1, 0, 1, 1, 1, 0, -1, -1};
    for (int i = 0; i < size * size; i++)
      backTracking(hashmap, visited, i, trie.getRoot(), x, y);
    // print the result
    ofstream outfile;
    outfile.open(outputfile, ios::out | ios::app);
    if (outfile.fail()) {
      cout << outputfile << "open fail!\n";
      return;
    }
    unordered_map<string, int>::iterator itr;
    for (itr = hashmap.begin(); itr != hashmap.end(); itr++) {
         outfile << itr->first <<" " << itr->second <<"\n";
         cout << itr->first <<" " << itr->second <<"\n";
    }
    outfile.close();
  }
  void backTracking(unordered_map<string, int> &hashmap,
    vector<int> visited, int pos, TrieNode * curr,
    vector<int> &x, vector<int> &y) {
    TrieNode * nextptr = trie.containsPrefix_Faster(curr, board[pos]);
   if ( nextptr == NULL) {
     return;
   } else {
      if (nextptr->isWord && visited.size() > 1) {
        string word;
        for_each(visited.begin(), visited.end(), [this, &word](int n) {
          word.push_back(board[n]);
        });
        word.push_back(board[pos]);
        if (hashmap.find(word) != hashmap.end())
          hashmap[word]++;
        else
          hashmap[word] = 1;
      }
      visited.push_back(pos);
      // find both unique and valid positions
      int i = (pos / size), j = (pos % size);
      for (int k = 0; k < 8; k++) {
         i += x[k]; j += y[k];
        if (i > -1 && i < size &&
            j > -1 && j < size ) {
          pos = i * size + j;
          if (count_if(visited.begin(), visited.end(),
            [&pos](int num){ return num == pos;}) == 0) {
            backTracking(hashmap, visited, pos, nextptr, x, y);
          }
        }
        i -= x[k]; j -= y[k];
      }
   }
 }
};
int main() {
  Boggle boggle;
  boggle.init("boggle.dat", "dictionary.txt");
  boggle.play("bogglewords.txt");
  return 0;
}

```

### Test files

+ [dictionary.txt](https://drive.google.com/file/d/0B4WEFlVUmo6xei1zWHF5U0RKd2s/view)

+ [boggle.dat](https://drive.google.com/file/d/0Bwxfq4Y7f7vkSl92ZkxoMm12cEE/view?usp=sharing)

### Output

+ [bogglewords.txt](../../../../files/bogglewords.txt)

### Contribution

 [@jianw851](http://jianwang.info/)


---
