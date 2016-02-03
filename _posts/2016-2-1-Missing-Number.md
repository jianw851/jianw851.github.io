---
layout: post
category: [algorithm]
title: Missing Number 
tagline: by Jian
tags: [Array, Bit Manipulation, Math]
---

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

Example:

Given nums = [0, 1, 3] return 2

<!--more-->


复杂度

时间：O(n)

空间：O(1)

实现一(cpp) 



	class Solution {
public:
   int missingNumber(vector<int>& nums) {
      if (nums.size() == 0) return 0;
      int sum = 0;
      int n = nums.size();
      for (int i = 0; i < nums.size(); i++) {
        sum += nums[i];
      }
      return (n+1)*n/2 - sum;
    }
	};


复杂度

时间：O(n)

空间：O(0)

实现二(cpp)


	class Solution {
public:
    int missingNumber(vector<int>& nums) {
      if (nums.size() == 0) return 0;
      int result = 0;
      for (int i = 0; i < nums.size(); i++) {
         result ^= (i+1) ^ nums[i];
      }
      return result;
    }
	};


复杂度

时间：O(n)

空间：O(n)

实现三(cpp)


	class Solution {
public:
   int missingNumber(vector<int>& nums) {
      if (nums.size() == 0) return 0;
      vector<bool> list(nums.size(), true);
      for (int i = 0; i < nums.size(); i++) {
        list[nums[i]] = false;
      }
      int i = 0;
      for (; i < list.size(); i++) {
        if (list[i]) return i;
      }
      return i;
    }
	};



 Contribution

 [@jianw851](http://jianwang.info/)

 Reference

 [268. Missing Number](https://leetcode.com/problems/missing-number/)	


---
