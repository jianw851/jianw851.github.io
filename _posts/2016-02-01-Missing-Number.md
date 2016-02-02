---
layout: post
category: [algorithm]
title: Missing Number 
tags: [Array, Bit Manipulation, Math]
---

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

Example:

Given nums = [0, 1, 3] return 2

<!--more-->

	
解法1: 数学法（推荐）：既然是连续的数，那么就是一个等差数列，把它想象成n＋1个等差数列之和 － 给出的数列之和 ＝ 结果.
  
解法2: 位操作（推荐）， 这道题跟single number的思路差不多，当一个数异或偶数次的时候就等于0，所以将给定数列 ^ 完整数列 ＝ 结果.

解法3: hash表：（不推荐）另外开一个布尔类型的array， 按照index值存放是否访问过， 第一遍编hash，第二遍输出结果， 注意第二遍输出结果可以用for，也可以用二分法，反正复杂度已经是O(n)了，感觉二分不二分差别不大了。
  
当然还有其他方法，在此已经找到最优解，所以就不引荐了。


**复杂度**

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

```
**复杂度**

时间：O(n)

空间：O(0)

**实现二(cpp)**


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

```
**复杂度**

时间：O(n)

空间：O(n)

**实现三(cpp)**


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



## Contribution

+ [@jianw851](http://jianwang.info/)

## Reference

[^1] [268. Missing Number](https://leetcode.com/problems/missing-number/)	


---
