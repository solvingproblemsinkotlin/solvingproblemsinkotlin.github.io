---
layout: post
title:  "Validate Binary Search Tree"
date:   2020-08-19 15:00:00 +0200
categories:
  - Medium
tags:
  - tree
---

You are given the root of a binary search tree. Return true if it is a valid binary search tree, and false otherwise.
Recall that a binary search tree has the property that all values in the left subtree are less than or equal to the root, and all values in the right subtree are greater than or equal to the root.

## Example 1:

{% highlight kotlin %}

  2
 / \
1   3

Input: [2,1,3]
Output: true

{% endhighlight %}

## Example 2:

{% highlight kotlin %}

  5
 / \
1   4
   / \
  3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.

{% endhighlight %}

# Solution

A very simple recursive function. The key is in the conditions.

{% highlight kotlin %}

class Solution {
    fun isValidBST(root: TreeNode?): Boolean {
        return isValidBSTRecursive(root, null, null)
    }

    fun isValidBSTRecursive(node: TreeNode?, lower: Int?, upper: Int?): Boolean {
        if (node == null) return true
        val value: Int = node.`val`
        if (lower != null && value <= lower) return false
        if (upper != null && value >= upper) return false
        if (!isValidBSTRecursive(node.right, value, upper)) return false
        if (!isValidBSTRecursive(node.left, lower, value)) return false
        return true
    }
}

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), since we visit each node exactly once.

_Space Complexity_: O(N), since we keep up to the entire tree.

# Explain me the code!

We are going to let a recursive function to do all the logic we need.

This is very simple, if the current node we are exploring is null, we don't need further checks because we comply with binary search tree requisites.

{% highlight kotlin %}
if (node == null) return true
{% endhighlight %}

We are just saving the value in a variable, for readability purposes.

{% highlight kotlin %}
val value: Int = node.`val`
{% endhighlight %}

If the lower node is not null and its value is bigger or equals than the value of the current node we are in, return false. We don't need further checks.

{% highlight kotlin %}
if (lower != null && value <= lower) return false
{% endhighlight %}

If the upper node is not null and its value is bigger or equals than the value of the current node we are in, return false. We don't need further checks.

{% highlight kotlin %}
if (upper != null && value >= upper) return false
{% endhighlight %}

We need to check the right node. For that, we are relying in our recursive function.

{% highlight kotlin %}
if (!isValidBSTRecursive(node.right, value, upper)) return false
{% endhighlight %}

We do the same with the left node.
{% highlight kotlin %}
if (!isValidBSTRecursive(node.left, lower, value)) return false
{% endhighlight %}

After all these checks, if everything was valid, we return true.
