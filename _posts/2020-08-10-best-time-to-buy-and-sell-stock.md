---
layout: post
title:  "Best Time to Buy and Sell Stock"
date:   2020-08-10 08:47:00 +0200
categories:
  - Easy
tags:
  - array
  - dynamic programming
---

This problem is also known as __Maximum Profit From Stocks__.

You are given an array. Each element represents the price of a stock on that particular day. Calculate and return the maximum profit you can make from buying and selling that stock only once.

## Example 1:

{% highlight kotlin %}

Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
{% endhighlight %}

## Example 2:

{% highlight kotlin %}

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

{% endhighlight %}

# Solution

Instead of going brute-force on this using a couple of for loops, think about this array as if it was a graph.

{% highlight kotlin %}

class Solution {
    var maxProfit: Int = 0
    var minPrice = Integer.MAX_VALUE

    fun maxProfit(prices: IntArray): Int {
        for(i in 0 until prices.size) {
            if(prices[i] < minPrice) {
                minPrice = prices[i]
            } else if (prices[i] - minPrice > maxProfit) {
                maxProfit = prices[i] - minPrice
            }
        }
        return maxProfit
    }
}

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), only a single iteration over the array is needed.

_Space Complexity_: O(1), only 2 variables are used.

# Explain me the code!

We are needing a couple variables. One for storing the max profit we are able to make and another one for tracking the lowest price found.

{% highlight kotlin %}
  var maxProfit: Int = 0
  var minPrice = Integer.MAX_VALUE
{% endhighlight %}

{% highlight kotlin %}
We are iterating over all the values in the array and returning the max profit.
fun maxProfit(prices: IntArray): Int {
    for(i in 0 until prices.size) {
        .
        .
        .
    }
    return maxProfit
}
{% endhighlight %}

Inside the for loop, we check if we have found a lower price than we currently have and, if so, we update it.

{% highlight kotlin %}
if(prices[i] < minPrice) {
    minPrice = prices[i]
}
{% endhighlight %}

On the other hand, if we don't have a lower price, we check if the difference between the current price and the min price is greater than our max profit. If so, we update it.

{% highlight kotlin %}
if(prices[i] < minPrice) {
    minPrice = prices[i]
} else if (prices[i] - minPrice > maxProfit) {
    maxProfit = prices[i] - minPrice
}
{% endhighlight %}
