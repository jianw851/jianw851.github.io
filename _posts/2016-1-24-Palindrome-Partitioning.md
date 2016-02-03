---
layout: post
category: [algorithm]
title: Palindrome Partitioning
tags: [graph, dfs]
---

  Given a string s, partition s such that every substring of the partition is a palindrome.

  Return all possible palindrome partitioning of s.

  Example
  Given s = "aab", return:

  [
    ["aa","b"],
    ["a","a","b"]
  ]


<!--more-->

	vector<vector<string>> partition(string s) {
      vector<vector<string>> result;
      if (s.length() == 0) return result;
      vector<string> list;
      dfs_traverse(result, list, s, 0);
      return result;
    }
    bool isParlindrome(string s) {
      int left = 0, right = s.length() - 1;
      while (left <= right) {
        if (s[left] != s[right]) {
          break;
        } else {
          left++; right--;
        }
      }
      if (left <= right)
        return false;
      return true;
    }
    void dfs_traverse(vector<vector<string>> &result, vector<string> list, string s, int pos) {
      int len = s.length();
      if (pos == len) {
        result.push_back(list);
      } else {
       for (int i = 1; i <= len - pos; i++) {
         string temp = s.substr(pos, i);
         if (!isParlindrome(temp))
         continue;
         list.push_back(temp);
         dfs_traverse(result, list, s, pos+i);
         list.pop_back();
       }
     }
	}
	
---
