This is the notes for my leetcode daily problems

## Day 5 - Jan 5 - [2381. Shifting Letters II](https://leetcode.com/problems/shifting-letters-ii/)

### Brute force solution - No
#### Thoughts
Although I came up with logic for brute force but I was not able to do the shifting of characters forward and backward. 

### Optimized Solution

#### Thoughts
The optimized solution uses **line sweep algorithm**. The algorithm looked simple but I still lack understanding of the problem. Need to learn about it. The character shifting was still tough for me.

Refer link: https://youtu.be/p06jf-QUYQE?si=bIsbOLatZcdZAZVN

## Day 6 - Jan 6 - [1769. Minimum Number of Operations to Move All Balls to Each Box](https://leetcode.com/problems/minimum-number-of-operations-to-move-all-balls-to-each-box/)

### Brute force solution - Yes

#### Thoughts
This was first time I came up with the solution on my own. I first calculated the number of total boxes and then by iterating through each box I store all the boxes with 1 ball in an arraylist and  by  | boxesWithball.get(j) - currentbox| we get how many steps we should take to add all the ball to that box.

Although its time complexity is O(n^2), the answer was still accepted. We need to optimize the code.

### Optimized solution:

The optimized solution is also pretty simple: We can first calculate the left ball and then the right balls for every box. and then for every box we keep adding all the first and last ball. I did not code this solution since I am busy with applying for jobs but I need to come back later to code the optimized solution. 
