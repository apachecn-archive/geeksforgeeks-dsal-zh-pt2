# 使给定阵列成为接入点所需的最小更改次数

> 原文:[https://www . geesforgeks . org/最小更改次数-制作给定阵列所需的更改次数-ap/](https://www.geeksforgeeks.org/minimum-number-of-changes-required-to-make-the-given-array-an-ap/)

给定一个由![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")个整数和一个数字![d ](img/3aaf2b05c24884036f21542f10ccb3e9.png "Rendered by QuickLaTeX.com")组成的数组 arr[]。您可以将数组的任何元素更改为整数。任务是找到使给定数组成为具有共同区别![d ](img/3aaf2b05c24884036f21542f10ccb3e9.png "Rendered by QuickLaTeX.com")的算术级数所需的最小变化数。

**示例**:

```
Input : N = 4, d = 2
        arr[] = {1, 2, 4, 6}
Output : 1
Explanation: change a[0]=0\. 
So, new sequence is 0, 2, 4, 6 which is an AP.

Input : N = 5, d = 1
        arr[] = {1, 3, 3, 4, 6}
Output : 2
Explanation: change a[1]=2 and a[4]=5\. 
So, new sequence is 1, 2, 3, 4, 5 which is an AP.

```

解决这个问题的想法是观察 AP 中第 n 项的公式是:

```
an = a0 + (n-1)*d

Where, a0 is the first term
and d is the common difference.
```

我们被赋予了![d   ](img/d2136f01cc70510f9dde0fa6df89b2a5.png "Rendered by QuickLaTeX.com")和**a<sub>n</sub>T4】的值。因此，我们将为 I 的所有值找到 a <sub>0</sub> 的值，其中 1 < =i < =n，并为 I 的不同值存储 a <sub>0</sub> 的出现频率。现在，需要更改的元素的最小数量是:**

```
n - (maximum frequency of a0)
```

其中**a<sub>0</sub>**的最大频率表示数组中第一项的值相同的元素总数。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum number
// of changes required to make the given
// array an AP with common difference d
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of changes required to make the given
// array an AP with common difference d
int minimumChanges(int arr[], int n, int d)
{
    int maxFreq = INT_MIN;

    // Map to store frequency of a0
    unordered_map<int, int> freq;

    // storing frequency of a0 for all possible
    // values of a[i] and finding the maximum
    // frequency
    for (int i = 0; i < n; ++i) {
        int a0 = arr[i] - (i)*d;

        // increment frequency by 1
        if (freq.find(a0) != freq.end()) {
            freq[a0]++;
        }
        else
            freq.insert(make_pair(a0, 1));

        // finds count of most frequent number
        if (freq[a0] > maxFreq)
            maxFreq = freq[a0];
    }

    // minimum number of elements needed to
    // be changed is: n - (maximum frequency of a0)
    return (n - maxFreq);
}

// Driver Program
int main()
{
    int n = 5, d = 1;

    int arr[] = { 1, 3, 3, 4, 6 };

    cout << minimumChanges(arr, n, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum number of changes
// required to make the given
// array an AP with common
// difference d
import java.util.*;

class GFG {

    // Function to find the minimum
    // number of changes required
    // to make the given array an
    // AP with common difference d
    static int minimumChanges(int arr[],
                              int n, int d)
    {
        int maxFreq = -1;

        // Map to store frequency of a0
        HashMap<Integer,
                Integer>
            freq = new HashMap<Integer,
                               Integer>();

        // storing frequency of a0 for
        // all possible values of a[i]
        // and finding the maximum
        // frequency
        for (int i = 0; i < n; ++i) {
            int a0 = arr[i] - (i)*d;

            // increment frequency by 1
            if (freq.containsKey(a0)) {
                freq.put(a0, freq.get(a0) + 1);
            }
            else
                freq.put(a0, 1);

            // finds count of most
            // frequent number
            if (freq.get(a0) > maxFreq)
                maxFreq = freq.get(a0);
        }

        // minimum number of elements
        // needed to be changed is:
        // n - (maximum frequency of a0)
        return (n - maxFreq);
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5, d = 1;

        int arr[] = { 1, 3, 3, 4, 6 };

        System.out.println(minimumChanges(arr, n, d));
    }
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# number of changes required to make
# the given array an AP with common
# difference d

# Function to find the minimum number
# of changes required to make the given
# array an AP with common difference d
def minimumChanges(arr, n, d):
    maxFreq = -2147483648

    # dictionary to store
    # frequency of a0
    freq = {}

    # storing frequency of a0 for
    # all possible values of a[i]
    # and finding the maximum'
    # frequency
    for i in range(n):
        a0 = arr[i] - i * d

        # increment frequency by 1
        if a0 in freq:
            freq[a0] += 1
        else:
            freq[a0] = 1

        # finds count of most
        # frequent number
        if freq[a0] > maxFreq:
            maxFreq = freq[a0]

    # minimum number of elements
    # needed to be changed is:
    # n - (maximum frequency of a0)
    return (n-maxFreq)

# Driver Code

# number of terms in ap
n = 5

# difference in AP
d = 1
arr = [1, 3, 3, 4, 6 ]
ans = minimumChanges(arr, n, d)
print(ans)

# This code is contributed
# by sahil shelangia
```

## C#

```
// C# program to find the
// minimum number of changes
// required to make the given
// array an AP with common
// difference d
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the minimum
    // number of changes required
    // to make the given array an
    // AP with common difference d
    static int minimumChanges(int[] arr,
                              int n, int d)
    {
        int maxFreq = -1;

        // Map to store frequency of a0
        Dictionary<int, int> freq = new Dictionary<int, int>();

        // storing frequency of a0 for
        // all possible values of a[i]
        // and finding the maximum
        // frequency
        for (int i = 0; i < n; ++i) {
            int a0 = arr[i] - (i)*d;

            // increment frequency by 1
            if (freq.ContainsKey(a0)) {
                var obj = freq[a0];
                freq.Remove(a0);
                freq.Add(a0, obj + 1);
            }
            else
                freq.Add(a0, 1);

            // finds count of most
            // frequent number
            if (freq[a0] > maxFreq)
                maxFreq = freq[a0];
        }

        // minimum number of elements
        // needed to be changed is:
        // n - (maximum frequency of a0)
        return (n - maxFreq);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 5, d = 1;

        int[] arr = { 1, 3, 3, 4, 6 };

        Console.WriteLine(minimumChanges(arr, n, d));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum number
// of changes required to make the given
// array an AP with common difference d

// Function to find the minimum number
// of changes required to make the given
// array an AP with common difference d
function minimumChanges(&$arr, $n, $d)
{
    $maxFreq = PHP_INT_MIN;

    // array to store frequency of a0
    $freq = array();

    // storing frequency of a0 for
    // all possible values of a[i]
    // and finding the maximum
    // frequency
    for ($i = 0; $i < $n; ++$i)
    {
        $a0 = $arr[$i] - ($i) * $d;

        // increment frequency by 1
        if(array_search($a0, $freq))
        {
            $freq[$a0]++;
        }
        else
            $freq[$a0] = 1;

        // finds count of most
        // frequent number
        if ($freq[$a0] > $maxFreq)
            $maxFreq = $freq[$a0];
    }

    // minimum number of elements
    // needed to be changed is:
    // $n - (maximum frequency of a0)
    return ($n - $maxFreq);
}

// Driver Code
$n = 5;
$d = 1;

$arr = array( 1, 3, 3, 4, 6 );

echo minimumChanges($arr, $n, $d);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to find the
// minimum number of changes
// required to make the given
// array an AP with common
// difference d

    // Function to find the minimum
    // number of changes required
    // to make the given array an
    // AP with common difference d
    function minimumChanges(arr,n,d)
    {
        let maxFreq = -1;

        // Map to store frequency of a0
        let freq = new Map();

        // storing frequency of a0 for
        // all possible values of a[i]
        // and finding the maximum
        // frequency
        for (let i = 0; i < n; ++i) {
            let a0 = arr[i] - (i)*d;

            // increment frequency by 1
            if (freq.has(a0)) {
                freq.set(a0, freq.get(a0) + 1);
            }
            else
                freq.set(a0, 1);

            // finds count of most
            // frequent number
            if (freq.get(a0) > maxFreq)
                maxFreq = freq.get(a0);
        }

        // minimum number of elements
        // needed to be changed is:
        // n - (maximum frequency of a0)
        return (n - maxFreq);
    }

      // Driver Code
    let n = 5, d = 1;
    let arr=[ 1, 3, 3, 4, 6];
    document.write(minimumChanges(arr, n, d));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)