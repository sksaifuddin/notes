
## Problem description

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Example 1:**

**Input:** nums = [1,2,3,1]
**Output:** true

**Example 2:**

**Input:** nums = [1,2,3,4]
**Output:** false

**Example 3:**

**Input:** nums = [1,1,1,3,3,4,3,2,4,2]
**Output:** true

**Constraints:**

- `1 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`

## My Solution:

```java
	class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for(int i=0; i < nums.length-1; i++) {
            if(nums[i] == nums[i+1]) {
                return true;
            }
        }
        return false;
    }
}
```

## Notes

I was able to come up with the logic in the first attempt and was intuitive for me. We first sort the array so that all the common elements come together. Once they are together then I just have to compare each element with its next element. If they are same then you found duplicate or move to the next element until you reach the last element.

time complexity: O(nlogn) - since sorting is involved.

There are other solutions with O(n) complexity using HashMap and HashSet, I will try to other problems with Hash, since it is too simple problem.

 [[Neetcode 150]]