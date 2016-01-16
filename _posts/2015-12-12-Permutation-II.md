---
layout: post
category: [algorithm]
title: Permutations II 
tags: [DFS, backtracking]
---
Given a list of numbers with duplicate number in it. Find all unique permutations.
Example
For numbers [1,2,2] the unique permutations are:
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
Challenge
Using recursion to do it is acceptable. If you can do it without recursion, that would be great!

<!--more-->

	vector<vector<int> > permuteUnique(vector<int> &nums) {
      vector<vector<int> > resultSets;
      vector<int> list;
      if (nums.size() == 0) {
        resultSets.push_back(list);
        return resultSets;
      }
      vector<bool> visited(nums.size());
      for_each(visited.begin(), visited.end(), [&](bool x) { x = false;});
      sort(nums.begin(), nums.end());
      permutation(resultSets, list, nums, visited);
      return resultSets;
    }
    void permutation(vector<vector<int> > &result, vector<int> &list,
                     vector<int> &nums, vector<bool> &visited) {
        if (list.size() == nums.size()) {
          result.push_back(list);
        } else {
          for (int i = 0; i < nums.size(); i++) {
            if (visited[i] == true||(i != 0&&nums[i] == nums[i-1]&&visited[i-1] == false)) {
              continue;
            }
            visited[i] = true;
            list.push_back(nums[i]);
            permutation(result, list, nums, visited);
            list.pop_back();
            visited[i] = false;
          }
        }
    }

	
---
