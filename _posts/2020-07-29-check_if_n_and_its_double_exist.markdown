---
layout: post
title:      " Check If N and Its Double Exist"
date:       2020-07-29 18:18:35 -0400
permalink:  check_if_n_and_its_double_exist
---


Some of the knowledge gaps bootcamp graduates encounter are data structures and algorithms, so I thought it might be helpful to provide a walk-through of a basic array search problem found on Leetcode.  

------------------------------

## The problem:

Given an array **arr** of integers, check if there exists two integers **N** and **M** such that **N** is the double of **M** ( i.e. N = 2 * M).

**Example 1:**<br><br>
**Input: ** ```arr = [10,2,5,3]```<br>
**Output: ** ```true```<br>
**Explanation: ** N = 10 is the double of M = 5,that is, 10 = 2 x 5.
<br><br><br>
**Example 2:**<br><br>
**Input: ** ```arr = [7,1,14,11]```<br>
**Output: ** ```true```<br>
**Explanation: ** N = 14 is the double of M = 7,that is, 14 = 2 x 7.
<br><br><br>
**Example 3: **<br><br>
**Input: ** ```arr = [3,1,7,11]```<br>
**Output: ** ```false```<br>
**Explanation: ** In this case does not exist N and M, such that N = 2 x M.

**Constraints:**
* ```2 <= arr.length <= 500```
* ```-10^3 <= arr[i] <= 10^3```

Long story short, you need to write a function ```checkIfExists(arr)``` that accepts an array of integers and returns ``true`` or ```false``` based on the requirements above.

**Before you read on, try and solve the problem yourself!**  It's so easy to skip ahead and view someone else's solution, but you rob yourself of actually *learning* the material.  Sure, you can copy and paste a solution, but do you understand the theory behind it?  Could you apply the solution to a similar, but slightly different problem?  **Allow yourself to struggle for at least 15 minutes** before looking for a hint.  This helps you really understand the methodology as well as identifying areas where you continually get stuck.  

## Solution Walkthrough (Javascript)

We are looking to see if there are two integers in a given array for which one integer in the array is the double of another interger in the array.  

**My Approach:**

I knew I needed to keep track of each value as I iterated through the array.  My first step was to create an empty array to store each "viewed" value.

```
const checkIfExist = arr => {
    let viewed = []
};
```


Using a for loop,  ``for (x of arr)``, I pushed ``x`` onto the ``viewed`` array at the end of each pass through the loop.

```
const checkIfExist = arr => {
    let viewed = []
    for (let x of arr) {
        viewed.push(x)
    }
};
```

I then was able to iterate through the provided array, returning ``true`` if ``x / 2`` or ``x * 2`` is contained in ``viewed`` or  ``false`` if no element meets the criteria.  


```
const checkIfExist = arr => {
    let viewed = []
    for (let x of arr) {
        if (viewed.includes(x/ 2) || viewed.includes(x * 2)) {
            return true
        }
        viewed.push(x)
    }
    return false
};

```

![Vince Carter saying it's over](https://media.giphy.com/media/l0ErLeqamV3UOARsA/giphy.gif)

And that's it!

Additional Resources:
* [LeetCode](https://leetcode.com/)
* [Daily Coding Problem](https://dailycodingproblem.com/)
* [Hacker Rank](http://hackerrank.com)





















