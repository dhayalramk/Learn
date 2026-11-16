# Problem: 258 [Add Digits](https://leetcode.com/problems/add-digits/description/)

# Solution 1: First try

Just loop till the digit becomes 1 digit using while loop

```python
class Solution:
    def addDigits(self, num: int) -> int:
        while num > 9:
            num = sum(int(n) for n in str(num))
        return num
```
----
## Solution 2: Math using 9

```python

class Solution:
    def addDigits(self, num: int) -> int:
        return 0 if num == 0 else 9 if num % 9 == 0 else num % 9
```

----
## Solution 3: Improve code quality

```
class Solution:
    def addDigits(self, num: int) -> int:
        if num == 0:
            return 0
        return (num -1) %9 + 1
```
