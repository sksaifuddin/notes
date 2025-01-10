While solving problem I always come across some common techniques, this is the list of all the techniques I come across and need them to solve more Leetcode problems
## Creating frequency array

Creating a frequency array of string. That is, counting number of character of the string and presented in the form of array.

```java
 public int[] getFreq(String word) {
        int freq[] = new int[26];
        for(int i = 0; i<word.length(); i++) {
            freq[word.charAt(i) - 'a']++;
        }

        return freq;
    }
```
