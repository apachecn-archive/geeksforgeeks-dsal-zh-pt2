# 最少 1 秒借出力量使整个阵列强大

> 原文:[https://www . geesforgeks . org/minimum-1s-make-整数组-power/](https://www.geeksforgeeks.org/minimum-1s-make-whole-array-powerful/)

给定一个二进制数组和一个整数 k，其中每个 1 都有幂，它可以把幂借给邻居和它自己。值为 1 的电池可以在距离< **k** 内供电。任务是找到需要借出能量的最小 1 数，以便所有细胞都变得强大。
如果无法让全阵强大，返回-1。
**示例:**

```
Input  : arr[] = {0, 1, 1, 1, 1, 0}                
             K = 2 
Output : 2
arr[1] and arr[5] need to lend

Input  :  arr[] = {1, 0, 1, 0, 0, 1, 0, 0, 0, 1}        
              K = 3
Output : 3
a[2], a[5] and a[9] lend to their right side zeros.

Input  :  arr[] = {1, 1, 1}        
              K = 2
Output : 1
arr[1] need to lend power to all cells.
```

一个**简单的解决方法**就是尝试所有可能的 1 的组合，从一个 1 开始，然后是两个 1，以此类推，直到我们找到一个让整个数组强大的组合。
一个**有效的解决方案**是基于每个小区在距离 k 内应该有一个 1 的观察。我们对数组进行预处理，并创建一个辅助数组，在左侧存储最接近 1 的索引。我们遍历整个数组，找到当前单元格 k 距离内最近的左 1 的索引。如果没有剩余的 1，我们返回-1。否则，我们增加 ans 并在 k 距离后移动到下一个单元格。

## C++

```
// C++ program to minimum of number of lendings
// by 1s.
#include <bits/stdc++.h>
using namespace std;

int minLendings(int arr[], int n, int k)
{
    // Create an auxiliary array and fill
    // indexes of closest 1s on left side.
    int leftOne[n];
    int oneInd = -1;
    for (int i = 0; i < n; i++) {
        if (arr[i] == 1)
            oneInd = i;
        leftOne[i] = oneInd;
    }

    // Traverse the array from left side. If
    // current element has a 1 on
    int ans = 0;
    for (int i = 0; i < n;) {

        // Find index of closest 1 after shift of
        // k-1 or end whichever is closer.
        int pos = leftOne[min(i + k - 1, n - 1)];

        // If there is no closest 1 within allowed
        // range.
        if (pos == -1 || pos + k <= i)
            return -1;

        // If a closest 1 is found, check after k
        // jumps and increment answer.
        i = pos + k;
        ans++;
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 0, 1, 1, 1, 1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << minLendings(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimum of number of
// lendings by 1s.
import java.math.*;

class GFG {

static int minLendings(int arr[], int n, int k)
{
    // Create an auxiliary array and fill
    // indexes of closest 1s on left side.
    int leftOne[] = new int[n];
    int oneInd = -1;
    for (int i = 0; i < n; i++) {
        if (arr[i] == 1)
            oneInd = i;
        leftOne[i] = oneInd;
    }

    // Traverse the array from left side. If
    // current element has a 1 on
    int ans = 0;
    for (int i = 0; i < n;) {

        // Find index of closest 1 after shift of
        // k-1 or end whichever is closer.
        int pos = leftOne[Math.min(i + k - 1, n - 1)];

        // If there is no closest 1 within
        // allowed range.
        if (pos == -1 || pos + k <= i)
            return -1;

        // If a closest 1 is found, check after k
        // jumps and increment answer.
        i = pos + k;
        ans++;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 1, 1, 1, 0 };
    int n = arr.length;
    int k = 2;
    System.out.println(minLendings(arr, n, k));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to minimum
# of number of lendings by 1s.

def minLendings(arr, n, k):

    # Create an auxiliary array and fill
    # indexes of closest 1s on left side.
    leftOne = [0 for i in range(n + 1)]
    oneInd = -1

    for i in range(n):
        if (arr[i] == 1):
            oneInd = i
        leftOne[i] = oneInd

    # Traverse the array from left side.
    # If current element has a 1 on
    ans = 0; i = 0

    while(i < n):

        # Find index of closest 1 after shift of
        # k-1 or end whichever is closer.
        pos = leftOne[min(i + k - 1, n - 1)]

        # If there is no closest 1 
        # within allowed range.
        if (pos == -1 or pos + k <= i):
            return -1

        # If a closest 1 is found, check after k
        # jumps and increment answer.
        i = pos + k
        ans += 1

    return ans

# Driver program
arr = [ 0, 1, 1, 1, 1, 0 ]
n = len(arr)
k = 2
print(minLendings(arr, n, k))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to minimum of number of
// lendings by 1s.
using System;

class GFG {

    static int minLendings(int []arr, int n, int k)
    {

        // Create an auxiliary array and fill
        // indexes of closest 1s on left side.
        int []leftOne = new int[n];
        int oneInd = -1;
        for (int i = 0; i < n; i++)
        {
            if (arr[i] == 1)
                oneInd = i;
            leftOne[i] = oneInd;
        }

        // Traverse the array from left side.
        // If current element has a 1 on
        int ans = 0;
        for (int i = 0; i < n;)
        {

            // Find index of closest 1 after
            // shift of k-1 or end whichever
            // is closer.
            int pos = leftOne[Math.Min(i + k - 1,
                                          n - 1)];

            // If there is no closest 1 within
            // allowed range.
            if (pos == -1 || pos + k <= i)
                return -1;

            // If a closest 1 is found, check
            // after k jumps and increment answer.
            i = pos + k;
            ans++;
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 0, 1, 1, 1, 1, 0 };
        int n = arr.Length;
        int k = 2;

        Console.WriteLine(minLendings(arr, n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to minimum of
// number of lendings by 1s.
function minLendings($arr, $n, $k)
{
    // Create an auxiliary array 
    // and fill indexes of closest
    // 1s on left side.
    $leftOne[$n] = array(0);
        $oneInd = -1;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == 1)
            $oneInd = $i;
        $leftOne[$i] = $oneInd;
    }

    // Traverse the array from
    // left side. If current
    // element has a 1 on
    $ans = 0;
    for ($i = 0; $i < $n😉
    {

        // Find index of closest 1 after
        // shift of k-1 or end whichever
        // is closer.
        $pos = $leftOne[min($i + $k - 1, $n - 1)];

        // If there is no closest 1
        // within allowed range.
        if ($pos == -1 || $pos + $k <= $i)
            return -1;

        // If a closest 1 is found, check
        // after k jumps and increment answer.
        $i = $pos + $k;
        $ans++;
    }
    return $ans;
}

// Driver code
$arr = array(0, 1, 1, 1, 1, 0 );
$n = sizeof($arr);
$k = 2;
echo minLendings($arr, $n, $k);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript program to minimum of number of lendings by 1s.

    function minLendings(arr, n, k)
    {

        // Create an auxiliary array and fill
        // indexes of closest 1s on left side.
        let leftOne = new Array(n);
        let oneInd = -1;
        for (let i = 0; i < n; i++)
        {
            if (arr[i] == 1)
                oneInd = i;
            leftOne[i] = oneInd;
        }

        // Traverse the array from left side.
        // If current element has a 1 on
        let ans = 0;
        for (let i = 0; i < n;)
        {

            // Find index of closest 1 after
            // shift of k-1 or end whichever
            // is closer.
            let pos = leftOne[Math.min(i + k - 1, n - 1)];

            // If there is no closest 1 within
            // allowed range.
            if (pos == -1 || pos + k <= i)
                return -1;

            // If a closest 1 is found, check
            // after k jumps and increment answer.
            i = pos + k;
            ans++;
        }

        return ans;
    }

    let arr = [ 0, 1, 1, 1, 1, 0 ];
    let n = arr.length;
    let k = 2;

    document.write(minLendings(arr, n, k));

</script>
```

**输出:**

```
2
```

该算法的时间复杂度为 **O(n)** 。
本文由 [**碧湖普拉萨德帕拉**](https://auth.geeksforgeeks.org/profile.php?user=Bibhu Pala) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。