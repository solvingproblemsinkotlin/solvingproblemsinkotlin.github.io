---
layout: post
title:  "Spiral Matrix"
date:   2020-08-07 08:33:12 +0200
categories:
  - Medium
tags:
  - array
---
Given a matrix of __m x n__ elements (__m__ rows, __n__ columns), return all elements of the matrix in spiral order.

## Example 1:

{% highlight kotlin %}

**Input:**
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
**Output:** [1,2,3,6,9,8,7,4,5]

{% endhighlight %}

## Example 2:

{% highlight kotlin %}

**Input:**
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
**Output:** [1,2,3,4,8,12,11,10,9,5,6,7]

{% endhighlight %}

# Solution

{% highlight kotlin %}

class Solution {
    fun spiralOrder(matrix: Array<IntArray>): List<Int> {
        val nums = mutableListOf<Int>()
        if(matrix.size == 0) {
            return nums
        }
        var top = 0
        var bottom = matrix.size - 1
        var left = 0
        var right = matrix[0].size - 1
        var size = matrix.size * matrix[0].size

        while(nums.size < size) {
            for(i in left..right) {
                if(nums.size < size) {
                    nums.add(matrix[top][i])   
                }
            }
            top++
            for(i in top..bottom) {
                if(nums.size < size) {
                    nums.add(matrix[i][right])
                }
            }
            right--
            for(i in right downTo left) {
                if(nums.size < size) {
                    nums.add(matrix[bottom][i])
                }
            }
            bottom--
            for(i in bottom downTo top) {
                if(nums.size < size) {
                    nums.add(matrix[i][left])
                }
            }
            left++
        }
        return nums
    }
}

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), where N is the total number of elements in the input matrix. We add every element in the matrix to our final answer.

_Space Complexity_: O(N), we have to populate the result array

# Explain me the code!

We need to create a list to store the result values of traversing the matrix in spiral order. If your matrix is empty, you return this list!

{% highlight kotlin %}
val nums = mutableListOf<Int>()
if(matrix.size == 0) {
    return nums
}
{% endhighlight %}

If you are not so lucky, is time to create the variables we're going to need:

- A variable indicating where is the top of our matrix at any moment. It will be 0.
- A variable indicating where is the bottom of our matrix at any moment. It will be the last position of the matrix (it's length - 1).
- A variable indicating where is the left side of our matrix at any moment. It will be 0.
- A variable indicating where is the right side of our matrix at any moment. It will be the last position of any array in the `Array<IntArray>`. This means, you take the first element in the array (it will be the `IntArray`, which is the equivalent of a row in a matrix), and then you take it's length - 1 (you want the last position, remember).
- A variable representing the number of elements in the matrix. This will also be your result list's size.

{% highlight kotlin %}
var top = 0
var bottom = matrix.size - 1
var left = 0
var right = matrix[0].size - 1
val size = matrix.size * matrix[0].size
{% endhighlight %}

Here comes the traversing fun! We are going to run this while loop until the size of our result list is equals to the size of our matrix.
Remember, the size of our matrix is `val size = matrix.size * matrix[0].size`.

{% highlight kotlin %}
while(nums.size < size) {
    for(i in left..right) {
        if(nums.size < size) {
            nums.add(matrix[top][i])   
        }
    }
    top++
    for(i in top..bottom) {
        if(nums.size < size) {
            nums.add(matrix[i][right])
        }
    }
    right--
    for(i in right downTo left) {
        if(nums.size < size) {
            nums.add(matrix[bottom][i])
        }
    }
    bottom--
    for(i in bottom downTo top) {
        if(nums.size < size) {
            nums.add(matrix[i][left])
        }
    }
    left++
}
{% endhighlight %}

Inside our while loop, we are going to start by traversing the matrix from left to right in the **top row** and adding this to the result array.
Once we are done, we need to increment the top variable, in order to not traverse the same row once and again.

{% highlight kotlin %}
for(i in left..right) {
    if(nums.size < size) {
        nums.add(matrix[top][i])   
    }
}
top++
{% endhighlight %}

It's time to move from top to bottom! We are going to do the same operation as before but in the **right column**.
When we are finished, we need to decrement the pointer to the right column.

{% highlight kotlin %}
for(i in top..bottom) {
    if(nums.size < size) {
        nums.add(matrix[i][right])
    }
}
right--
{% endhighlight %}

Now, we are moving from left to right in the **bottom row**. After that, we are decrementing our bottom row pointer.

{% highlight kotlin %}
for(i in right downTo left) {
    if(nums.size < size) {
        nums.add(matrix[bottom][i])
    }
}
bottom--
{% endhighlight %}

Finally, we are traversing from bottom to top in the **left column**. Then, we increment the left column pointer.

{% highlight kotlin %}
for(i in bottom downTo top) {
    if(nums.size < size) {
        nums.add(matrix[i][left])
    }
}
left++
{% endhighlight %}

We are done adding the elements of the matrix in spiral order. The last piece of code? Just return the result list!
