---
layout: post
category: [algorithm]
title: Total Occurrence of Target 
tags: [Binary Search]
---

Given a target number and an integer array sorted in ascending order. Find the total number of occurrences of target in the array.
Given [1, 3, 3, 4, 5] and target = 3, return 2.
Given [2, 2, 3, 4, 6] and target = 4, return 1.
Given [1, 2, 3, 4, 5] and target = 6, return 0.
Challenge
Time complexity in O(logn)

<!--more-->
	
	class Solution {
public:
    /**
     * @param A an integer array sorted in ascending order
     * @param target an integer
     * @return an integer
     */
    int totalOccurrence(vector<int>& A, int target) {
      if (A.size() == 0) {
        return 0;
      } else if (target < A[0]||target > A[A.size()-1]) {
        return 0;
      }
      if (A.size() == 1&&A[0] == target) {
        return 1;
      }
      int begin = 0;
      int end = A.size() - 1;
      while (begin != end -1) {
        int mid = (begin + end)/2;
        if (A[mid] == target) {
          int leftIdx = leftSearch(A, target, begin, mid);
          int rightIdx = rightSearch(A, target, mid, end);
          return rightIdx - leftIdx + 1;
        } else if (A[mid] > target) {
          end = mid;
        } else {
          begin = mid;
        }
      }
      if (A[begin] == target) {
        return 1;
      } else if (A[end] == target) {
        return 1;
      } else {
        return 0;
      }
    }
    int leftSearch(vector<int>& A, int target, int begin, int end) {
      if (begin == end - 1) {
        if (A[begin] == target) {
          return begin;
        } else {
          return end;
        }
      }
      int mid = (begin + end)/2;
      if (A[mid] ==  target) {
        leftSearch(A, target, begin, mid);
      } else {
        leftSearch(A, target, mid, end);
      }
    }
     int rightSearch(vector<int>& A, int target, int begin, int end) {
      if (begin == end - 1) {
        if (A[end] == target) {
          return end;
        } else {
          return begin;
        }
      }
      int mid = (begin + end)/2;
      if (A[mid] ==  target) {
        rightSearch(A, target, mid, end);
      } else {
        rightSearch(A, target, begin, mid);
      }
    }
};

---
