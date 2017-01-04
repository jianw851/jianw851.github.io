---
layout: post
category: [algorithm]
title: Ugly Number II 
tagline: by Jian
tags: [Dynamic Programming, Math, Heap, Three Pointer]
---

 Problem 264 Ugly Number II

 Write a program to find the n-th ugly number.

  Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

  Note that 1 is typically treated as an ugly number.

  Hint: The naive approach is to call isUgly for every number until you reach the nth one. Most numbers are not ugly. Try to focus your effort on generating only the ugly ones. An ugly number must be multiplied by either 2, 3, or 5 from a smaller ugly number.

Example 1:

 n = 10 return 12

<!--more-->

## Solution

+ C++

## Analysis

解法1: Brute Force： 此暴力破解还稍微带点动态规划的意味在里面。 思路是利用它的一个规律。 打个比喻：即从最小的丑数开始，“1， 2，3，4，5...”，你会发现如果把前面这串数字当成一个保龄球轨道的话，那么“2，3，5”这个就是一个滚动的保龄球，从头开始滚动，保龄球与轨道接触的那一面的数字相乘的结果（去重复后）往轨道最后放。相切的点就是的结果。但是这样的方法有很多明显的缺陷，为了去重要多花费2n的空间（6*3等于9*2重复） ，而且实际执行的次数要多于n。
  
解法2: 三指针： 与以上解法相比，此解法发现了真正的pattern。还拿以上例子来讲，就是把保龄球换成蜗牛，三个蜗牛（数字分别是2，3，5）起初都在起跑线上，谁与轨道的乘积最小谁就往前爬一步，这样当出现重复数字的时候，都会在同一个循环里，（即3*6与2*9两个最小值在同时出现，那么两者都往前爬一步），这样就省了去重复的多余空间和操作。



**复杂度**

时间：O(n)

空间：O(n)

**实现一(cpp)** 


	class Solution {
public:
    long long nthUglyNumber1(int n) {
     if (n == 0) return 0;
     unordered_set<long long> set1;
     vector<int> ugly = {2,3,5};
     priority_queue<long long> queue1;
     for (int i = 1; i < 6; i++ ) {
       queue1.push(-i);
       set1.emplace(i);
     }
     long long result;
     for (int i = 0; i < k; i++) {
       result = -queue1.top();
       queue1.pop();
       for (int j = 0; j < 3; j++) {
         if (set1.find(ugly[j]*result) == set1.end()) {
           queue1.push(-ugly[j]*result);
           set1.emplace(ugly[j]*result);
         }
       }
     }
     return result;
  }
	};

**复杂度**

时间：O(n)

空间：O(n)

**实现二(cpp)** 


	class Solution {
public:
    int nthUglyNumber(int n) {    
        vector<int> result(1, 1);
        int i2 = 0, i3 = 0, i5 = 0;
        while (result.size() < n) {
            int m2 = result[i2] * 2, 
                m3 = result[i3] * 3, 
                m5 = result[i5] * 5;
            int mn = min(m2, min(m3, m5));
            if (mn == m2) ++i2;
            if (mn == m3) ++i3;
            if (mn == m5) ++i5;
            result.push_back(mn);
        }
        return result.back();
    }
	};

* 596 / 596 test cases passed.
* Status: Accepted
* Runtime: 20 ms
* Beats: 48.17%

**实现三(cpp)**


	public class Solution {
    public int nthUglyNumber(int n) {
        int[] ugly = new int[n];
        int v2 = 1, v3 = 1, v5 = 1;
        int i2 = 0, i3 = 0, i5 = 0;
        for (int k = 0; k < n; ++k) {
            int v = Math.min(v2, Math.min(v3, v5));
            ugly[k] = v;
            if (v2 == v) v2 = ugly[i2++] * 2;
            if (v3 == v) v3 = ugly[i3++] * 3;
            if (v5 == v) v5 = ugly[i5++] * 5;
        }
        return ugly[n-1];
    }
	}

* 596 / 596 test cases passed.
* Status: Accepted
* Runtime: 8 ms
* Beats: 90.84%

**实现四(Java)**


	public class Solution {
    public int nthUglyNumber(int n) {
        int[] ugly = new int[n];
        int v2 = 1, v3 = 1, v5 = 1;
        int i2 = 0, i3 = 0, i5 = 0;
        for (int k = 0; k < n; ++k) {
            int v = Math.min(v2, Math.min(v3, v5));
            ugly[k] = v;
            if (v2 == v) v2 = ugly[i2++] * 2;
            if (v3 == v) v3 = ugly[i3++] * 3;
            if (v5 == v) v5 = ugly[i5++] * 5;
        }
        return ugly[n-1];
    }
	}

* 596 / 596 test cases passed.
* Status: Accepted
* Runtime: 8 ms
* Beats: 85.65%

**实现五(Python)**

	def nthUglyNumber(self, n):
    ugly = [1] * n
    i2 = i3 = i5 = -1
    x = v2 = v3 = v5 = 1
    for k in xrange(n):
        x = min(v2, v3, v5)
        ugly[k] = x
        if x == v2:
            i2 += 1
            v2 = ugly[i2] * 2
        if x == v3:
            i3 += 1
            v3 = ugly[i3] * 3
        if x == v5:
            i5 += 1
            v5 = ugly[i5] * 5
    return x


* 596 / 596 test cases passed.
* Status: Accepted
* Runtime: 176 ms
* 94.23%


 Contribution

 [@jianw851](http://jianwang.info/)

## Reference

[^1] [264. Ugly Number II ](https://leetcode.com/problems/ugly-number-ii/)

[^2] [博客园Grandyang](http://www.cnblogs.com/grandyang/p/4743837.html)

---
