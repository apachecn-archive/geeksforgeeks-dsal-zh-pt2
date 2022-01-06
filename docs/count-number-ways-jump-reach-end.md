# 计数跳跃到达终点的方式数

> 原文:[https://www . geesforgeks . org/count-number-way-jump-reach-end/](https://www.geeksforgeeks.org/count-number-ways-jump-reach-end/)

给定一个数字数组，其中每个元素代表从该元素向前跳的最大次数。对于每个数组元素，计算从该元素跳转到数组末尾的次数。如果一个元素为 0，则不能通过该元素进行移动。不能到达终点的元素应该有一个计数“-1”。

**示例:**

```
Input : {3, 2, 0, 1}
Output : 2 1 -1 0
For 3 number of steps or jumps that 
can be taken are 1, 2 or 3\. The different ways are:
3 -> 2 -> 1
3 -> 1

For 2 number of steps or jumps that 
can be taken are 1, or 2\. The different ways are:
2 -> 1

For 0 number of steps or jumps that 
can be taken are 0\. 
One cannot move forward from this point.

For 1 number of steps or jumps that 
can be taken are 1\. But the element is at
the end so no jump is required.

Input : {1, 3, 5, 8, 9, 1, 0, 7, 6, 8, 9}
Output : 52 52 28 16 8 -1 -1 4 2 1 0
```

这个问题是[到达终点的最小跳跃次数(方法 3)](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/) 的变体。这里我们需要计算从每个细胞到达终点的所有方法。
解决方案是[到达终点的最小跳跃次数(方法 3)](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/) 问题的修改版本。
这个问题旨在统计从每个元素跳到最后的不同方式。对于每个元素，计数是通过将所有能够到达终点且当前元素能够到达+ 1(如果元素能够直接到达终点)的正向元素的计数相加来计算的。

**算法:**

```
countWays(arr, n)
    Initialize array count_jump[n] = {0}

    count_jump[n-1] = 0
    for i = n-2 to 0
        if arr[i] >= (n-i-1)
         count_jump[i]++
        for j=i+1; j < n-1 && j <= arr[i]+i; i++
          if count_jump[j] != -1
             count_jump[i] += count_jump[j]
        if count_jump[i] == 0
         count_jump[i] = -1

    for i = 0 to n-1
        print count_jump[i]
```

## C++

```
// C++ implementation to count number
// of ways to jump to reach end
#include <bits/stdc++.h>
using namespace std;

// function to count ways to jump to
// reach end for each array element
void countWaysToJump(int arr[], int n)
{
    // count_jump[i] store number of ways
    // arr[i] can reach to the end
    int count_jump[n];
    memset(count_jump, 0, sizeof(count_jump));

    // Last element does not require to jump.
    // Count ways to jump for remaining
    // elements
    for (int i=n-2; i>=0; i--)
    {
        // if the element can directly
        // jump to the end
        if (arr[i] >= n - i - 1)
            count_jump[i]++;

        // add the count of all the elements
        // that can reach to end and arr[i] can
        // reach to them
        for (int j=i+1; j < n-1 && j <= arr[i] + i; j++)

            // if element can reach to end then add
            // its count to count_jump[i]
            if (count_jump[j] != -1)
                 count_jump[i] += count_jump[j];

        // if arr[i] cannot reach to the end
        if (count_jump[i] == 0)
            count_jump[i] = -1;
    }

    // print count_jump for each
    // array element
    for (int i=0; i<n; i++)
        cout << count_jump[i] << " ";
}

// Driver program to test above
int main()
{
    int arr[] = {1, 3, 5, 8, 9, 1, 0, 7, 6, 8, 9};
    int n = sizeof(arr) / sizeof(arr[0]);
    countWaysToJump(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count number
// of ways to jump to reach end
import java.util.Arrays;

class GFG {

    // function to count ways to jump to
    // reach end for each array element
    static void countWaysToJump(int arr[], int n)
    {

        // count_jump[i] store number of ways
        // arr[i] can reach to the end
        int count_jump[] = new int[n];
        Arrays.fill(count_jump, 0);

        // Last element does not require to jump.
        // Count ways to jump for remaining
        // elements
        for (int i = n-2; i >= 0; i--)
        {

            // if the element can directly
            // jump to the end
            if (arr[i] >= n - i - 1)
                count_jump[i]++;

            // add the count of all the elements
            // that can reach to end and arr[i] can
            // reach to them
            for (int j = i+1; j < n-1 && j <= arr[i] + i; j++)

                // if element can reach to end then add
                // its count to count_jump[i]
                if (count_jump[j] != -1)
                    count_jump[i] += count_jump[j];

            // if arr[i] cannot reach to the end
            if (count_jump[i] == 0)
                count_jump[i] = -1;
        }

        // print count_jump for each
        // array element
        for (int i = 0; i < n; i++)
            System.out.print(count_jump[i] + " ");
    }

    //driver code
    public static void main (String[] args)
    {

        int arr[] = {1, 3, 5, 8, 9, 1, 0, 7, 6, 8, 9};
        int n = arr.length;

        countWaysToJump(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to count
# number of ways to jump to reach end

# Function to count ways to jump to
# reach end for each array element
def countWaysToJump(arr, n):

    # count_jump[i] store number of ways
    # arr[i] can reach to the end
    count_jump = [0 for i in range(n)]

    # Last element does not require
    # to jump. Count ways to jump for
    # remaining elements
    for i in range(n - 2, -1, -1):

        # if the element can directly
        # jump to the end
        if (arr[i] >= n - i - 1):
            count_jump[i] += 1

        # Add the count of all the elements
        # that can reach to end and arr[i]
        # can reach to them
        j = i + 1
        while(j < n-1 and j <= arr[i] + i):

            # if element can reach to end then
            # add its count to count_jump[i]
            if (count_jump[j] != -1):
                count_jump[i] += count_jump[j]
            j += 1

        # if arr[i] cannot reach to the end
        if (count_jump[i] == 0):
            count_jump[i] = -1

    # print count_jump for each
    # array element
    for i in range(n):
        print(count_jump[i], end = " ")

# Driver code
arr = [1, 3, 5, 8, 9, 1, 0, 7, 6, 8, 9]
n = len(arr)
countWaysToJump(arr, n)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to count number
// of ways to jump to reach end
using System;

class GFG {

    // function to count ways to jump to
    // reach end for each array element
    static void countWaysToJump(int[] arr, int n)
    {

        // count_jump[i] store number of ways
        // arr[i] can reach to the end
        int[] count_jump = new int[n];

        for(int i = 0; i < n; i++)
            count_jump[i] = 0;

        // Last element does not require to jump.
        // Count ways to jump for remaining
        // elements
        for (int i = n-2; i >= 0; i--)
        {

            // if the element can directly
            // jump to the end
            if (arr[i] >= n - i - 1)
                count_jump[i]++;

            // add the count of all the elements
            // that can reach to end and arr[i] can
            // reach to them
            for (int j = i+1; j < n-1 && j <= arr[i] + i; j++)

                // if element can reach to end then add
                // its count to count_jump[i]
                if (count_jump[j] != -1)
                    count_jump[i] += count_jump[j];

            // if arr[i] cannot reach to the end
            if (count_jump[i] == 0)
                count_jump[i] = -1;
        }

        // print count_jump for each
        // array element
        for (int i = 0; i < n; i++)
            Console.Write(count_jump[i] + " ");
    }

    // Driver code
    public static void Main ()
    {
        int[] arr = {1, 3, 5, 8, 9,
                 1, 0, 7, 6, 8, 9};
        int n = arr.Length;
        countWaysToJump(arr, n);
    }
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count number
// of ways to jump to reach end

// function to count ways to jump to
// reach end for each array element
function countWaysToJump($arr, $n)
{
    // count_jump[i] store number of ways
    // arr[i] can reach to the end
    $count_jump;
    for($i = 0; $i < $n; $i++)
        $count_jump[$i] = 0;

    // Last element does not require to jump.
    // Count ways to jump for remaining
    // elements
    for ($i = $n - 2; $i >= 0; $i--)
    {
        // if the element can directly
        // jump to the end
        if ($arr[$i] >= $n - $i - 1)
            $count_jump[$i]++;

        // add the count of all the elements
        // that can reach to end and arr[i]
        // can reach to them
        for ($j = $i + 1; $j < $n - 1 &&
             $j <= $arr[$i] + $i; $j++)

            // if element can reach to end then
            // add its count to count_jump[i]
            if ($count_jump[$j] != -1)
                $count_jump[$i] += $count_jump[$j];

        // if arr[i] cannot reach to the end
        if ($count_jump[$i] == 0)
            $count_jump[$i] = -1;
    }

    // print count_jump for each
    // array element
    for ($i = 0; $i < $n; $i++)
        echo $count_jump[$i] . " ";
}

// Driver Code
$arr = array(1, 3, 5, 8, 9, 1,
                0, 7, 6, 8, 9);
$n = count($arr);
countWaysToJump($arr, $n);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript implementation to count number
// of ways to jump to reach end

    // function to count ways to jump to
    // reach end for each array element
    function countWaysToJump(arr,n)
    {
        // count_jump[i] store number of ways
        // arr[i] can reach to the end
        let count_jump = new Array(n);
        for(let i=0;i<n;i++)
        {
            count_jump[i]=0;
        }

        // Last element does not require to jump.
        // Count ways to jump for remaining
        // elements
        for (let i = n-2; i >= 0; i--)
        {

            // if the element can directly
            // jump to the end
            if (arr[i] >= n - i - 1)
                count_jump[i]++;

            // add the count of all the elements
            // that can reach to end and arr[i] can
            // reach to them
            for (let j = i+1; j < n-1 && j <= arr[i] + i; j++)

                // if element can reach to end then add
                // its count to count_jump[i]
                if (count_jump[j] != -1)
                    count_jump[i] += count_jump[j];

            // if arr[i] cannot reach to the end
            if (count_jump[i] == 0)
                count_jump[i] = -1;
        }

        // print count_jump for each
        // array element
        for (let i = 0; i < n; i++)
            document.write(count_jump[i] + " ");
    }

    //driver code
    let arr=[1, 3, 5, 8, 9, 1, 0, 7, 6, 8, 9];
    let n = arr.length;
    countWaysToJump(arr, n);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
52 52 28 16 8 -1 -1 4 2 1 0
```

**时间复杂度:最坏情况下** O(n <sup>2</sup> )。