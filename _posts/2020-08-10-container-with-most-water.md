---
layout: post
title:  "Container With Most Water"
date:   2020-08-10 15:30:00 +0200
categories:
  - Medium
tags:
  - array
  - two pointers
---

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

## Example 1:

{% highlight kotlin %}

Input: [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: You choose 8 and 7. Min is 7. Difference between position where 7 is and position where 8 is is 8 - 1 = 7. 7*7 = 49

{% endhighlight %}

# Solution

Two pointer solution is the optimal.

{% highlight kotlin %}

fun maxArea(height: IntArray): Int {
        var maxArea = 0
        var left = 0
        var right = height.size - 1
        while (left < right) {
            maxArea = Math.max(maxArea,
                               Math.min(height[left], height[right])
                                * (right - left))

            if (height[left] < height[right]) {
                left++     
            } else {
                right--   
            }
        }
        return maxArea
}

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), the length of the array.

_Space Complexity_: O(1).

# Explain me the code!

We initialize the needed values. We need a variable to store the max area, a left and a right pointers.

{% highlight kotlin %}
var maxArea = 0
var left = 0
var right = height.size - 1
{% endhighlight %}

We iterate over the values.
- You need to find the minimum height (it's going to be one edge of the rectangle) and multiply it by the difference between the pointers.
- You have the current area. Cool. If this area is bigger than the current maximum area found, update the maximum area.

{% highlight kotlin %}
while (left < right) {
    maxArea = Math.max(maxArea,
                       Math.min(height[left], height[right])
                        * (right - left))

    ...
}
{% endhighlight %}

Finally, we need to update the pointers. We update the one who contains a lower value.

{% highlight kotlin %}
while (left < right) {
    .
    .
    .
    if (height[left] < height[right]) {
        left++     
    } else {
        right--   
    }
}
{% endhighlight %}
