# 计算具有一个可变字符的子字符串的出现次数

> 原文:[https://www . geeksforgeeks . org/count-出现次数-带有一个可变字符的子字符串/](https://www.geeksforgeeks.org/count-occurrences-of-a-sub-string-with-one-variable-character/)

给定两个字符串 **a** 和 **b** ，以及一个整数 **k** ，该整数是 **b** 中的索引，在该索引处该字符可以被更改为任何其他字符，任务是检查 **b** 是否是 **a** 中的子字符串，并在替换**b【k】**后打印出 **b** 在 **a** 中总共出现了多少次

**示例:**

> **输入:** a =“极客”，b =“ee”，k = 1
> **输出:** 1
> 将 b[1]替换为‘k’，并且“ek”是“极客”
> 中的子串“ee”也是“极客”
> 中的子串因此总计数为 2
> 
> **输入:**a =“dogdog”，b =“DOP”，k = 2
> **输出:** 2
> 将 b[2]替换为‘g’”，“dog”是“dog dog”中出现两次的子串。

**方法:**通过遍历所有小写字母并将 **k <sup>th</sup>** 即 **b** 中的**b【k】**字符替换为当前字符，列出字符串 **b** 的所有可能版本。
然后计算新字符串 **b** 在原字符串 **a** 中的出现次数，并将其存储在变量计数中。使用完所有小写字符后，打印**计数**。

下面是上述方法的实现:

```
# Python3 implementation of the approach
import string

# Function to return the count of occurrences
def countOccurrence(a, b, k):    

    # Generate all possible substrings to
    # be searched 
    x = []
    for i in range(26):
        x.append(b[0:k] + string.ascii_lowercase[i] + b[k + 1:])

    # Now search every substring 'a' and
    # increment count   
    count = 0
    for var in x:
        if var in a:
            count += a.count(var)

    return count

# Driver code
a, b = "geeks", "ee"
k = 1
print(countOccurrence(a, b, k))
```

**Output:**

```
2

```