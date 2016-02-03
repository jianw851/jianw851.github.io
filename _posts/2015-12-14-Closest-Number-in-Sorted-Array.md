---
layout: post
category: [algorithm]
title: Closest Number in Sorted Array 
tags: [Binary Search]
---

Given a target number and an integer array A sorted in ascending order, find the index i in A such that A[i] is closest to the given target.
Return -1 if there is no element in the array.
Given [1, 2, 3] and target = 2, return 1.
Given [1, 4, 6] and target = 3, return 1.
Given [1, 4, 6] and target = 5, return 1 or 2.
Given [1, 3, 3, 4] and target = 2, return 0 or 1 or 2.
There can be duplicate elements in the array, and we can return any of the indices with same value.
O(logn) time complexity.

<!--more-->
	int closestNumber(vector<int>& A, int target) {
      if (A.size() == 0) {
        return -1;
      } else if (A.size() == 1) {
        return 0;
      }
      int begin = 0;
      int end = A.size() - 1;
      while (begin != end - 1) {
        int mid = (begin + end)/2;
        if (A[mid] == target) {
          return mid;
        } else if (A[mid] > target) {
          end = mid;
        } else {
          begin = mid;
        }
      }
      if (A[begin] == target) {
        return begin;
      } else if (A[end] == target) {
        return end;
      } else if (A[end] - target >= target - A[begin]) {
        return begin;
      } else if (A[end] - target < target - A[begin]) {
        return end;
      }
    }
	
---
