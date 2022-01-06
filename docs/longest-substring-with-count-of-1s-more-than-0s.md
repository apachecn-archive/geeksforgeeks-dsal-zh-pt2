# 计数为 1s 大于 0s 的最长子串

> 原文:[https://www . geeksforgeeks . org/最长子串计数为 1 大于 0/](https://www.geeksforgeeks.org/longest-substring-with-count-of-1s-more-than-0s/)

给定一个二进制字符串，找出包含 1 个大于 0 个的最长子字符串。
**示例:**

```
Input : 1010
Output : 3
Substring 101 has 1 occurring more number of times than 0.

Input : 101100
Output : 5
Substring 10110 has 1 occurring more number of times than 0.
```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

一个简单的**解决方案是逐一考虑所有子串，并检查该子串的计数是否大于 0。如果计数大于其长度与迄今为止找到的最大长度子串的比较。这个解决方案的时间复杂度是 O(n^2).
一个有效的**解决方案是使用哈希。这个想法是找到迄今为止遍历的字符串的总和。如果当前字符为“1”，则结果加 1，否则减 1。现在问题简化为寻找总和大于零的最大子阵列。为了找到总和大于零的最大子阵列，我们检查总和的值。如果和大于零，那么和大于零的最大子阵列是 arr[0..我】。如果总和小于零，则求子阵 arr[j+1]的大小..I ),其中 j 是子阵列 arr[0..j]是 sum -1 和 j < i，并将该尺寸与目前发现最大子阵列尺寸进行比较。为了找到索引 j，存储 arr[0..j]在哈希表中为所有 0 < = j < = i .可能存在给定值的总和重复的可能性。在这种情况下，只存储第一个索引，因为需要获得最大子阵列的长度，并且该索引是从第一个索引出现时获得的。
以下是上述方法的实施:**** 

## ****C++****

```
**// CPP program to find largest substring
// having count of 1s more than count
// count of 0s.
#include <bits/stdc++.h>
using namespace std;

// Function to find longest substring
// having count of 1s more than count
// of 0s.
int findLongestSub(string bin)
{
    int n = bin.length(), i;

    // To store sum.
    int sum = 0;

    // To store first occurrence of each
    // sum value.
    unordered_map<int, int> prevSum;

    // To store maximum length.
    int maxlen = 0;

    // To store current substring length.
    int currlen;

    for (i = 0; i < n; i++) {

        // Add 1 if current character is 1
        // else subtract 1.
        if (bin[i] == '1')
            sum++;
        else
            sum--;

        // If sum is positive, then maximum
        // length substring is bin[0..i]
        if (sum > 0) {
            maxlen = i + 1;
        }

        // If sum is negative, then maximum
        // length substring is bin[j+1..i], where
        // sum of substring bin[0..j] is sum-1.
        else if (sum <= 0) {
            if (prevSum.find(sum - 1) != prevSum.end()) {
                currlen = i - prevSum[sum - 1];
                maxlen = max(maxlen, currlen);
            }
        }

        // Make entry for this sum value in hash
        // table if this value is not present.
        if (prevSum.find(sum) == prevSum.end())
            prevSum[sum] = i;
    }

    return maxlen;
}

// Driver code
int main()
{
    string bin = "1010";
    cout << findLongestSub(bin);
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to find largest substring
// having count of 1s more than count
// count of 0s.
import java.util.HashMap;

class GFG
{

    // Function to find longest substring
    // having count of 1s more than count
    // of 0s.
    static int findLongestSub(String bin)
    {
        int n = bin.length(), i;

        // To store sum.
        int sum = 0;

        // To store first occurrence of each
        // sum value.
        HashMap<Integer,
                Integer> prevSum = new HashMap<>();

        // To store maximum length.
        int maxlen = 0;

        // To store current substring length.
        int currlen;
        for (i = 0; i < n; i++)
        {

            // Add 1 if current character is 1
            // else subtract 1.
            if (bin.charAt(i) == '1')
                sum++;
            else
                sum--;

            // If sum is positive, then maximum
            // length substring is bin[0..i]
            if (sum > 0)
            {
                maxlen = i + 1;
            }

            // If sum is negative, then maximum
            // length substring is bin[j+1..i], where
            // sum of substring bin[0..j] is sum-1.
            else if (sum <= 0)

            {
                if (prevSum.containsKey(sum - 1))
                {
                    currlen = i - (prevSum.get(sum - 1) == null ? 1 :
                                   prevSum.get(sum - 1));
                    maxlen = Math.max(maxlen, currlen);
                }
            }

            // Make entry for this sum value in hash
            // table if this value is not present.
            if (!prevSum.containsKey(sum))
                prevSum.put(sum, i);
        }
        return maxlen;
    }

    // Driver code
    public static void main(String[] args)
    {
        String bin = "1010";
        System.out.println(findLongestSub(bin));
    }
}

// This code is contributed by
// sanjeev2552**
```

## ****蟒蛇 3****

```
**# Python 3 program to find largest substring
# having count of 1s more than count
# count of 0s.

# Function to find longest substring
# having count of 1s more than count
# of 0s.
def findLongestSub(bin1):
    n = len(bin1)

    # To store sum.
    sum = 0

    # To store first occurrence of each
    # sum value.
    prevSum = {i:0 for i in range(n)}

    # To store maximum length.
    maxlen = 0

    # To store current substring length.
    for i in range(n):

        # Add 1 if current character is 1
        # else subtract 1.
        if (bin1[i] == '1'):
            sum += 1
        else:
            sum -= 1

        # If sum is positive, then maximum
        # length substring is bin1[0..i]
        if (sum > 0):
            maxlen = i + 1

        # If sum is negative, then maximum
        # length substring is bin1[j+1..i], where
        # sum of substring bin1[0..j] is sum-1.
        elif (sum <= 0):
            if ((sum - 1) in prevSum):
                currlen = i - prevSum[sum - 1]
                maxlen = max(maxlen, currlen)

        # Make entry for this sum value in hash
        # table if this value is not present.
        if ((sum) not in prevSum):
            prevSum[sum] = i

    return maxlen

# Driver code
if __name__ == '__main__':
    bin1 = "1010"
    print(findLongestSub(bin1))

# This code is contributed by
# Surendra_Gangwar**
```

## ****C#****

```
**// C# program to find largest substring
// having count of 1s more than count
// count of 0s.
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find longest substring
    // having count of 1s more than count
    // of 0s.
    static int findLongestSub(String bin)
    {
        int n = bin.Length, i;

        // To store sum.
        int sum = 0;

        // To store first occurrence of each
        // sum value.
        Dictionary<int,
                   int> prevSum = new Dictionary<int,
                                                 int>();

        // To store maximum length.
        int maxlen = 0;

        // To store current substring length.
        int currlen;
        for (i = 0; i < n; i++)
        {

            // Add 1 if current character is 1
            // else subtract 1.
            if (bin[i] == '1')
                sum++;
            else
                sum--;

            // If sum is positive, then maximum
            // length substring is bin[0..i]
            if (sum > 0)
            {
                maxlen = i + 1;
            }

            // If sum is negative, then maximum
            // length substring is bin[j+1..i], where
            // sum of substring bin[0..j] is sum-1.
            else if (sum <= 0)

            {
                if (prevSum.ContainsKey(sum - 1))
                {
                    currlen = i - (prevSum[sum - 1] == 0 ? 1 :
                                   prevSum[sum - 1]);
                    maxlen = Math.Max(maxlen, currlen);
                }
            }

            // Make entry for this sum value in hash
            // table if this value is not present.
            if (!prevSum.ContainsKey(sum))
                prevSum.Add(sum, i);
        }
        return maxlen;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String bin = "1010";
        Console.WriteLine(findLongestSub(bin));
    }
}

// This code is contributed by 29AjayKumar**
```

## ****java 描述语言****

```
**<script>
// Javascript program to find largest substring
// having count of 1s more than count
// count of 0s.

// Function to find longest substring
    // having count of 1s more than count
    // of 0s.
function findLongestSub(bin)
{
    let n = bin.length, i;

        // To store sum.
        let sum = 0;

        // To store first occurrence of each
        // sum value.
        let prevSum = new Map();

        // To store maximum length.
        let maxlen = 0;

        // To store current substring length.
        let currlen;
        for (i = 0; i < n; i++)
        {

            // Add 1 if current character is 1
            // else subtract 1.
            if (bin[i] == '1')
                sum++;
            else
                sum--;

            // If sum is positive, then maximum
            // length substring is bin[0..i]
            if (sum > 0)
            {
                maxlen = i + 1;
            }

            // If sum is negative, then maximum
            // length substring is bin[j+1..i], where
            // sum of substring bin[0..j] is sum-1.
            else if (sum <= 0)

            {
                if (prevSum.has(sum - 1))
                {
                    currlen = i - (prevSum.get(sum - 1) == null ? 1 :
                                   prevSum.get(sum - 1));
                    maxlen = Math.max(maxlen, currlen);
                }
            }

            // Make entry for this sum value in hash
            // table if this value is not present.
            if (!prevSum.has(sum))
                prevSum.set(sum, i);
        }
        return maxlen;
}

// Driver code
let bin = "1010";
document.write(findLongestSub(bin));

// This code is contributed by rag2127
</script>**
```

******输出:****** 

```
**3**
```

******时间复杂度:**O(n)
T3】辅助空间: O(n)****