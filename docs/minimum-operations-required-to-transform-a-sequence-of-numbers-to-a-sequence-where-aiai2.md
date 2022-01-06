# 将一系列数字转换为一个序列所需的最小运算，其中 a[i]=a[i+2]

> 原文:[https://www . geeksforgeeks . org/将数字序列转换为序列所需的最小操作 aiai2/](https://www.geeksforgeeks.org/minimum-operations-required-to-transform-a-sequence-of-numbers-to-a-sequence-where-aiai2/)

给定偶数长度为“n”的整数序列，任务是找到转换序列所需的最小操作数，以遵循规则 a[i]=a[i+2]，其中“I”是索引。
这里的操作是用任意元素替换序列的任意元素。

**示例:**

```
Input : n=4 ; Array : 3, 1, 3, 2
Output : 1
If we change the last element to '1' then, 
the sequence will become 3, 1, 3, 1 (satisfying the condition)
So, only 1 replacement is required.

Input : n=6 ; Array : 105 119 105 119 105 119
Output : 0
As the sequence is already in the required state.
So, no replacement of elements is required. 
```

**方法:**如我们所见，指数 0，2，…，n-2 是独立连接的，而 1，3，5，…，n 是独立连接的，并且必须具有相同的值。所以，

*   我们必须通过将数字及其出现频率存储在一张地图中来找到序列(偶数和奇数)中出现次数最多的数字。
*   那么该序列中的每隔一个数字都必须被相同序列中出现次数最多的数字替换。
*   最后，上一步的替换计数将是答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum replacements
int minReplace(int a[], int n)
{
    int i;

    // Map to store the frequency of
    // the numbers at the even indices
    map<int, int> te;

    // Map to store the frequency of
    // the numbers at the odd indices
    map<int, int> to;

    for (i = 0; i < n; i++)
    {

        // Checking if the index
        // is odd or even
        if (i % 2 == 0)

            // If the number is already present then,
            // just increase the occurrence by 1
            te[a[i]]++;
        else

            // If the number is already present then,
            // just increase the occurrence by 1
            to[a[i]]++;
    }

    // To store the character with
    // maximum frequency in even indices.
    int me = -1;

    // To store the character with
    // maximum frequency in odd indices.
    int mo = -1;

    // To store the frequency of the
    // maximum occurring number in even indices.
    int ce = -1;

    // To store the frequency of the
    // maximum occurring number in odd indices.
    int co = -1;

    // Iterating over Map of even indices to
    // get the maximum occurring number.
    for (auto it : te)
    {
        if (it.second > ce)
        {
            ce = it.second;
            me = it.first;
        }
    }

    // Iterating over Map of odd indices to
    // get the maximum occurring number.
    for (auto it : to)
    {
        if (it.second > co)
        {
            co = it.second;
            mo = it.first;
        }
    }

    // To store the final answer
    int res = 0;

    for (i = 0; i < n; i++)
    {
        if (i % 2 == 0)
        {

            // If the index is even but
            // a[i] != me
            // then a[i] needs to be replaced
            if (a[i] != me) res++;
        }

        else
        {

            // If the index is odd but
            // a[i] != mo
            // then a[i] needs to be replaced
            if (a[i] != mo) res++;
        }
    }
    return res;
}

// Driver Code
int main()
{
    int n = 4;
    int a[] = {3, 1, 3, 2};
    cout << minReplace(a, n) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;
class GFG {

    // Function to return the minimum replacements
    public static int minReplace(int a[], int n)
    {
        int i;

        // Map to store the frequency of
        // the numbers at the even indices
        HashMap<Integer, Integer> te = new HashMap<>();

        // Map to store the frequency of
        // the numbers at the odd indices
        HashMap<Integer, Integer> to = new HashMap<>();

        for (i = 0; i < n; i++) {

            // Checking if the index
            // is odd or even
            if (i % 2 == 0) {

                // If the number is already present then,
                // just increase the occurrence by 1
                if (te.containsKey(a[i]))
                    te.put(a[i], te.get(a[i]) + 1);
                else
                    te.put(a[i], 1);
            }
            else {

                // If the number is already present then,
                // just increase the occurrence by 1
                if (to.containsKey(a[i]))
                    to.put(a[i], to.get(a[i]) + 1);
                else
                    to.put(a[i], 1);
            }
        }

        // To store the character with
        // maximum frequency in even indices.
        int me = -1;

        // To store the character with
        // maximum frequency in odd indices.
        int mo = -1;

        // To store the frequency of the
        // maximum occurring number in even indices.
        int ce = -1;

        // To store the frequency of the
        // maximum occurring number in odd indices.
        int co = -1;

        // Iterating over Map of even indices to
        // get the maximum occurring number.
        for (Integer It : te.keySet()) {
            if (te.get(It) > ce) {
                ce = te.get(It);
                me = It;
            }
        }

        // Iterating over Map of odd indices to
        // get the maximum occurring number.
        for (Integer It : to.keySet()) {
            if (to.get(It) > co) {
                co = to.get(It);
                mo = It;
            }
        }

        // To store the final answer
        int res = 0;

        for (i = 0; i < n; i++) {
            if (i % 2 == 0) {

                // If the index is even but
                // a[i] != me
                // then a[i] needs to be replaced
                if (a[i] != me)
                    res++;
            }
            else {

                // If the index is odd but
                // a[i] != mo
                // then a[i] needs to be replaced
                if (a[i] != mo)
                    res++;
            }
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n;
        n = 4;
        int a[] = { 3, 1, 3, 2 };
        System.out.println(minReplace(a, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum replacements
def minReplace(a: list, n) -> int:

    # Map to store the frequency of
    # the numbers at the even indices
    te = dict()

    # Map to store the frequency of
    # the numbers at the odd indices
    to = dict()

    for i in range(n):

        # Checking if the index
        # is odd or even
        if i % 2 == 0:

            # If the number is already present then,
            # just increase the occurrence by 1
            if a[i] not in te:
                te[a[i]] = 1
            else:
                te[a[i]] += 1
        else:

            # If the number is already present then,
            # just increase the occurrence by 1
            if a[i] not in to:
                to[a[i]] = 1
            else:
                to[a[i]] += 1

    # To store the character with
    # maximum frequency in even indices.
    me = -1

    # To store the character with
    # maximum frequency in odd indices.
    mo = -1

    # To store the frequency of the
    # maximum occurring number in even indices.
    ce = -1

    # To store the frequency of the
    # maximum occurring number in odd indices.
    co = -1

    # Iterating over Map of even indices to
    # get the maximum occurring number.
    for it in te:
        if te[it] > ce:
            ce = te[it]
            me = it

    # Iterating over Map of odd indices to
    # get the maximum occurring number.
    for it in to:
        if to[it] > co:
            co = to[it]
            mo = it

    # To store the final answer
    res = 0

    for i in range(n):
        if i % 2 == 0:

            # If the index is even but
            # a[i] != me
            # then a[i] needs to be replaced
            if a[i] != me:
                res += 1
        else:

            # If the index is odd but
            # a[i] != mo
            # then a[i] needs to be replaced
            if a[i] != mo:
                res += 1

    return res

# Driver Code
if __name__ == "__main__":
    n = 4
    a = [3, 1, 3, 2]
    print(minReplace(a, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the minimum replacements
    public static int minReplace(int []a, int n)
    {
        int i;

        // Map to store the frequency of
        // the numbers at the even indices
        Dictionary<int,
                   int> te = new Dictionary<int,
                                            int>();

        // Map to store the frequency of
        // the numbers at the odd indices
        Dictionary<int,
                   int> to = new Dictionary<int,
                                            int>();

        for (i = 0; i < n; i++)
        {

            // Checking if the index
            // is odd or even
            if (i % 2 == 0)
            {

                // If the number is already present then,
                // just increase the occurrence by 1
                if (te.ContainsKey(a[i]))
                    te[a[i]] = te[a[i]] + 1;
                else
                    te.Add(a[i], 1);
            }
            else
            {

                // If the number is already present then,
                // just increase the occurrence by 1
                if (to.ContainsKey(a[i]))
                    to[a[i]] = te[a[i]] + 1;
                else
                    to.Add(a[i], 1);
            }
        }

        // To store the character with
        // maximum frequency in even indices.
        int me = -1;

        // To store the character with
        // maximum frequency in odd indices.
        int mo = -1;

        // To store the frequency of the
        // maximum occurring number in even indices.
        int ce = -1;

        // To store the frequency of the
        // maximum occurring number in odd indices.
        int co = -1;

        // Iterating over Map of even indices to
        // get the maximum occurring number.
        foreach (int It in te.Keys)
        {
            if (te[It] > ce)
            {
                ce = te[It];
                me = It;
            }
        }

        // Iterating over Map of odd indices to
        // get the maximum occurring number.
        foreach (int It in to.Keys)
        {
            if (to[It] > co)
            {
                co = to[It];
                mo = It;
            }
        }

        // To store the final answer
        int res = 0;

        for (i = 0; i < n; i++)
        {
            if (i % 2 == 0)
            {

                // If the index is even but
                // a[i] != me
                // then a[i] needs to be replaced
                if (a[i] != me)
                    res++;
            }
            else
            {

                // If the index is odd but
                // a[i] != mo
                // then a[i] needs to be replaced
                if (a[i] != mo)
                    res++;
            }
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n;
        n = 4;
        int []a = { 3, 1, 3, 2 };
        Console.WriteLine(minReplace(a, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum replacements
function minReplace(a, n)
{
    var i;

    // Map to store the frequency of
    // the numbers at the even indices
    var te = new Map();

    // Map to store the frequency of
    // the numbers at the odd indices
    var to = new Map();

    for (i = 0; i < n; i++)
    {

        // Checking if the index
        // is odd or even
        if (i % 2 == 0)

            // If the number is already present then,
            // just increase the occurrence by 1
            if(te.has(a[i]))
                te.set(a[i], te.get(a[i])+1)
            else
                te.set(a[i],1)
        else

            // If the number is already present then,
            // just increase the occurrence by 1
            if(to.has(a[i]))
                to.set(a[i], to.get(a[i])+1)
            else
                to.set(a[i],1)
    }

    // To store the character with
    // maximum frequency in even indices.
    var me = -1;

    // To store the character with
    // maximum frequency in odd indices.
    var mo = -1;

    // To store the frequency of the
    // maximum occurring number in even indices.
    var ce = -1;

    // To store the frequency of the
    // maximum occurring number in odd indices.
    var co = -1;

    // Iterating over Map of even indices to
    // get the maximum occurring number.
    te.forEach((value, key) => {

        if (value > ce)
        {
            ce = value;
            me = key;
        }
    });

    // Iterating over Map of odd indices to
    // get the maximum occurring number.
    to.forEach((value, key) => {

        if (value > co)
        {
            co = value;
            mo = key;
        }
    });

    // To store the final answer
    var res = 0;

    for (i = 0; i < n; i++)
    {
        if (i % 2 == 0)
        {

            // If the index is even but
            // a[i] != me
            // then a[i] needs to be replaced
            if (a[i] != me)
              res++;
        }

        else
        {

            // If the index is odd but
            // a[i] != mo
            // then a[i] needs to be replaced
            if (a[i] != mo)
              res++;
        }
    }
    return res;
}

// Driver Code
var n = 4;
var a = [3, 1, 3, 2];
document.write( minReplace(a, n) );

</script>
```

**Output:** 

```
1
```