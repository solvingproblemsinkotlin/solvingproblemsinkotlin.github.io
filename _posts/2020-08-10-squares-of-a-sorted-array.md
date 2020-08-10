---
layout: post
title:  "Squares of a Sorted Array"
date:   2020-08-10 15:30:00 +0200
categories:
  - Easy
tags:
  - array
  - two pointers
---

Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

## Example 1:

{% highlight kotlin %}

Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]

{% endhighlight %}

## Example 2:

{% highlight kotlin %}

Input: [-7,-3,2,3,11]
Output: [4,9,9,49,121]

{% endhighlight %}

# Solution

{% highlight kotlin %}

fun sortedSquares(A: IntArray): IntArray {
        val N = A.size.toInt()
        var j = 0
        while (j < N && A[j] < 0) j++
        var i = j - 1
        val ans = IntArray(N)
        var t = 0
        while (i >= 0 && j < N) {
            if (A[i] * A[i] < A[j] * A[j]) {
                ans[t++] = A[i] * A[i]
                i--
            } else {
                ans[t++] = A[j] * A[j]
                j++
            }
        }
        while (i >= 0) {
            ans[t++] = A[i] * A[i]
            i--
        }
        while (j < N) {
            ans[t++] = A[j] * A[j]
            j++
        }
        return ans
    }

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), the length of the array.

_Space Complexity_: O(N).

# Explain me the code!

We initialize the needed values. Pointer __j__ for negative values, pointer __i__ for positive values.

{% highlight kotlin %}
  val N = A.size.toInt()
  var j = 0
  while (j < N && A[j] < 0) j++
  var i = j - 1
  val ans = IntArray(N)
  var t = 0
{% endhighlight %}

We iterate over the values.
- When the __i__ value is greater than the __j__ value, then we include the squared element, and we update the __i__ pointer.
- Else, we add the squared value and we update the __i__ pointer.

{% highlight kotlin %}
while (i >= 0 && j < N) {
    if (A[i] * A[i] < A[j] * A[j]) {
        ans[t++] = A[i] * A[i]
        i--
    } else {
        ans[t++] = A[j] * A[j]
        j++
    }
}
{% endhighlight %}

We fill with the remaining positive values.

{% highlight kotlin %}
while (i >= 0) {
    ans[t++] = A[i] * A[i]
    i--
}
{% endhighlight %}

We fill with the remaining negative values.

{% highlight kotlin %}
while (j < N) {
    ans[t++] = A[j] * A[j]
    j++
}
{% endhighlight %}
