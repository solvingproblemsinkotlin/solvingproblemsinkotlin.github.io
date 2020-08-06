---
layout: post
title:  "K Closest Points to Origin"
date:   2020-08-06 10:45:12 +0200
categories:
  - Medium
tags:
  - divide and conquer
  - heap
  - sort
---
We have a list of points on the plane.  Find the K closest points to the origin (0, 0).

(Here, the distance between two points on a plane is the Euclidean distance.)

You may return the answer in any order.  The answer is guaranteed to be unique (except for the order that it is in.)

## Example 1:

{% highlight kotlin %}

Input: points = [[1,3],[-2,2]], K = 1
Output: [[-2,2]]
Explanation:
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest K = 1 points from the origin, so the answer is just [[-2,2]].

{% endhighlight %}

## Example 2:

{% highlight kotlin %}

Input: points = [[3,3],[5,-1],[-2,4]], K = 2
Output: [[3,3],[-2,4]]
(The answer [[-2,4],[3,3]] would also be accepted.)

{% endhighlight %}

__Notes__

- 1 <= K <= points.length <= 10000
- -10000 < points[i][0] < 10000
- -10000 < points[i][1] < 10000


# Solution

If you receive an array with only one element, yuhu! no computation needed. Just return that array!

__If you are not so lucky:__

- Create a map where the key is the pair of coordinates and the value is their distance to the origin.
- Create a PriorityQueue. This PriorityQueue needs to follow a descending order, so larger values will be at the head.
- Add the pairs of coordinates to the Queue. If the size of the Queue gets bigger than K, then remove the first element.
- Create a list with the first K elements and return it.

{% highlight kotlin %}

class Solution {
    fun kClosest(points: Array<IntArray>, K: Int): Array<IntArray> {
        if(points.size == 1) {
            return points
        }

        val distances: MutableMap<IntArray, Double> = HashMap()
        for (pair in points) {
            distances[pair] = Math.sqrt(Math.pow(pair[0].toDouble(), 2.0) + Math.pow(pair[1].toDouble(), 2.0))
        }

        val heap: Queue<IntArray> = PriorityQueue<IntArray>(compareByDescending { distances[it] })

        for (n in distances.keys) {
            heap.add(n)
            if (heap.size > K) heap.remove()
        }

        val top = mutableListOf<IntArray>()
        for (i in 0 until K) {
            top.add(heap.poll())
        }
        return top.toTypedArray()
    }
}

{% endhighlight %}

## Complexity Analysis

_Time Complexity_: O(N), Building the distances + Building the heap + building the returning array.

_Space Complexity_: O(N), where N is the number of elements in the array.
