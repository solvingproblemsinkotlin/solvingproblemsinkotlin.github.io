---
layout: post
title:  "Maximum Subarray"
date:   2020-08-11 15:00:00 +0200
categories:
  - Easy
tags:
  - array
  - dynamic programming
  - divide and conquer
---

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

## Example:

{% highlight kotlin %}

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.

{% endhighlight %}

# Solution

We need to use [Kedane's algorithm!](https://medium.com/@rsinghal757/kadanes-algorithm-dynamic-programming-how-and-why-does-it-work-3fd8849ed73d#:~:text=Kadane's%20algorithm%20is%20able%20to,runtime%20of%20O(n).)

We need a variable `currentSum` to store the current accumulated value and the maximum accumulated value we have found, `maxSum`.

We are going to iterate over each number in the array. For each number
- Check if the current accumulated value `currentSum` is less than 0. In that case, set it to be 0.
- We are going to add it to the current accumulated value.
- We are updating the maximum accumulated value in case the current addition is greater than the `maxSum` we currently have.

Then, we are just returning the `maxSum`

{% highlight kotlin %}

fun maxSubArray(nums: IntArray): Int {
        var currentSum = 0
        var maxSum: Int = nums[0]
        for (number in nums) {
            currentSum = (if (currentSum < 0) 0 else currentSum) + number
            maxSum = Math.max(currentSum, maxSum)
        }
        return maxSum
}

{% endhighlight %}

If you want to check out a more difficult iteration over this problem, go read [Maximum product subarray]({% post_url 2020-08-11-maximum-product-subarray %}). It also makes use of the very same algorithm. The difference is we are multiplying instead of adding.

## Complexity Analysis

_Time Complexity_: O(N), the length of the array.

_Space Complexity_: O(1).
