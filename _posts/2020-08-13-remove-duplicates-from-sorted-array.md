---
layout: post
title:  "Remove Duplicates from Sorted Array"
date:   2020-08-13 15:00:00 +0200
categories:
  - Easy
tags:
  - array
  - two pointers
  - divide and conquer
---

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

## Example 1:

{% highlight kotlin %}

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.

{% endhighlight %}

## Example 2:

{% highlight kotlin %}

Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.

{% endhighlight %}

# Solution

Once an element is encountered, you simply need to bypass its duplicates and move on to the next unique element.

{% highlight kotlin %}

fun removeDuplicates(nums: IntArray): Int {
    var index = 1
    for(i in 0 until nums.size - 1) {
        if(nums[i] != nums[i+1]) {
            nums[index++] = nums[i + 1]
        }
    }
    return index
}

Why `var ìndex = 1`? Essentially, the very first element in the array is going to be unique.
We return the `index` because it's going to be actually the size of the array after removing the duplicates.

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), the length of the array.

_Space Complexity_: O(1).
