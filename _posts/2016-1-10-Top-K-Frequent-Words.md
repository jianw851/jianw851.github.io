---
layout: post
category: [algorithm]
title: Top K Frequent Words
tags: [data structure]
---

  Given a list of words and an integer k, return the top k frequent words in the list.
  You should order the words by the frequency of them in the return list, the most frequent one comes first. If two words has the same frequency, the one with lower alphabetical order come first.
  Do it in O(nlogk) time and O(n) extra space.
Extra points if you can do it in O(n) time with O(k) extra space.

<!--more-->
	
	 class Solution {
     public:
     class resultType {
       public:
       string word;
       int count;
       resultType(string _word, int _count) {
         word = _word;
         count = _count;
      }
      bool operator<(const resultType &oth) const {
        return count > oth.count || (count == oth.count && word < oth.word);
      }
     };
      vector<string> topKFrequentWords(vector<string>& words, int k) {
      vector<string> result;
      if (words.size() == 0 || k == 0) {
        return result;
      }
      vector<resultType> resultSet;
      map<string, int> map1;
      map<string, int>::iterator iterator1;
      for (int i = 0; i < words.size(); i++) {
       if (map1.find(words[i]) == map1.end())
         map1[words[i]] = 1;
       else
         map1[words[i]] += 1;
      }
      for (iterator1 = map1.begin(); iterator1 != map1.end(); iterator1++) {
        resultSet.push_back(resultType(iterator1->first, iterator1->second));
      }
      //sort(resultSet.begin(), resultSet.end());
      sort(resultSet.begin(), resultSet.end(),[&](resultType a, resultType b) {
        return a.count > b.count||(a.count==b.count&&a.word<b.word);});
      for (int i = 0; i < k ; i++) {
        result.push_back(resultSet[i].word);
      }
      return result;
    }
  };

---
