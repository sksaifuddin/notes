
## Problem statement

Given two strings `s` and `t`, return `true` _if_ `t` _is an anagram of_ `s`_, and_ `false` _otherwise_.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "anagram", t = "nagaram"
**Output:** true

**Example 2:**

**Input:** s = "rat", t = "car"
**Output:** false

**Constraints:**

- `1 <= s.length, t.length <= 5 * 104`
- `s` and `t` consist of lowercase English letters.

## My solution:

```java
class Solution {

    public boolean isAnagram(String s, String t) {

        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        char[] sCharArray = s.toCharArray();
        char[] tCharArray = t.toCharArray();

        if(sCharArray.length != tCharArray.length) {
            return false;
        }

        for(int i=0; i<sCharArray.length; i++) {

            // if there is already char present in hashmap then increase its value by one

            // else insert the char with value as 1

            char key = sCharArray[i];
            if(map.containsKey(key)) {
                 map.put(key, map.get(key) + 1);
            } else {
                map.put(key, 1);
            }
        }

        for(int i=0; i<tCharArray.length; i++) {
            char key = tCharArray[i];
            if(map.containsKey(key)) {
                 map.put(key, map.get(key) - 1);
            }
        }

        for ( Integer value: map.values()) {
            if ( value > 0) {
                return false;
            }
        }
        return true;
    }

}
```

This the first solution which came to my mind. Since in an anagram we need equal number of characters I had to count the number of characters in s and then check if all t has all those characters. First thing which came to my mind was to create two HashMap but to improve the space complexity I created one HashMap and then checked if each character of t is present in s HashMap. If there is character then decrease its value by 1. At last if we have all the elements in HashMap as 0 then its an anagram else return false.

### time complexity = O(s+t)

## Solution 2:

I read about another solution online. We just sort both the strings and then compare them. If they are equal then they are anagram otherwise not. This is was more simple solution. But downside is the sorting. Best sorting complexity can be O(nlogn). But this solution can be considered too.