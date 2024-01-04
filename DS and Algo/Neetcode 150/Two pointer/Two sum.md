## Leetcode number

167
## Link

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
## Problem description

Given a **1-indexed** array of integers `numbers` that is already **_sorted in non-decreasing order_**, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return _the indices of the two numbers,_ `index1` _and_ `index2`_, **added by one** as an integer array_ `[index1, index2]` _of length 2._

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Your solution must use only constant extra space.

**Example 1:**

**Input:** numbers = [2,7,11,15], target = 9
**Output:** [1,2]
**Explanation:** The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

**Example 2:**

**Input:** numbers = [2,3,4], target = 6
**Output:** [1,3]
**Explanation:** The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

**Example 3:**

**Input:** numbers = [-1,0], target = -1
**Output:** [1,2]
**Explanation:** The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].

**Constraints:**

- `2 <= numbers.length <= 3 * 104`
- `-1000 <= numbers[i] <= 1000`
- `numbers` is sorted in **non-decreasing order**.
- `-1000 <= target <= 1000`
- The tests are generated such that there is **exactly one solution**.

## Solution

Finding two numbers in a sorted array is a classic two pointer technique problem. This is like the most known technique ever. We maintain two pointers and keep find sum for each iteration. If the sum is smaller than the target, that means we need greater number, which could be achieved by increasing the p1 pointer. If the target is greater then we need a smaller number, so we decrease the value of p2 pointer. Keep bringing them to the center until they coincide.

``` java

class Solution {

    public int[] twoSum(int[] numbers, int target) {

        int p1=0; int p2=numbers.length-1;

        while(p1<p2) {
            int sum = numbers[p1] + numbers[p2];
            if(sum == target) {
                return new int[]{++p1, ++p2};
            }

            if(sum < target) {
                p1++;
            } else {
                p2--;
            }
        }
        return new int[]{};
    }
}
```

[[Neetcode 150]]
