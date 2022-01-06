# 使用 Map 函数

在 Python 中二进制字符串中连续 1 的最大长度

> 原文:[https://www . geesforgeks . org/最大长度-连续-1s-二进制-字符串-python-使用-map-function/](https://www.geeksforgeeks.org/maximum-length-consecutive-1s-binary-string-python-using-map-function/)

给我们一个包含 1 和 0 的二进制字符串。找出其中连续 1 的最大长度。

**例:**

```
Input : str = '11000111101010111'
Output : 4
```

对于这个问题，我们有一个现有的解决方案，请参考链接中二进制数组的最大连续 1(或 0)。我们可以在 Python 的单行代码中解决这个问题。方法很简单，

1.  Use the [split ()](https://www.geeksforgeeks.org/how-to-split-a-string-in-cc-python-and-java/) method of strings to separate all substrings of consecutive 1s separated by zeros.
2.  Print a disassembly string with a maximum length of 1.

## Python

```
# Function to find Maximum length of consecutive 1's in a binary string

def maxConsecutive1(input):
     # input.split('0') --> splits all sub-strings of consecutive 1's
     # separated by 0's, output will be like ['11','1111','1','1','111']
     # map(len,input.split('0'))  --> map function maps len function on each
     # sub-string of consecutive 1's
     # max() returns maximum element from a list
     print max(map(len,input.split('0')))

# Driver program
if __name__ == "__main__":
    input = '11000111101010111'
    maxConsecutive1(input)
```

**输出:**

```
4
```