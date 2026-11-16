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


