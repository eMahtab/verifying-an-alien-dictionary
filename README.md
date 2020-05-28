# Verifying an alien dictionary
## https://leetcode.com/problems/verifying-an-alien-dictionary

In an alien language, surprisingly they also use english lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.

Given a sequence of words written in the alien language, and the order of the alphabet, return true if and only if the given words are sorted lexicographicaly in this alien language.

```
Example 1:

Input: words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
Output: true
Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.

Example 2:

Input: words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
Output: false
Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.

Example 3:

Input: words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
Output: false
Explanation: The first three characters "app" match, and the second string is shorter (in size.) 
According to lexicographical rules "apple" > "app", because 'l' > '∅', where '∅' is defined as 
the blank character which is less than any other character (More info).
``` 

**Constraints:**
1. 1 <= words.length <= 100
2. 1 <= words[i].length <= 20
3. order.length == 26
4. All characters in words[i] and order are English lowercase letters.

# Implementation :

```java
class Solution {
    public boolean isAlienSorted(String[] words, String order) {
        int[] ordering = new int[26];
        for(int i = 0; i < order.length(); i++) {
            ordering[order.charAt(i) - 'a'] = i;
        }
        
        for(int i = 0; i < words.length - 1; i++) {
            String first = words[i];
            String second = words[i+1];
            // Check If second word is a prefix of first word, If thats the case its not a valid alien dictionary
            // eg. ["apple", "app"]
            if(first.startsWith(second) && first.length() > second.length())
                return false;
            int minLength = Math.min(first.length(), second.length());
            for(int index = 0; index < minLength; index++) {
                // Find the first different character
                if(first.charAt(index) != second.charAt(index)) {
                    if(ordering[first.charAt(index) - 'a'] > ordering[second.charAt(index) - 'a'])
                        return false;
                    break;
                }
            }
        }
        return true;
    }
}
```

## Important :
1. Prefix check is required to handle e.g. ["apple", "app"] these type of inputs. 
2. Don't compare after the first different character, so break; is must
3. Don't forget array's have `length` property while strings have `length()` method

# References :
https://leetcode.com/articles/verifying-an-alien-dictionary
