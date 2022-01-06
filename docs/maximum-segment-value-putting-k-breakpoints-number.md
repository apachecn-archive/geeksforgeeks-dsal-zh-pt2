# 将 k 个断点放入一个数字后的最大分段值

> 原文:[https://www . geesforgeks . org/maximum-segment-value-put-k-断点-number/](https://www.geeksforgeeks.org/maximum-segment-value-putting-k-breakpoints-number/)

给定一个大的数字作为字符串 s 和一个整数 k，它表示断点的数量，我们必须在数字 k <=字符串长度中输入。任务是在精确放置 k 个断点后找到最大段值。

**示例:**

```
Input : s = "8754", k = 2
Output : Maximum number = 87
Explanation : We need to two breakpoints. After
putting the breakpoints, we get following options
8 75 4
87 5 4
The maximum segment value is 87.

Input : s = "999", k = 1 
Output : Maximum Segment Value = 99
Explanation : We need to one breakpoint. After
putting the breakpoint, we either get 99,9 or
9,99.

```

一个重要的观察是，最大值总是长度为“字符串长度-k”，这是任何段的最大值。考虑到这个事实，问题变得像[滑动窗口问题](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)意味着我们需要找到所有大小(字符串长度–k)的子字符串的最大值。

## C++

```
// CPP program to find the maximum segment
// value after putting k breaks.
#include <bits/stdc++.h>
using namespace std;

// Function to Find Maximum Number
int findMaxSegment(string &s, int k) {

  // Maximum segment length
  int seg_len = s.length() - k;

  // Find value of first segment of seg_len
  int res = 0;
  for (int i=0; i<seg_len; i++)
     res = res * 10 + (s[i] - '0');

  // Find value of remaining segments using sliding
  // window
  int seg_len_pow = pow(10, seg_len-1);
  int curr_val = res;
  for (int i = 1; i <= (s.length() - seg_len); i++) {

    // To find value of current segment, first remove
    // leading digit from previous value    
    curr_val = curr_val - (s[i-1]- '0')*seg_len_pow;

    // Then add trailing digit
    curr_val = curr_val*10 + (s[i+seg_len-1]- '0');

    res = max(res, curr_val);
  }
  return res;
}

// Driver's Function
int main() {
  string s = "8754";
  int k = 2;
  cout << "Maximum number = " << findMaxSegment(s, k);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum segment
// value after putting k breaks.
class GFG {

    // Function to Find Maximum Number
    static int findMaxSegment(String s, int k) {

        // Maximum segment length
        int seg_len = s.length() - k;

        // Find value of first segment of seg_len
        int res = 0;

        for (int i = 0; i < seg_len; i++)
            res = res * 10 + (s.charAt(i) - '0');

        // Find value of remaining segments using 
        // sliding window
        int seg_len_pow = (int)Math.pow(10,
                                    seg_len - 1);
        int curr_val = res;

        for (int i = 1; 
             i <= (s.length() - seg_len); i++) {

            // To find value of current segment, 
            // first remove leading digit from 
            // previous value
            curr_val = curr_val - 
            (s.charAt(i - 1) - '0') * seg_len_pow;

            // Then add trailing digit
            curr_val = curr_val * 10 + 
               (s.charAt(i + seg_len - 1) - '0');

            res = Math.max(res, curr_val);
        }

        return res;
    }

    // Driver code
    public static void main(String[] args) {

        String s = "8754";
        int k = 2;

        System.out.print("Maximum number = "
                        + findMaxSegment(s, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find the maximum segment 
# value after putting k breaks. 

# Function to Find Maximum Number 
def findMaxSegment(s, k):

    # Maximum segment length 
    seg_len = len(s) - k 

    # Find value of first segment of seg_len 
    res = 0
    for i in range(seg_len):
        res = res * 10 + (ord(s[i]) - ord('0')) 

    # Find value of remaining segments
    # using sliding window 
    seg_len_pow = pow(10, seg_len - 1) 
    curr_val = res 
    for i in range(1, len(s) - seg_len):

        # To find value of current segment, 
        # first remove leading digit from 
        # previous value     
        curr_val = curr_val - (ord(s[i - 1])- 
                               ord('0')) * seg_len_pow 

        # Then add trailing digit 
        curr_val = (curr_val * 10 + 
                   (ord(s[i + seg_len - 1]) - ord('0'))) 

        res = max(res, curr_val)
    return res

# Driver Code
if __name__ == '__main__':
    s = "8754"
    k = 2
    print("Maximum number = ",
         findMaxSegment(s, k))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find the maximum segment
// value after putting k breaks.
using System;

class GFG {

    // Function to Find Maximum Number
    static int findMaxSegment(string s, int k) {

        // Maximum segment length
        int seg_len = s.Length - k;

        // Find value of first segment of seg_len
        int res = 0;

        for (int i = 0; i < seg_len; i++)
            res = res * 10 + (s[i] - '0');

        // Find value of remaining segments using 
        // sliding window
        int seg_len_pow = (int)Math.Pow(10,
                                    seg_len - 1);
        int curr_val = res;

        for (int i = 1; 
            i <= (s.Length- seg_len); i++) {

            // To find value of current segment, 
            // first remove leading digit from 
            // previous value
            curr_val = curr_val - 
            (s[i - 1] - '0') * seg_len_pow;

            // Then add trailing digit
            curr_val = curr_val * 10 + 
            (s[i + seg_len - 1] - '0');

            res = Math.Max(res, curr_val);
        }

        return res;
    }

    // Driver code
    public static void Main() {

        String s = "8754";
        int k = 2;

        Console.WriteLine("Maximum number = "
                        + findMaxSegment(s, k));
    }
}

// This code is contributed by vt_m.
```

**Output:**

```
Maximum number = 87

```