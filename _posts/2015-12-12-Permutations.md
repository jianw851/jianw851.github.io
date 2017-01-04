---
layout: post
category: [algorithm]
title: Permutations 
tags: [DFS, backtracking]
---

Given a list of numbers, return all possible permutations.
Example
For nums = [1,2,3], the permutations are:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
Challenge
Do it without recursion.

<!--more-->

	 vector<vector<int> > permute(vector<int> nums) {
     vector<vector<int> > resultSets;
     vector<int> list;
     if (nums.size() == 0) {
        return resultSets;
     }
     permutation(resultSets, list, nums);
    return resultSets;
    }
    void permutation(vector<vector<int> > &result, vector<int> &list, vector<int> &nums) {
        if (list.size() == nums.size()) {
          result.push_back(list);
        } else {
            for (int i = 0; i < nums.size(); i++) {
            if (count(list.begin(), list.end(), nums[i]) > 0) {
             continue;
            }
             list.push_back(nums[i]);
             permutation(result, list, nums);
             list.pop_back();
            }
        }
    }
	
---
