## Problem: 2243. [Calculate Digit Sum of a string](https://leetcode.com/problems/calculate-digit-sum-of-a-string/?envType=daily-question&envId=2026-11-16)

## Solution - 1: First Try

```python
class Solution:
    def digitSum(self, s: str, k: int) -> str:
        if len(s) <= k:
            return s

        new_s = ""
        for i in range(0, len(s)):
            if i %k != 0:
                # print(f"Test: {i}, {k}, {i % k}")
                continue
            tmp = s[i:i+k]
            total = 0
            for x in range(k):
                if x>= len(tmp):
                    new_s = f"{new_s}{total}"
                    break
                total += int(tmp[x])
            if x< len(tmp):
                new_s = f"{new_s}{total}"
            # print(new_s, i)
        return self.digitSum(new_s, k)
```
----

## Solution 2: Improvement - Changing to while loop
For loop is unnecessary for this scenario. so changing it to while loop, which is the correct for this scenario

```python
class Solution:
    def digitSum(self, s: str, k: int) -> str:
        if len(s) <= k:
            return s

        new_s = ""
        i, n = 0, len(s)
        while i < len(s):
            tmp = s[i:i+k]
            total = 0
            for x in range(k):
                if x>= len(tmp):
                    new_s = f"{new_s}{total}"
                    break
                total += int(tmp[x])
            if x< len(tmp):
                new_s = f"{new_s}{total}"
            # print(new_s, i)
            i += k
        return self.digitSum(new_s, k)
```
----

## Solution 3: Improvement - Remove not needed condition in the loop

When the tmp variable itself giving proper count, why we need to count again and break and all, so improved it

```python
class Solution:
    def digitSum(self, s: str, k: int) -> str:
        if len(s) <= k:
            return s

        new_s = ""
        i, n = 0, len(s)
        while i < len(s):
            tmp = s[i:i+k]
            total = 0
            for x in range(len(tmp)):
                total += int(tmp[x])
            new_s = f"{new_s}{total}"
            i += k
        return self.digitSum(new_s, k)
```

----

## Solution 4: Improvement - String construction

Python string are immutable, which means every time I try to concat it's trying to recreate entire memory and assign it, behalf of that, we can just keep as list and then construct the final string

```python
class Solution:
    def digitSum(self, s: str, k: int) -> str:
        if len(s) <= k:
            return s

        new_s = []
        i, n = 0, len(s)
        while i < len(s):
            tmp = s[i:i+k]
            total = 0
            for x in range(len(tmp)):
                total += int(tmp[x])
            new_s.append(str(total))
            i += k
        return self.digitSum("".join(new_s), k)

```
## Solution 5: Improvement - Remove unnecessary variable

When we can able to loop in single line, we can reduce unnecessary local variables

```python
class Solution:
    def digitSum(self, s: str, k: int) -> str:
        if len(s) <= k:
            return s

        new_s = []
        i = 0
        while i < len(s):
            new_s.append(str(sum([int(x) for x in s[i:i+k]])))
            i += k
        return self.digitSum("".join(new_s), k)
```


