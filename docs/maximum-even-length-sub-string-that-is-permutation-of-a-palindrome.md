# 回文排列的最大偶数长度子串

> 原文:[https://www . geesforgeks . org/最大偶数长度子串即回文置换/](https://www.geeksforgeeks.org/maximum-even-length-sub-string-that-is-permutation-of-a-palindrome/)

给定一个字符串![str](img/18a4823b2e68e228257b5de182b8b4ec.png "Rendered by QuickLaTeX.com")，任务是找到![str](img/18a4823b2e68e228257b5de182b8b4ec.png "Rendered by QuickLaTeX.com")的子字符串中可以排列成[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)的最大长度(即它的排列中至少有一个是回文)。**注意**子串长度必须均匀。

**示例:**

> **输入:** str = "124565463"
> **输出:**6
> “456546”为有效子串
> 
> **输入:**str = " 122313 "
> T3】输出: 6

**方法:**使用两个变量:**开始**(包含)和**结束**(不包含)来跟踪给定字符串中正在考虑的当前子字符串的开始和结束索引。也可以使用名为**计数**的字典来记录一个字符在当前子字符串中出现的次数。现在，子字符串有两种可能的情况:

1.  如果子串的长度是奇数，那么在最终的解决方案中不能考虑它。
2.  如果子串的长度是偶数，那么只有当该子串中的每个字符出现偶数次时，这才是可能的解决方案，这可以使用字典**计数**来完成。我们检查每个字符是否出现偶数次。如果是，那么我们将其作为可能的解决方案之一。然后，我们通过在字符串中包含下一个字符来形成下一个子字符串，这可以通过简单地递增 **end** 来完成，并且递归地检查是否可以形成满足给定条件的更长的子字符串，并且返回所有可能解的最大值。

以下是上述方法的实现:

## C++

```
// C++ code to find the maximum length of 
// sub-string (of even length) which can be
// arranged into a Palindrome
#include <bits/stdc++.h>
using namespace std;

unordered_map<int, int> countt;

// function that returns true if the given
// sub-string can be arranged into a Palindrome
bool canBePalindrome(unordered_map<int, int> &countt) 
{
    for (auto key : countt)
    {
        if (key.second & 1) return false;
    }
    return true;
}

// This function returns the maximum length of
// the sub-string (of even length) which can be
// arranged into a Palindrome
int maxPal(string str,
           unordered_map<int, int> &countt,
           int start, int end)
{

    // If we reach end of the string
    if (end == str.length()) 
    {

        // if string is of even length
        if ((end - start) % 2 == 0)

            // if string can be arranged into a
            // palindrome
            if (canBePalindrome(countt)) return end - start;

        return 0;
    } 
    else 
    {

        // Even length sub-string
        if ((end - start) % 2 == 0) 
        {

            // Check if current sub-string can be
            // arranged into a palindrome
            if (canBePalindrome(countt))
            {
                countt[str[end]]++;
                return max(end - start, maxPal(str, countt, 
                                               start, end + 1));
            } 
            else
            {
                countt[str[end]]++;
                return maxPal(str, countt, start, end + 1);
            }
        }

        // Odd length sub-string
        else
        {
            countt[str[end]]++;
            unordered_map<int, int> c(countt.begin(), 
                                      countt.end());
            int length = maxPal(str, c, start, end + 1);

            countt[str[end]]--;
            countt[str[start]]--;
            return max(length, maxPal(str, countt, 
                                      start + 1, end));
        }
    }
}

// Driver code
int main(int argc, char const *argv[])
{
    string str = "124565463";
    int start = 0, end = 0;

    cout << maxPal(str, countt, start, end) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the maximum length of 
// sub-string (of even length) which can be 
// arranged into a Palindrome 
import java.io.*;
import java.util.*;

class GFG 
{

    static HashMap<Integer, Integer> count = new HashMap<>();

    // function that returns true if the given
    // sub-string can be arranged into a Palindrome
    static boolean canBePalindrome(HashMap<Integer, Integer> count)
    {
        for (HashMap.Entry<Integer, Integer> entry : count.entrySet())
            if ((entry.getValue() & 1) == 1)
                return false;
        return true;
    }

    // This function returns the maximum length of
    // the sub-string (of even length) which can be
    // arranged into a Palindrome
    static int maxPal(String str, int start, int end, 
                       HashMap<Integer, Integer> count)
    {

        // If we reach end of the string
        if (end == str.length())
        {

            // if string is of even length
            if ((end - start) % 2 == 0)

                // if string can be arranged into a
                // palindrome
                if (canBePalindrome(count))
                    return end - start;

            return 0;
        } 
        else
        {

            // Even length sub-string
            if ((end - start) % 2 == 0) 
            {

                // Check if current sub-string can be
                // arranged into a palindrome
                if (canBePalindrome(count))
                {
                    count.put((int) str.charAt(end),
                    count.get((int) str.charAt(end)) ==
                    null ? 1 : count.get((int) str.charAt(end)) + 1);
                    return Math.max(end - start, 
                            maxPal(str, start, end + 1, count));
                }
                else
                {
                    count.put((int) str.charAt(end),
                    count.get((int) str.charAt(end)) ==
                    null ? 1 : count.get((int) str.charAt(end)) + 1);
                    return maxPal(str, start, end + 1, count);
                }
            }

            // Odd length sub-string
            else
            {
                count.put((int) str.charAt(end),
                count.get((int) str.charAt(end)) == 
                null ? 1 : count.get((int) str.charAt(end)) + 1);
                HashMap<Integer, Integer> c = new HashMap<>(count);

                int length = maxPal(str, start, end + 1, c);

                count.put((int) str.charAt(end),
                count.get((int) str.charAt(end)) ==
                null ? -1 : count.get((int) str.charAt(end)) - 1);

                count.put((int) str.charAt(start),
                count.get((int) str.charAt(start)) ==
                null ? -1 : count.get((int) str.charAt(start)) - 1);

                return Math.max(length, maxPal(str, 
                            start + 1, end, count));
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "124565463";
        int start = 0, end = 0;
        System.out.println(maxPal(str, start, end, count));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 code to find the maximum length of sub-string 
# (of even length) which can be arranged into a Palindrome

from collections import defaultdict

# function that returns true if the given 
# sub-string can be arranged into a Palindrome
def canBePalindrome(count):    
    for key in count:
        if count[key] % 2 != 0:
            return False            
    return True

# This function returns the maximum length of 
# the sub-string (of even length) which can be 
# arranged into a Palindrome
def maxPal(string, count, start, end):

    # If we reach end of the string
    if end == len(string):

        # if string is of even length
        if (end-start) % 2 == 0:

            # if string can be arranged into a
            # palindrome
            if canBePalindrome(count) == True:
                return end-start

        return 0

    else:

        # Even length sub-string
        if (end-start) % 2 == 0:

            # Check if current sub-string can be 
            # arranged into a palindrome
            if canBePalindrome(count) == True:
                count[string[end]] += 1
                return max(end-start, maxPal(string, count, start, end + 1))

            else:
                count[string[end]] += 1
                return maxPal(string, count, start, end + 1)

        # Odd length sub-string  
        else:

            count[string[end]] += 1
            length = maxPal(string, count.copy(), start, end + 1)

            count[string[end]] -= 1
            count[string[start]] -= 1
            return max(length, maxPal(string, count, start + 1, end))

# Driver code
string = '124565463'
start, end = 0, 0
count = defaultdict(lambda : 0)

print(maxPal(string, count, start, end))
```

**Output:**

```
6

```