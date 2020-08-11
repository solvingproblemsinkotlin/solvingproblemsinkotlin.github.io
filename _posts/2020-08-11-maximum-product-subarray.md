---
layout: post
title:  "Maximum Product Subarray"
date:   2020-08-11 15:00:00 +0200
categories:
  - Easy
tags:
  - array
  - dynamic programming
---

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

## Example 1:

{% highlight kotlin %}

Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.

{% endhighlight %}

## Example 2:

{% highlight kotlin %}

Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.

{% endhighlight %}

# Solution

We need to use [Kedane's algorithm](https://medium.com/@rsinghal757/kadanes-algorithm-dynamic-programming-how-and-why-does-it-work-3fd8849ed73d#:~:text=Kadane's%20algorithm%20is%20able%20to,runtime%20of%20O(n).) like we used the problem [Maximum subarray]({% post_url 2020-08-11-maximum-subarray %}). I recommend you to check out that problem, since it's a simpler version of this one.

{% highlight kotlin %}

fun maxProduct(nums: IntArray): Int {
      var min = nums[0]
      var max = nums[0]
      var result = max
      for (i in 1 until nums.size) {
          if (nums[i] < 0) {
              val tmp = min
              min = max
              max = tmp
          }
          max = Math.max(nums[i], max * nums[i])
          min = Math.min(nums[i], min * nums[i])
          result = Math.max(result, max)
      }
      return result
}

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), the length of the array.

_Space Complexity_: O(1).

# Explain me the code!

The variables we are needing:

- We need to keep track of the current biggest multiplication `max`.
- Since we need to multiply, we remember that 2 negative values multiplied result in on positive value. Hence, we need `min`.
- We have a `result` variable which corresponds to the biggest value we've gotten.

{% highlight kotlin %}

var min = nums[0]
var max = nums[0]
var result = max

{% endhighlight %}

For each number from the second position in the array on, if the number is negative: we swap `min` and `max` values, so they're not going to interfere with the next calculations.

Example: `[-2,3,-4]`

We are going to face the swapping when tackling the last value, `-4`. `min` will be `3` and `max` will be `-6`.

After doing this, we are just going to update both `max` and `min` values and we will update the current `result` in case `max` is greater.
{% highlight kotlin %}

for (i in 1 until nums.size) {
    if (nums[i] < 0) {
        val tmp = min
        min = max
        max = tmp
    }
    max = Math.max(nums[i], max * nums[i])
    min = Math.min(nums[i], min * nums[i])
    result = Math.max(result, max)
}

{% endhighlight %}
