---
layout: post
category: [algorithm]
title: Subsets II 
tags: [DFS, backtracking]
---

Given a list of numbers that may has duplicate numbers, return all possible subsets
Example
If S = [1,2,2], a solution is:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
Note
Each element in a subset must be in non-descending order.
The ordering between two subsets is free.
The solution set must not contain duplicate subsets.
Challenge
Can you do it in both recursively and iteratively?

<!--more-->

	vector<vector<int> > subsetsWithDup(vector<int> &S) {
       vector<vector<int> > resultSets;
       vector<int> list;
       if (S.size() == 0) {
        resultSets.push_back(S);
        return resultSets;
       }
        sort(S.begin(), S.end());
        subDivide(resultSets, list, S, 0);
      return resultSets;
    }
    void subDivide(vector<vector <int>> &result, vector<int> &list, const vector<int> &S, int pos) {
         result.push_back(list);
         for (int i = pos; i < S.size(); i++) {
            if ((i != pos)&&S[i] == S[i-1])
            continue;
            list.push_back(S[i]);
            subDivide(result, list, S, i+1);
            list.pop_back();
        }
     }
	
---
