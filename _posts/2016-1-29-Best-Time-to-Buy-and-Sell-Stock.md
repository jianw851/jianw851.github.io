---
layout: post
category: [algorithm]
title: Best Time to Buy and Sell Stock
tags: [Array, Dynamic Programming]
---

  Say you have an array for which the ith element is the price of a given stock on day i.If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.
  
  Example
  Given an example [3,2,3,1,2], return 1

<!--more-->

	 int maxProfit(vector<int> &prices) {
      if (prices.size() == 0) {
        return 0;
      }
      int minValue = INT_MAX, profit = INT_MIN;
      for (int i = 0; i < prices.size(); i++) {
        minValue = min(minValue, prices[i]);
        if (prices[i] - minValue > profit) {
          profit = prices[i] - minValue;
        }
      }
      return profit;
    }
	
---
