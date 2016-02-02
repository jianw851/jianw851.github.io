---
layout: post
category: Algorithm
title: Power Of Two
tagline: by Jian
tags: [bit manipulation]
---

<!--more-->

# Problem 231 Power of Two
 Given an integer, write a function to determine if it is a power of two.

Example 1:

n = 12

return false

Example 2:

n = 64

return true


解法1: 数学法， 2的幂不管怎样二分，都能被2整除，直到变为1.
  
解法2: 位操作， 2的幂在二进制表示的时候，有一个特性，那就是只有一个1在里面（如：00001000就是2的幂，而00001100就不是2的幂），利用这个特性我们就可以衍生出三种解法都可以达到用O(1)的时间复杂度.

1. 移位法：把后面的0移掉，剩下的部分＝＝1，就对了 (不推荐)
2. －1求与：n & n-1 == 0 就对了 （推荐）
3. 补数求与： (n & (~n + 1)) == n 就对了 （尚可）
  
网上对这道题的分析太透彻，其他的解法我就不再赘述，把链接贴在reference大家自己看。我就把两种解法写出来。


**复杂度**

时间：O(1)

空间：O(0)

**实现一(cpp)** 

	class Solution {
public:
    bool isPowerOfTwo(int n) {
      return n > 0 && ((n & (n - 1)) == 0);
    }
	};
**复杂度**

时间：O(logn)

空间：O(1)
**实现二(cpp)**

	class Solution {
public:
    bool isPowerOfTwo(int n) {
      if (n <= 0) return false;
      while (n != 1) {
        if (n % 2 != 0)
        return false;
        n /= 2;
      }
      return true;
    }
	};




## Contribution

+ [@jianw851](http://jianwang.info/)

## Reference

[^1] [231. Power of Two](https://leetcode.com/problems/power-of-two/)

[^2] [Ten Ways to Check if an Integer Is a Power Of Two in C](http://www.exploringbinary.com/ten-ways-to-check-if-an-integer-is-a-power-of-two-in-c/)

 

