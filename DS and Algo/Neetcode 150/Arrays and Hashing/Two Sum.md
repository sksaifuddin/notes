## Leetcode number

1
## Link

https://leetcode.com/problems/two-sum
## Problem description:

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

**Example 1:**

**Input:** nums = [2,7,11,15], target = 9
**Output:** [0,1]
**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

**Example 2:**

**Input:** nums = [3,2,4], target = 6
**Output:** [1,2]

**Example 3:**

**Input:** nums = [3,3], target = 6
**Output:** [0,1]

**Constraints:**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **Only one valid answer exists.**

## Thought to myself

I have solved this problem before and every time I try  to do this problem with two pointers, which is so fundamentally wrong. My mind associates two sum with two pointers. We have to practice to come up with clever solutions. Need to improve logical building.
## solution 1: Brute force

The most simplest solution is to take one value and look for another number which could sum up to the target value. This will require us to use two for loops. 

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int n = nums.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[]{}; // No solution found
    }
}
```
source: https://leetcode.com/problems/two-sum/solutions/3619262/3-method-s-c-java-python-beginner-friendly/

## Solution 2: Using Hash table

A much better solution is to use a HashMap. The main thing to understand here is that we need to find the complement of the current number. Consider the formula:

complement = target - current_number

if the target = 4 and current_number = 2, then we have look for 4-2 = 2 in the array. Its just an clever and simple way to solve this. Once we figure out  this logic then problem is just soring key as number and its index as the value in a hash table and then iterating through the hash table and checking if the complement is present. 

You'll probably get a noob thought that: "why don't we just search the array instead of storing the number". Try to iterate with one example. because the value becomes negative when the target is smaller than the current_number, so the numbers needs to be in correct order.

``` java
class Solution {
    public int[] twoSum(int[] nums, int target) {
       Map<Integer, Integer> map = new HashMap<Integer, Integer>();

       for(int i=0; i<nums.length; i++) {
           int complement = target - nums[i];
           if(map.containsKey(complement)) {
               return new int[]{i, map.get(complement)};
           } else {
               map.put(nums[i], i);
           }
       }
       return new int[]{};
    }
}
```
