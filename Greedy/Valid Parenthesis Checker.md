
[678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)

Given a string `s` containing only three types of characters: `'('`, `')'` and `'*'`, return `true` _if_ `s` _is **valid**_.

The following rules define a **valid** string:

- Any left parenthesis `'('` must have a corresponding right parenthesis `')'`.
- Any right parenthesis `')'` must have a corresponding left parenthesis `'('`.
- Left parenthesis `'('` must go before the corresponding right parenthesis `')'`.
- `'*'` could be treated as a single right parenthesis `')'` or a single left parenthesis `'('` or an empty string `""`.

**Example 1:**

**Input:** s = "()"
**Output:** true

**Example 2:**

**Input:** s = "(*)"
**Output:** true
>[!Intuition]
>Do not fully get it

```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        leftmin,leftmax = 0,0

        for ch in s:
            if ch=='(':
                leftmin+=1
                leftmax+=1
            elif ch==')':
                leftmin-=1
                leftmax-=1 
            else:
                leftmax,leftmin = leftmax+1,leftmin-1

            if leftmax<0:
                return False
                
            leftmin = max(leftmin,0)
        
        return leftmin==0

```