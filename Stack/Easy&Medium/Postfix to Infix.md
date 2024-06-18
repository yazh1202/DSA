
**Very similar to prefix to infix except we need to reverse the order of operands due to the right to left association**

[Problem Link](https://www.codingninjas.com/studio/problems/postfix-to-infix_8382386?leftPanelTabValue=SUBMISSION)
```python
def postToInfix(postfix: str) -> str:
    
    stack = []

    for c in postfix:
        if (c<='z' and c>='a') or (c<='Z' and c>='A'):
            stack.append(c)
        else :
            a = stack.pop()
            b = stack.pop()
            exp = "("+b+c+a+")"
            stack.append(exp)


    return stack[0]
```