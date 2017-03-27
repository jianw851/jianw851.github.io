---
layout: post
category: [algorithm]
title: A Web Problem Practice
tagline: by Jian
tags: [Graph, DFS]
---


I implemented runable c++ code for problem #1 and problem #2. And provide test using c++ cassert library. This code can only compile with c++1x.



<!--more-->

```cpp
/**********************************
compile using following command
$ g++ -std=c++11 hw.cpp -o hw
run using following command
$ ./hw < testData.txt
***********************************/
#include <iostream>
#include <unordered_map>
#include <unordered_set>
#include <string>
#include <algorithm>
#include <cassert>
#include <vector>

using namespace std;

class solution {
public:

  // getUsersByDomain function
  // time complexity: average O(1), worst case O(n)
  // n represent the length of the set of URL
  bool saveUrl(string &userToken, string &URL) {
    domainWithUsers[extractDomain(URL)].emplace(userToken);
    if (usersWithUrls[userToken].find(URL) != usersWithUrls[userToken].end()) {
       return false;
    }
    usersWithUrls[userToken].emplace(URL);
    return true;
  }

  // getUrls function
  // time complexity: O(1)
  unordered_set<string> getUrls(string &userToken) {
    return usersWithUrls[userToken];
  }

  // removeUrl function
  // time complexity: average O(1), worst case O(n)
  // n represent the length of the set of URL
  bool removeUrl(string userToken, string URL) {
    domainWithUsers[extractDomain(URL)].erase(userToken);
    if (usersWithUrls[userToken].find(URL) != usersWithUrls[userToken].end()) {
       usersWithUrls[userToken].erase(URL);
       return true;
    }
    return false;
  }

  // assume the implementation of extractDomain
  // function is like this
  // because I want it to compile
  string extractDomain(string &url) {
    return url;
  }

  // implementation of getUsersByDomain function
  // time complexity: O(1)
  unordered_set<string> getUsersByDomain(string &domain) {
    return domainWithUsers[domain];
  }

private:
  unordered_map<string, unordered_set<string> > usersWithUrls;
  unordered_map<string, unordered_set<string> > domainWithUsers;
};

// main function
// description: to test 3 functions above
int main() {
  solution solu;
  int num; // number of test cases
  int oper; // operation of the input
            // 1 : saveUrl
            // 2 : getUrl
            // 3 : removeUrl
  string userToken;
  string URL;
  bool test1; //  return value for testing saveUrl
  bool test3; //  return value for testing removeUrl
  unordered_set<string> test2; //  return value for testing getUrl
  cin >> num;
  while (num) {
    cin >> oper;
    switch (oper) {
      case 1: {
        // test function saveUrl
        cin >> userToken;
        cin >> URL;
        cin >> test1;
        bool testSave = solu.saveUrl(userToken, URL);
        assert(testSave == test1);
        break;
      } case 2: {
        // test function getUrl
        cin >> userToken;
        unordered_set<string> testGet = solu.getUrls(userToken);
        int size; // the size of test data
        cin >> size;
        while(size) {
          cin >> URL;
          test2.emplace(URL);
          size--;
        }
        assert(testGet == test2);
        test2.clear();
        break;
      } case 3: {
        // test function removeUrl
        cin >> userToken;
        cin >> URL;
        cin >> test3;
        bool testRemove = solu.removeUrl(userToken, URL);
        assert(testRemove == test3);
        break;
      }
    }
    num--;
  }
  return 0;
}

```


```cpp

/**
1. assume I have following functions
Node* getNode(string &url);
string getUrl(Node *node);
class Node {
 Node* A();
 Node* B();
 Node* C();
};
2. Ideally this file should be merged into hw.cpp as public functions.
But for compile reason, I seperated them.
**/

vector<string> getRecommendedUrls(string &userToken, string &url) {
  vector<string> urls;
  // get the user saved urls and passed this as a parameter to DFS helper function
  unordered_set<string> savedUrls = usersWithUrls[userToken];
  Node * node = getNode(url);
  // begin the DFS helper function call
  dfsHelper(urls, node, 0, savedUrls);
  return urls;
}


// An modification for helper function of Problem #3
// time complexity : O(1 + 3 + 3^2 + (3^3 * Urls) ) = O(Urls)
void dfsHelper(vector<string> &urls, Node * node, int degree, unordered_set<string> &savedUrls) {
  if (node == NULL) return; // corner case: the input is invalid
  if (degree == 3 && savedUrls.find(getUrl(node)) == savedUrls.end()) {
    urls.push_back(getUrl(node));
    return;
  }
  // begin to search A B and C
  Node * a = node->A();
  Node * b = node->B();
  Node * c = node->C();
  if (a) dfsHelper(urls, a, degree+1, savedUrls);
  if (b) dfsHelper(urls, b, degree+1, savedUrls);
  if (c) dfsHelper(urls, c, degree+1, savedUrls);
}


```

```
9
1 user1 google.com 1
1 user2 uber.com 1
1 user1 google.com 0
1 user1 hello.com 1
3 user1 google.com 1
3 user1 google.com 0
1 user1 google.com 1
2 user1 2 google.com hello.com
2 user3 0

```
