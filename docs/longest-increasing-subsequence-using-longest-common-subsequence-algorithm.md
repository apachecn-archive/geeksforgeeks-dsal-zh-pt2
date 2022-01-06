# 使用最长公共子序列算法的最长递增子序列

> 原文:[https://www . geesforgeks . org/最长递增子序列使用最长公共子序列算法/](https://www.geeksforgeeks.org/longest-increasing-subsequence-using-longest-common-subsequence-algorithm/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到并打印最长的递增子序列。
**例:**

> **输入:** arr[] = {12，34，1，5，40，80}
> **输出:** 4
> {12，34，40，80}和{1，5，40，80}是
> 最长的递增子序列。
> **输入:** arr[] = {10，22，9，33，21，50，41，60，80}
> **输出:** 6

先决条件: [LCS](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/) 、 [LIS](https://www.geeksforgeeks.org/construction-of-longest-increasing-subsequence-using-dynamic-programming/) 、
T5】方法:任何序列中最长的递增子序列是其自身排序序列的子序列。可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法来解决。该方法与经典的 [LCS](https://www.geeksforgeeks.org/longest-common-subsequence/) 问题相同，但是代替第二序列，给定序列以其排序形式再次被采用。
**注意:**数组应该有不同的元素，否则可能会给出错误的结果。例如，在{1，1，1}中，我们知道最长的递增子序列(a1 < a2 < … ak)的长度为 1，但是如果我们使用 LCS 方法在 LIS 中尝试这个例子，我们将得到 3(因为它找到了最长的公共子序列)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the size of the
// longest increasing subsequence
int LISusingLCS(vector<int>& seq)
{
    int n = seq.size();

    // Create an 2D array of integer
    // for tabulation
    vector<vector<int> > L(n + 1, vector<int>(n + 1));

    // Take the second sequence as the sorted
    // sequence of the given sequence
    vector<int> sortedseq(seq);

    sort(sortedseq.begin(), sortedseq.end());

    // Classical Dynamic Programming algorithm
    // for Longest Common Subsequence
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (seq[i - 1] == sortedseq[j - 1])
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }

    // Return the ans
    return L[n][n];
}

// Driver code
int main()
{

    vector<int> sequence{ 12, 34, 1, 5, 40, 80 };

    cout << LISusingLCS(sequence) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach
import java.util.*;

class GFG
{

// Function to return the size of the
// longest increasing subsequence
static int LISusingLCS(Vector<Integer> seq)
{
    int n = seq.size();

    // Create an 2D array of integer
    // for tabulation
    int L[][] = new int [n + 1][n + 1];

    // Take the second sequence as the sorted
    // sequence of the given sequence
    Vector<Integer> sortedseq = new Vector<Integer>(seq);

    Collections.sort(sortedseq);

    // Classical Dynamic Programming algorithm
    // for Longest Common Subsequence
    for (int i = 0; i <= n; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (seq.get(i - 1) == sortedseq.get(j - 1))
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = Math.max(L[i - 1][j],
                                   L[i][j - 1]);
        }
    }

    // Return the ans
    return L[n][n];
}

// Driver code
public static void main(String args[])
{
    Vector<Integer> sequence = new Vector<Integer>();
    sequence.add(12);
    sequence.add(34);
    sequence.add(1);
    sequence.add(5);
    sequence.add(40);
    sequence.add(80);

    System.out.println(LISusingLCS(sequence));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the size of the
# longest increasing subsequence
def LISusingLCS(seq):
    n = len(seq)

    # Create an 2D array of integer
    # for tabulation
    L = [[0 for i in range(n + 1)]
            for i in range(n + 1)]

    # Take the second sequence as the sorted
    # sequence of the given sequence
    sortedseq = sorted(seq)

    # Classical Dynamic Programming algorithm
    # for Longest Common Subsequence
    for i in range(n + 1):
        for j in range(n + 1):
            if (i == 0 or j == 0):
                L[i][j] = 0

            elif (seq[i - 1] == sortedseq[j - 1]):
                L[i][j] = L[i - 1][j - 1] + 1

            else:
                L[i][j] = max(L[i - 1][j],
                              L[i][j - 1])

    # Return the ans
    return L[n][n]

# Driver code
sequence = [12, 34, 1, 5, 40, 80]

print(LISusingLCS(sequence))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the size of the
// longest increasing subsequence
static int LISusingLCS(List<int> seq)
{
    int n = seq.Count;

    // Create an 2D array of integer
    // for tabulation
    int [,]L = new int [n + 1, n + 1];

    // Take the second sequence as the sorted
    // sequence of the given sequence
    List<int> sortedseq = new List<int>(seq);

    sortedseq.Sort();

    // Classical Dynamic Programming algorithm
    // for longest Common Subsequence
    for (int i = 0; i <= n; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i, j] = 0;

            else if (seq[i - 1] == sortedseq[j - 1])
                L[i, j] = L[i - 1, j - 1] + 1;

            else
                L[i,j] = Math.Max(L[i - 1, j],
                                L[i, j - 1]);
        }
    }

    // Return the ans
    return L[n, n];
}

// Driver code
public static void Main(String []args)
{
    List<int> sequence = new List<int>();
    sequence.Add(12);
    sequence.Add(34);
    sequence.Add(1);
    sequence.Add(5);
    sequence.Add(40);
    sequence.Add(80);

    Console.WriteLine(LISusingLCS(sequence));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
//Javascript implementation of above approach

// Function to return the size of the
// longest increasing subsequence
function LISusingLCS(seq)
{
    let n = seq.length;

    // Create an 2D array of integer
    // for tabulation
    let L = new Array(n + 1);
    for(let i = 0; i < (n + 1); i++)
    {
        L[i] = new Array(n + 1);
        for(let j = 0; j < (n + 1); j++)
        {
            L[i][j] = 0;
        }
    }

    // Take the second sequence as the sorted
    // sequence of the given sequence
    let sortedseq =[...seq];

    sortedseq.sort(function(a,b){return a-b;});
    // Classical Dynamic Programming algorithm
    // for Longest Common Subsequence
    for (let i = 0; i <= n; i++)
    {
        for (let j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (seq[i - 1] == sortedseq[j - 1])
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = Math.max(L[i - 1][j],
                                   L[i][j - 1]);
        }
    }

    // Return the ans
    return L[n][n];
}

// Driver code
let sequence = [12, 34, 1, 5, 40, 80];
document.write(LISusingLCS(sequence));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(n <sup>2</sup> )其中 n 是序列的长度
T5】辅助空间: O(n <sup>2</sup> )