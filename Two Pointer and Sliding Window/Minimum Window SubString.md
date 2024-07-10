


[76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window**_ **_substring_** _of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window_. If there is no such substring, return _the empty string_ `""`.

The testcases will be generated such that the answer is **unique**.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"
**Output:** "BANC"
**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

>[!Intuition]
>The main intuition is observing that the substring in it will have the either more or equal frequency for the characters in target string

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        
        first = {}
        # Frequency for the target string
        for char in t:
            first[char] = first.get(char,0)+1

        # Iterating over the sliding window and checking if the window characters
        # frequencies are greater than or equal to the target string character frequency 
        window = {}
        i = 0
        j = 0
        ans = ""
        for i in range(0,len(s)):
            window[s[i]] = window.get(s[i],0)+1
            if self.matches(window,first):
                while j<len(s) and self.matches(window,first):
                    # This if statement was the main confusion point
                    # Putting it over here ensures that the sliding window
                    # removes unneeded prefix elements for the substrings
                    # and the smallest answer is picked
                    if ans == "" or len(ans)>(i-j+1):
                        ans = s[j:i+1]
                    window[s[j]]-=1
                    j+=1
                
        return ans

        # Checking for window match with the target
    def matches(self,window,first):
        for i in first.keys():
            if (window.get(i) is None ) or first[i]>window[i]:
                return False
        return True
```