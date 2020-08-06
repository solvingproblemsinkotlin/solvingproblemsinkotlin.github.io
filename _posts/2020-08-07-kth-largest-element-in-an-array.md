---
layout: post
title:  "Kth largest element in an array"
date:   2020-08-06 08:45:12 +0200
categories:
  - Medium
tags:
  - divide and conquer
  - heap
---
Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

## Example 1:

{% highlight kotlin %}

Input: [3,2,1,5,6,4] and k = 2

#=> Output: 5
{% endhighlight %}

## Example 2:

{% highlight kotlin %}

Input: [3,2,3,1,2,4,5,5,6] and k = 4

#=> Output: 4
{% endhighlight %}

# Solution

Trivial Solution: Sort the array and return the number in the `size-k` position, this will be the kth largest element.

Better Solution: We are using a heap and we are adding each element to the heap. Once the size of the heap is greater than `k`, we start removing elements from it. The next element in the heap is the number we are searching.

{% highlight kotlin %}
class Solution {
    fun findKthLargest(nums: IntArray, k: Int): Int {
        val minHeap = PriorityQueue<Int>()
        for(n in nums) {
            minHeap.add(n)
            if(minHeap.size > k) {
                minHeap.remove()
            }
        }
        return minHeap.remove()
    }
}
{% endhighlight %}

We are using a `PriorityQueue` because it follows a FIFO Algorithm (First In First Out).

## Complexity Analysis

_Time Complexity_: O(N), the cost of building the heap.

_Space Complexity_: O(N), where N is the number of elements in the array.
