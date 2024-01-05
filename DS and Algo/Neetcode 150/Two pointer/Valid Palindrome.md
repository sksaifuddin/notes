## Leetcode number

125
## Link

https://leetcode.com/problems/valid-palindrome
## Problem description

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` _if it is a **palindrome**, or_ `false` _otherwise_.

**Example 1:**

**Input:** s = "A man, a plan, a canal: Panama"
**Output:** true
**Explanation:** "amanaplanacanalpanama" is a palindrome.

**Example 2:**

**Input:** s = "race a car"
**Output:** false
**Explanation:** "raceacar" is not a palindrome.

**Example 3:**

**Input:** s = " "
**Output:** true
**Explanation:** s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

**Constraints:**

- `1 <= s.length <= 2 * 105`
- `s` consists only of printable ASCII characters.

## Solution

This code is an implementation of a solution to determine if a given string is a palindrome. A string is considered a palindrome if it reads the same forwards and backwards, ignoring spaces, punctuation, and letter casing.

The approach used in this solution is a two-pointer technique, where two pointers are maintained, one at the start of the string and the other at the end of the string. The two pointers move towards each other until they meet in the middle of the string.

At each iteration of the while loop, the characters pointed to by the start and last pointers are checked. If either of the characters is not a letter or digit (e.g., a space or punctuation), the pointer is moved one step to the right (for start) or one step to the left (for last) until a letter or digit is found.

If both characters are letters or digits, they are converted to lowercase and compared. If they are not equal, the function returns false, as the string is not a palindrome. If they are equal, both pointers are moved one step to the right and left, respectively.

The while loop continues until the start pointer is greater than the last pointer, indicating that all the characters have been checked and that the string is a palindrome. The function then returns true.

# Complexity

- Time complexity:  
    The time complexity of this solution is O(n), where n is the length of the string. This is because, in the worst case, all characters in the string need to be checked once, so the number of operations is proportional to the length of the string.
    
- Space complexity:  
    The space complexity of this solution is O(1), as no additional data structures are used, and only a constant amount of memory is required for the start and last pointers and a few variables.
source: https://leetcode.com/problems/valid-palindrome/solutions/3165353/beats-96-9-well-explained-code-in-java/

## Thoughts to myself

I was able to come up with the logic but struggled a bit with if statements and with java functions. Still need to practice more java. I need to get better at it to solve problems faster.

```java

class Solution {

    public boolean isPalindrome(String s) {

        char[] arr = s.toCharArray();

  

        int p1=0; int p2= arr.length-1;

  

        while(p1<p2) {

            if(!Character.isLetterOrDigit(arr[p1])) {

                p1++;

            } else if(!Character.isLetterOrDigit(arr[p2])) {

                p2--;

            } else {

                if(Character.toLowerCase(arr[p1]) != Character.toLowerCase(arr[p2])) {

                    return false;

                }

  

                p1++;

                p2--;

            }

        }

  

        return true;

    }

}
```

[[Neetcode 150]]