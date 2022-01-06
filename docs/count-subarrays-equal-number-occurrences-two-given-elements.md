# 对两个给定元素出现次数相等的子阵列进行计数

> 原文:[https://www . geesforgeks . org/count-subarrays-等次数出现-两个给定元素/](https://www.geeksforgeeks.org/count-subarrays-equal-number-occurrences-two-given-elements/)

给定一个数组和两个整数，比如 x 和 y，求子数组的个数，其中 x 的出现次数等于 y 的出现次数。

**示例:**

```
Input : arr[] = {1, 2, 1},
        x = 1, y = 2 
Output : 2
The possible sub-arrays have same equal number 
of occurrences of x and y are:
1) {1, 2}, x and y have same occurrence(1).
2) {2, 1}, x and y have same occurrence(1).

Input : arr[] = {1, 2, 1},
        x = 4, y = 6
Output : 6
The possible sub-arrays have same equal number of 
occurrences of x and y are:
1) {1}, x and y have same occurrence(0).
2) {2}, x and y have same occurrence(0).
3) {1}, x and y have same occurrence(0).
1) {1, 2}, x and y have same occurrence(0).
2) {2, 1}, x and y have same occurrence(0).
3) {1, 2, 1}, x and y have same occurrence(0).

Input : arr[] = {1, 2, 1},
        x = 1, y = 1
Output : 6
The possible sub-arrays have same equal number 
of occurrences of x and y are:
1) {1}, x and y have same occurrence(1).
2) {2}, x and y have same occurrence(0).
3) {1}, x and y have same occurrence(1).
1) {1, 2}, x and y have same occurrence(1).
2) {2, 1}, x and y have same occurrence(1).
3) {1, 2, 1}, x and y have same occurrences (2).
```

**蛮力方法(时间复杂度–O(N<sup>2</sup>):**

我们可以简单地生成所有可能的子阵列，并检查每个子阵列中 x 的出现次数是否等于 y 的出现次数。

## C++

```
/* C++ program to count number of sub-arrays in which
   number of occurrence of x is equal to that of y
    using brute force */
#include <bits/stdc++.h>
using namespace std;

int sameOccurrence(int arr[], int n, int x, int y)
{
    int result = 0;

    // Check for each subarray for the required condition
    for (int i = 0; i <= n - 1; i++) {
        int ctX = 0,  ctY = 0;
        for (int j = i; j <= n - 1; j++) {
            if (arr[j] == x)
                ctX += 1;
            else if (arr[j] == y)
                ctY += 1;
            if (ctX == ctY)
                result += 1;           
        }
    }

    return (result);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 3, 4, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 2, y = 3;
    cout << sameOccurrence(arr, n, x, y);
    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to count number of sub-arrays in which
number of occurrence of x is equal to that of y
    using brute force */
import java.util.*;

class solution
{

static int sameOccurrence(int arr[], int n, int x, int y)
{
    int result = 0;

    // Check for each subarray for the required condition
    for (int i = 0; i <= n - 1; i++) {
        int ctX = 0, ctY = 0;
        for (int j = i; j <= n - 1; j++) {
            if (arr[j] == x)
                ctX += 1;
            else if (arr[j] == y)
                ctY += 1;
            if (ctX == ctY)
                result += 1;        
        }
    }

    return (result);
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 2, 3, 4, 1 };
    int n = arr.length;
    int x = 2, y = 3;
    System.out.println(sameOccurrence(arr, n, x, y));

}
}

// This code is contributed by
// Sahil_shelangia
```

## 蟒蛇 3

```
# Python 3 program to count number of
# sub-arrays in which number of occurrence
# of x is equal to that of y using brute force
def sameOccurrence(arr, n, x, y):
    result = 0

    # Check for each subarray for
    # the required condition
    for i in range(n):
        ctX = 0
        ctY = 0
        for j in range(i, n, 1):
            if (arr[j] == x):
                ctX += 1;
            elif (arr[j] == y):
                ctY += 1
            if (ctX == ctY):
                result += 1

    return (result)

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 2, 3, 4, 1]
    n = len(arr)
    x = 2
    y = 3
    print(sameOccurrence(arr, n, x, y))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
/* C# program to count number of sub-arrays in which
number of occurrence of x is equal to that of y
using brute force */
using System;

class GFG
{

static int sameOccurrence(int[] arr, int n,
                            int x, int y)
{
    int result = 0;

    // Check for each subarray for
    // the required condition
    for (int i = 0; i <= n - 1; i++)
    {
        int ctX = 0, ctY = 0;
        for (int j = i; j <= n - 1; j++)
        {
            if (arr[j] == x)
                ctX += 1;
            else if (arr[j] == y)
                ctY += 1;
            if (ctX == ctY)
                result += 1;        
        }
    }
    return (result);
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 2, 3, 4, 1 };
    int n = arr.Length;
    int x = 2, y = 3;
    Console.Write(sameOccurrence(arr, n, x, y));

}
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of sub-arrays
// in which number of occurrence of x is equal
// to that of y using brute force

function sameOccurrence($arr, $n, $x, $y)
{
    $result = 0;

    // Check for each subarray for the
    // required condition
    for ($i = 0; $i <= $n - 1; $i++)
    {
        $ctX = 0; $ctY = 0;
        for ( $j = $i; $j <= $n - 1; $j++)
        {
            if ($arr[$j] == $x)
                $ctX += 1;
            else if ($arr[$j] == $y)
                $ctY += 1;
            if ($ctX == $ctY)
                $result += 1;    
        }
    }

    return ($result);
}

// Driver code
$arr = array( 1, 2, 2, 3, 4, 1 );
$n = count($arr);
$x = 2; $y = 3;
echo sameOccurrence($arr, $n, $x, $y);

// This code is contributed by 29AjayKumar
?>
```

## java 描述语言

```
<script>

// Javascript program to count number
// of sub-arrays in which number of
// occurrence of x is equal to that of y
// using brute force
function sameOccurrence(arr, n, x, y)
{
    let result = 0;

    // Check for each subarray for the
    // required condition
    for(let i = 0; i <= n - 1; i++)
    {
        let ctX = 0, ctY = 0;
        for(let j = i; j <= n - 1; j++)
        {
            if (arr[j] == x)
                ctX += 1;
            else if (arr[j] == y)
                ctY += 1;
            if (ctX == ctY)
                result += 1;        
        }
    }
    return(result);
}

// Driver code
let arr = [ 1, 2, 2, 3, 4, 1 ];
let n = arr.length;
let x = 2, y = 3;

document.write(sameOccurrence(arr, n, x, y));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
7
```

**时间复杂度–**o(n^2)
**辅助空间–**o(1)

**有效方法(O(N)时间复杂度):**

在这个解中，辅助空间是 O(N)，时间复杂度也是 O(N)。我们创建两个数组，比如 countX[]和 COuntry[]，分别表示到数组中的那个点为止 x 和 y 的出现次数。然后，我们计算另一个数组，比如 diff，它存储(COuntx[I]-COuntry[I])，I 是数组的索引。现在，将数组 diff 的每个元素的计数存储在一个映射中，比如 m。将结果初始化为 m[0]，因为 diff 数组中 0 的出现为我们提供了子数组计数，其中遵循了所需的条件。现在，遍历映射并使用握手公式更新结果，因为 diff 数组中的两个相同值表示子数组包含相同数量的 x 和 y。

```
Explanation:
arr[] = {1, 2, 2, 3, 4, 1};
x = 2, y = 3;

Two arrays countX[] and countY[] are be evaluated as-
countX[] = {0, 1, 2, 2, 2, 2};
countY[] = {0, 0, 0, 1, 1, 1};

Hence, diff[] = {0, 1, 2, 1, 1, 1}; 
(diff[i] = countX[i]-countY[i], i be the index of array)

Now, create a map and store the count of each element of diff in it,
so, finally, we get-
m[0] = 1, m[1] = 4, m[2] = 1;

Initialize result as m[0]
i.e result = m[0] = 1

Further, using handshake formula, updating the 
result as follows-
result  = result + (1*(1-1))/2 = 1 + 0 = 1
result  = result + (4*(4-1))/2 = 1 + 6 = 7
result  = result + (1*(1-1))/2 = 7 + 0 = 7

so, the final result will be 7, required subarrays having 
same number of occurrences of x and y.
```

## C++

```
/* C++ program to count number of sub-arrays in which
  number of occurrence of x is equal to that of y using
  efficient approach in terms of time */
#include <bits/stdc++.h>
using namespace std;

int sameOccurrence(int arr[], int n, int x, int y)
{
    int countX[n], countY[n];

    map<int, int> m; // To store counts of same diffs

    // Count occurrences of x and y
    for (int i = 0; i < n; i++) {
        if (arr[i] == x) {
            if (i != 0)
                countX[i] = countX[i - 1] + 1;
            else
                countX[i] = 1;
        } else {
            if (i != 0)
                countX[i] = countX[i - 1];
            else
                countX[i] = 0;
        }
        if (arr[i] == y) {
            if (i != 0)
                countY[i] = countY[i - 1] + 1;
            else
                countY[i] = 1;
        } else {
            if (i != 0)
                countY[i] = countY[i - 1];
            else
                countY[i] = 0;
        }

         // Increment count of current
         m[countX[i] - countY[i]]++;
    }

    // Traverse map and commute result.
    int result = m[0];
    for (auto it = m.begin(); it != m.end(); it++)
        result = result + ((it->second) * ((it->second) - 1)) / 2;

    return (result);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 3, 4, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 2, y = 3;
    cout << sameOccurrence(arr, n, x, y);
    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to count number of sub-arrays in which
number of occurrence of x is equal to that of y using
efficient approach in terms of time */
import java.util.*;

class GFG
{

static int sameOccurrence(int arr[], int n, int x, int y)
{
    int []countX = new int[n];
    int []countY = new int[n];

    Map<Integer,Integer> m = new HashMap<>();

    // To store counts of same diff
    // Count occurrences of x and y
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == x)
        {
            if (i != 0)
                countX[i] = countX[i - 1] + 1;
            else
                countX[i] = 1;
        }
        else
        {
            if (i != 0)
                countX[i] = countX[i - 1];
            else
                countX[i] = 0;
        }
        if (arr[i] == y)
        {
            if (i != 0)
                countY[i] = countY[i - 1] + 1;
            else
                countY[i] = 1;
        }
        else
        {
            if (i != 0)
                countY[i] = countY[i - 1];
            else
                countY[i] = 0;
        }

        // Increment count of current
        if(m.containsKey(countX[i] - countY[i]))
        {
            m.put(countX[i] - countY[i], m.get(countX[i] - countY[i])+1);
        }
        else
        {
            m.put(countX[i] - countY[i], 1);
        }
    }

    // Traverse map and commute result.
    int result = m.get(0);
    for (Map.Entry<Integer,Integer> it : m.entrySet())
        result = result + ((it.getValue()) * ((it.getValue()) - 1)) / 2;

    return (result);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 3, 4, 1 };
    int n = arr.length;
    int x = 2, y = 3;
    System.out.println(sameOccurrence(arr, n, x, y));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count number of
# sub-arrays in which number of occurrence
# of x is equal to that of y using efficient
# approach in terms of time */
def sameOccurrence( arr, n, x, y):

    countX = [0 for i in range(n)]
    countY = [0 for i in range(n)]

    # To store counts of same diffs
    m = dict()

    # Count occurrences of x and y
    for i in range(n):
        if (arr[i] == x):
            if (i != 0):
                countX[i] = countX[i - 1] + 1
            else:
                countX[i] = 1
        else:
            if (i != 0):
                countX[i] = countX[i - 1]
            else:
                countX[i] = 0

        if (arr[i] == y):
            if (i != 0):
                countY[i] = countY[i - 1] + 1
            else:
                countY[i] = 1
        else:
            if (i != 0):
                countY[i] = countY[i - 1]
            else:
                countY[i] = 0

        # Increment count of current
        m[countX[i] - countY[i]] = m.get(countX[i] -
                                         countY[i], 0) + 1

    # Traverse map and commute result.
    result = m[0]
    for j in m:
        result += (m[j] * (m[j] - 1)) // 2

    return result

# Driver code
arr = [1, 2, 2, 3, 4, 1]
n = len(arr)
x, y = 2, 3
print(sameOccurrence(arr, n, x, y))

# This code is contributed
# by mohit kumar
```

## C#

```
/* C# program to count number of sub-arrays in which
number of occurrence of x is equal to that of y using
efficient approach in terms of time */
using System;
using System.Collections.Generic;

class GFG
{

static int sameOccurrence(int []arr, int n, int x, int y)
{
    int []countX = new int[n];
    int []countY = new int[n];

    Dictionary<int,int> m = new Dictionary<int,int>();

    // To store counts of same diff
    // Count occurrences of x and y
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == x)
        {
            if (i != 0)
                countX[i] = countX[i - 1] + 1;
            else
                countX[i] = 1;
        }
        else
        {
            if (i != 0)
                countX[i] = countX[i - 1];
            else
                countX[i] = 0;
        }
        if (arr[i] == y)
        {
            if (i != 0)
                countY[i] = countY[i - 1] + 1;
            else
                countY[i] = 1;
        }
        else
        {
            if (i != 0)
                countY[i] = countY[i - 1];
            else
                countY[i] = 0;
        }

        // Increment count of current
        if(m.ContainsKey(countX[i] - countY[i]))
        {
            var v = m[countX[i] - countY[i]]+1;
            m.Remove(countX[i] - countY[i]);
            m.Add(countX[i] - countY[i], v);
        }
        else
        {
            m.Add(countX[i] - countY[i], 1);
        }
    }

    // Traverse map and commute result.
    int result = m[0];
    foreach(KeyValuePair<int, int> it in m)
        result = result + ((it.Value) * ((it.Value) - 1)) / 2;

    return (result);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 2, 3, 4, 1 };
    int n = arr.Length;
    int x = 2, y = 3;
    Console.WriteLine(sameOccurrence(arr, n, x, y));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

/* Javascript program to count number of sub-arrays in which
number of occurrence of x is equal to that of y using
efficient approach in terms of time */

    function sameOccurrence(arr,n,x,y)
    {
        let countX = new Array(n);
        let countY = new Array(n);

        let m = new Map();

        // To store counts of same diff
    // Count occurrences of x and y
    for (let i = 0; i < n; i++)
    {
        if (arr[i] == x)
        {
            if (i != 0)
                countX[i] = countX[i - 1] + 1;
            else
                countX[i] = 1;
        }
        else
        {
            if (i != 0)
                countX[i] = countX[i - 1];
            else
                countX[i] = 0;
        }
        if (arr[i] == y)
        {
            if (i != 0)
                countY[i] = countY[i - 1] + 1;
            else
                countY[i] = 1;
        }
        else
        {
            if (i != 0)
                countY[i] = countY[i - 1];
            else
                countY[i] = 0;
        }

        // Increment count of current
        if(m.has(countX[i] - countY[i]))
        {
            m.set(countX[i] - countY[i], m.get(countX[i] - countY[i])+1);
        }
        else
        {
            m.set(countX[i] - countY[i], 1);
        }
    }

    // Traverse map and commute result.
    let result = m.get(0);
    for (let [key, value] of m.entries())
        result = result + (value) * ((value) - 1) / 2;

    return (result);
    }

    // Driver code
    let arr=[1, 2, 2, 3, 4, 1];
    let n = arr.length;
    let x = 2, y = 3;
    document.write(sameOccurrence(arr, n, x, y));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
7
```

**时间复杂度–**O(N)
T3】辅助空间–O(N)

本文由 [**Divyanshu_Gupta**](https://auth.geeksforgeeks.org/profile.php?user=Divyanshu_Gupta) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。