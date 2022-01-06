# 数组的字典上最大排列，使得 a[i] = a[i-1] + gcd(a[i-1]，a[i-2])

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大排列-这样-ai-ai-1-gcdai-1-ai-2/](https://www.geeksforgeeks.org/lexicographically-largest-permutation-of-the-array-such-that-ai-ai-1-gcdai-1-ai-2/)

给定一个大小为 **N** ( **N > 2** 的数组**[]**)。任务是找到数组的字典式最大排列，使得**arr[I]= arr[I–1]+gcd(arr[I–1]，arr[I–2])**。如果无法找到这样的排列，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {4，6，2，5，3}
> **输出:** 2 3 4 5 6
> 4 = 3 + gcd(2，3)
> 5 = 4 + gcd(3，4)
> 6 = 5 + gcd(4，5)
> **输入:** arr[] = {1，6，8}
> **输出:** -1

**方法:**如果您正在考虑一个解决方案，该解决方案将涉及[排序](https://www.geeksforgeeks.org/sorting-algorithms/)数组，然后检查 gcd 条件是否成立。你说的有一部分是对的，数字必须是递增的，但有一种情况除外，那就是在排列的开始可能会出现一个数字。例如，arr[] = {2，4，6，8，8}在这种情况下，8 可以放在数组的开头，以获得排列{8，2，4，6，8}。
**角箱:**

*   频率大于 1 的元素不能超过两个。
*   如果数组中有两个零，唯一可能的排列就是所有的 0

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find elements of vector
void Print(vector<int>& ans)
{
    for (auto i : ans)
        cout << i << " ";
}

// Function to find the lexicographically largest
// permutation that satisfies the given condition
void Permutation(int a[], int n)
{
    int flag = 0, pos;

    // To store the required ans
    vector<int> ans;

    // Sort the array
    sort(a, a + n);

    for (int i = 2; i < n; i++) {

        // If need to make arranagement
        if (a[i] != a[i - 1] + __gcd(a[i - 1], a[i - 2])) {
            flag = 1;
            pos = i;
            break;
        }
    }

    // If possible then check for lexographically
    // larger permutation (if any possible)
    if (flag == 0) {

        // If larger arrangement is possible
        if (a[1] == a[0] + __gcd(a[0], a[n - 1])) {
            ans.push_back(a[n - 1]);
            for (int i = 0; i < n - 1; i++)
                ans.push_back(a[i]);

            Print(ans);
            return;
        }

        // If no other arrangement is possible
        else {
            for (int i = 0; i < n; i++)
                ans.push_back(a[i]);

            Print(ans);
            return;
        }
    }

    // Need to re-arrange the array
    else {

        // If possible, place at first position
        if (a[1] == a[0] + __gcd(a[pos], a[0])) {
            flag = 0;
            for (int i = n - 1; i > pos + 2; i--) {

                // If even after one arrangement its impossible
                // to get the required array
                if (a[i] != a[i - 1] + __gcd(a[i - 1], a[i - 2])) {
                    flag = 1;
                    break;
                }
            }

            if (flag == 0 and pos < n - 1) {

                // If it is not possible to get
                // the required array
                if (a[pos + 1]
                    != a[pos - 1] + __gcd(a[pos - 1], a[pos - 2]))
                    flag = 1;
            }

            if (flag == 0 and pos < n - 2) {

                // If it is not possible to get
                // the required array
                if (a[pos + 2]
                    != a[pos + 1] + __gcd(a[pos - 1], a[pos + 1]))
                    flag = 1;
            }

            // If it is possible to get the answer
            if (flag == 0) {
                ans.push_back(a[pos]);
                for (int i = 0; i < n; i++)
                    if (i != pos)
                        ans.push_back(a[i]);

                Print(ans);
                return;
            }
        }
    }

    ans.push_back(-1);
    Print(ans);
}

// Driver code
int main()
{
    int a[] = { 4, 6, 2, 8, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    Permutation(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find elements of vector
static void Print(Vector<Integer> ans)
{
    for (Integer i : ans)
        System.out.print(i + " ");
}

// Function to find the lexicographically largest
// permutation that satisfies the given condition
static void Permutation(int a[], int n)
{
    int flag = 0, pos = 0;

    // To store the required ans
    Vector<Integer> ans = new Vector<Integer>();

    // Sort the array
    Arrays.sort(a);

    for (int i = 2; i < n; i++)
    {

        // If need to make arranagement
        if (a[i] != a[i - 1] + __gcd(a[i - 1],
                                     a[i - 2]))
        {
            flag = 1;
            pos = i;
            break;
        }
    }

    // If possible then check for lexographically
    // larger permutation (if any possible)
    if (flag == 0)
    {

        // If larger arrangement is possible
        if (a[1] == a[0] + __gcd(a[0],
                                 a[n - 1]))
        {
            ans.add(a[n - 1]);
            for (int i = 0; i < n - 1; i++)
                ans.add(a[i]);

            Print(ans);
            return;
        }

        // If no other arrangement is possible
        else
        {
            for (int i = 0; i < n; i++)
                ans.add(a[i]);

            Print(ans);
            return;
        }
    }

    // Need to re-arrange the array
    else
    {

        // If possible, place at first position
        if (a[1] == a[0] + __gcd(a[pos], a[0]))
        {
            flag = 0;
            for (int i = n - 1; i > pos + 2; i--)
            {

                // If even after one arrangement
                // its impossible to get
                // the required array
                if (a[i] != a[i - 1] + __gcd(a[i - 1],
                                             a[i - 2]))
                {
                    flag = 1;
                    break;
                }
            }

            if (flag == 0 & pos < n - 1)
            {

                // If it is not possible to get
                // the required array
                if (a[pos + 1]
                    != a[pos - 1] + __gcd(a[pos - 1],
                                          a[pos - 2]))
                    flag = 1;
            }

            if (flag == 0 & pos < n - 2)
            {

                // If it is not possible to get
                // the required array
                if (a[pos + 2]
                    != a[pos + 1] + __gcd(a[pos - 1],
                                          a[pos + 1]))
                    flag = 1;
            }

            // If it is possible to get the answer
            if (flag == 0)
            {
                ans.add(a[pos]);
                for (int i = 0; i < n; i++)
                    if (i != pos)
                        ans.add(a[i]);

                Print(ans);
                return;
            }
        }
    }

    ans.add(-1);
    Print(ans);
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 4, 6, 2, 8, 8 };
    int n = a.length;

    Permutation(a, n);
    }
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import gcd

# Function to find elements of vector
def Print(ans):
    for i in range(len(ans)):
        print(ans[i], end = " ")

# Function to find the lexicographically
# largest permutation that satisfies
# the given condition
def Permutation(a, n):
    flag = 0

    # To store the required ans
    ans = []

    # Sort the array
    a.sort(reverse = False)

    for i in range(2, n, 1):

        # If need to make arranagement
        if (a[i] != a[i - 1] +
        gcd(a[i - 1], a[i - 2])):
            flag = 1
            pos = i
            break

    # If possible then check for
    # lexographically larger
    # permutation (if any possible)
    if (flag == 0):

        # If larger arrangement is possible
        if (a[1] == a[0] +
        gcd(a[0], a[n - 1])):
            ans.append(a[n - 1])
            for i in range(n - 1):
                ans.append(a[i])

            Print(ans)
            return

        # If no other arrangement is possible
        else:
            for i in range(n):
                ans.append(a[i])

            Print(ans)
            return

    # Need to re-arrange the array
    else:

        # If possible, place at first position
        if (a[1] == a[0] +
        gcd(a[pos], a[0])):
            flag = 0
            i = n - 1
            while(i > pos + 2):

                # If even after one arrangement its
                # impossible to get the required array
                if (a[i] != a[i - 1] +
                gcd(a[i - 1], a[i - 2])):
                    flag = 1
                    break

                i -= 1

            if (flag == 0 and pos < n - 1):

                # If it is not possible to get
                # the required array
                if (a[pos + 1] != a[pos - 1] +
                gcd(a[pos - 1], a[pos - 2])):
                    flag = 1

            if (flag == 0 and pos < n - 2):

                # If it is not possible to get
                # the required array
                if (a[pos + 2] != a[pos + 1] +
                gcd(a[pos - 1], a[pos + 1])):
                    flag = 1

            # If it is possible to get the answer
            if (flag == 0):
                ans.append(a[pos])
                for i in range(n):
                    if (i != pos):
                        ans.append(a[i])

                Print(ans)
                return

    ans.append(-1)
    Print(ans)

# Driver code
if __name__ == '__main__':
    a = [4, 6, 2, 8, 8]
    n = len(a)

    Permutation(a, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find elements of vector
static void Print(List<int> ans)
{
    foreach (int i in ans)
        Console.Write(i + " ");
}

// Function to find the lexicographically largest
// permutation that satisfies the given condition
static void Permutation(int []a, int n)
{
    int flag = 0, pos = 0;

    // To store the required ans
    List<int> ans = new List<int>();

    // Sort the array
    Array.Sort(a);

    for (int i = 2; i < n; i++)
    {

        // If need to make arranagement
        if (a[i] != a[i - 1] + __gcd(a[i - 1],
                                     a[i - 2]))
        {
            flag = 1;
            pos = i;
            break;
        }
    }

    // If possible then check for lexographically
    // larger permutation (if any possible)
    if (flag == 0)
    {

        // If larger arrangement is possible
        if (a[1] == a[0] + __gcd(a[0],
                                 a[n - 1]))
        {
            ans.Add(a[n - 1]);
            for (int i = 0; i < n - 1; i++)
                ans.Add(a[i]);

            Print(ans);
            return;
        }

        // If no other arrangement is possible
        else
        {
            for (int i = 0; i < n; i++)
                ans.Add(a[i]);

            Print(ans);
            return;
        }
    }

    // Need to re-arrange the array
    else
    {

        // If possible, place at first position
        if (a[1] == a[0] + __gcd(a[pos], a[0]))
        {
            flag = 0;
            for (int i = n - 1; i > pos + 2; i--)
            {

                // If even after one arrangement
                // its impossible to get
                // the required array
                if (a[i] != a[i - 1] + __gcd(a[i - 1],
                                             a[i - 2]))
                {
                    flag = 1;
                    break;
                }
            }

            if (flag == 0 & pos < n - 1)
            {

                // If it is not possible to get
                // the required array
                if (a[pos + 1]
                    != a[pos - 1] + __gcd(a[pos - 1],
                                          a[pos - 2]))
                    flag = 1;
            }

            if (flag == 0 & pos < n - 2)
            {

                // If it is not possible to get
                // the required array
                if (a[pos + 2]
                    != a[pos + 1] + __gcd(a[pos - 1],
                                          a[pos + 1]))
                    flag = 1;
            }

            // If it is possible to get the answer
            if (flag == 0)
            {
                ans.Add(a[pos]);
                for (int i = 0; i < n; i++)
                    if (i != pos)
                        ans.Add(a[i]);

                Print(ans);
                return;
            }
        }
    }

    ans.Add(-1);
    Print(ans);
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 4, 6, 2, 8, 8 };
    int n = a.Length;

    Permutation(a, n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find elements of vector
function Print(ans) {
    for (let i of ans)
        document.write(i + " ");
}

// Function to find the lexicographically largest
// permutation that satisfies the given condition
function Permutation(a, n) {
    let flag = 0, pos = 0;

    // To store the required ans
    let ans = new Array();

    // Sort the array
    a.sort((a, b) => a - b);

    for (let i = 2; i < n; i++) {

        // If need to make arranagement
        if (a[i] != a[i - 1] + __gcd(a[i - 1],
            a[i - 2])) {
            flag = 1;
            pos = i;
            break;
        }
    }

    // If possible then check for lexographically
    // larger permutation (if any possible)
    if (flag == 0) {

        // If larger arrangement is possible
        if (a[1] == a[0] + __gcd(a[0],
            a[n - 1])) {
            ans.push(a[n - 1]);
            for (let i = 0; i < n - 1; i++)
                ans.push(a[i]);

            Print(ans);
            return;
        }

        // If no other arrangement is possible
        else {
            for (let i = 0; i < n; i++)
                ans.push(a[i]);

            Print(ans);
            return;
        }
    }

    // Need to re-arrange the array
    else {

        // If possible, place at first position
        if (a[1] == a[0] + __gcd(a[pos], a[0])) {
            flag = 0;
            for (let i = n - 1; i > pos + 2; i--) {

                // If even after one arrangement
                // its impossible to get
                // the required array
                if (a[i] != a[i - 1] + __gcd(a[i - 1],
                    a[i - 2])) {
                    flag = 1;
                    break;
                }
            }

            if (flag == 0 & pos < n - 1) {

                // If it is not possible to get
                // the required array
                if (a[pos + 1]
                    != a[pos - 1] + __gcd(a[pos - 1],
                        a[pos - 2]))
                    flag = 1;
            }

            if (flag == 0 & pos < n - 2) {

                // If it is not possible to get
                // the required array
                if (a[pos + 2]
                    != a[pos + 1] + __gcd(a[pos - 1],
                        a[pos + 1]))
                    flag = 1;
            }

            // If it is possible to get the answer
            if (flag == 0) {
                ans.push(a[pos]);
                for (let i = 0; i < n; i++)
                    if (i != pos)
                        ans.push(a[i]);

                Print(ans);
                return;
            }
        }
    }

    ans.push(-1);
    Print(ans);
}

function __gcd(a, b) {
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver code

let a = [4, 6, 2, 8, 8];
let n = a.length;

Permutation(a, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
8 2 4 6 8
```

**时间复杂度:** O(NlogN)