---
layout: post
title:      "Compare the Triplets : JavaScript Solution"
date:       2020-08-08 01:35:30 +0000
permalink:  compare_the_triplets_javascript_solution
---


*I try to carve out about 2 hours a day to work on code problems.  In addition to solving them, I find it really useful to write a brief expanation of my process.  It gets me in the habit of putting words to my coding decisions, a skill that interviewers want to see when you're working through a technical problem.  Writing out the approach also helps with remembering certain strategies when encountering similar problems down the road.*

## Compare the Triplets

Lula and Jack each wrote their own sitcom pilot.  They asked a friend to rate the two pilots, awarding points on a scale from 1 to 100 for three categories: originality, humor, and storyline.

The rating for Lula's sitcom, "Dinosaur Wall Street" is the triplet a = (a[0], a[1], a[2]), and the rating for Jack's sitcom, "Small Town Napkin Factory" is the triplet b = (b[0], b[1], b[2]).

Your task is to find their comparison points by comparing a[0] with b[0], a[1] with b[1], and a[2] with b[2].

* If a[i] > b[i], then Lula is awarded 1 point.
* If a[i] < b[i], then Jack is awarded 1 point.
* If a[i] = b[i], then neither person receives a point.

Comparison points are the total points a person earned.

Given a and b, determine their respective comparison points.

**Example**

a = [1, 2, 3]
b = [3, 2, 1]
* For elements *0*, Jack is awarded a point because a[0] .
* For the equal elements a[1] and b[1], no points are earned.
* Finally, for elements 2, a[2] > b[2] so Lula receives a point.

The return array is [1, 1] with Lula's score first and Jack's second.

**Function Description**

Complete the function compareTriplets in the editor below.

compareTriplets has the following parameter(s):

* int a[3]: Lula's challenge rating
* int b[3]: Jack's challenge rating

**Return**

* int[2]: Lula's score is in the first position, and Jack's score is in the second.

**Input Format**

The first line contains 3 space-separated integers, a[0], a[1], and a[2], the respective values in triplet a.
**
The second line contains 3 space-separated integers, b[0], b[1], and b[2], the respective values in triplet b.

**Constraints**

* 1 ≤ a[i] ≤ 100
* 1 ≤ b[i] ≤ 100


**Sample Input 0**

``[5, 6, 7]``

``[3, 6, 10]``


**Sample Output 0**

```[1, 1]```

**Explanation 0**

In this example:

* a = (a[0], a[1], a[2]) = (5,6,7)
* b = (b[0], b[1], b[2]) = (3, 6, 10)

Now, let's compare each individual score:

* a[0] > b[0], so Lula receives 1 point.
* a[1] = b[1], so nobody receives a point.
* a[2] < b[2], so Jack receives  1 point.

Lula's comparison score is 1, and Jack's comparison score is 1. 

Thus, we return the array [1, 1].

**Sample Input 1**

``[17, 28, 30]``

``[99, 16, 8]``

**Sample Output 1**

``[2, 1]``


**Explanation 1**

Comparing the *0th* elements,  *17 < 99* so Jack receives a point.

Comparing the  *1st* and  *2nd* elements, *28 > 16* and  *30 > 8* so Lula receives two points.

The return array is [2, 1].

## Solution and Explanation
*There is rarely one way to solve a problem and this is simply one solution.  There are probably many solutions better than this and a few that are worse.  *

The task is to write a function, ```compareTriplets()``` that accepts two arrays as an argument (Lula and Jack's individual sitcom-rating triplets) and returns an array of their respective comparision points.  Long story short, compare the two arrays, awarding a point to the person whose rating is higher for each category.  Then return the "score."  

```
function compareTriplets(a, b) {
  // Compare the triplets
	
  // Return the score
}
```

I know I'll need to eventually return an array of the comparison points, so my first step is to declare a variable ``score`` and assign it an inital value.

```
function compareTriplets(a, b) {
   let score = [0,0]
	 
}
```

I also know what the function needs to return.

```
function compareTriplets(a, b) {
   let score = [0,0]
   
   // compare the two arrays

   return score

}
```

The comparison itself is fairly straightforward - higher rating in each category (each *index*) gets a point, equal ratings do nothing.  Iterating through the arrays using a for loop, I compare each index.  If the two integers are not equal, I award a point to the correct score index. Returning the score array after the loop completes.

```
function compareTriplets(a, b) {
    let score = [0,0]
    for (let i=0; i < a.length; i++) {
        if (a[i] !== b[i]){
            a[i] > b[i] ? score[0] += 1 : score[1] += 1
        }
    }
    return score
}
```

At this point I have working solution.  I can move onto something else or take the time to re-examine my solution, looking for alternate approaches or potential improvements.  This is putting in the work.





