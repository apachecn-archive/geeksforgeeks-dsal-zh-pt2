# 要移除的最小元素，使得相邻元素的总和总是奇数

> 原文:[https://www . geeksforgeeks . org/待移除的最小元素-这样相邻元素的总和总是奇数/](https://www.geeksforgeeks.org/minimum-elements-to-be-removed-such-that-sum-of-adjacent-elements-is-always-odd/)

给定一个 N 个整数的数组。任务是消除最小数量的元素，以便在结果数组中任何两个相邻值的和都是奇数。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 0
> 所有相邻元素之和已经是奇数。
> **输入:** arr[] = {1，3，5，4，2}
> **输出:** 3
> 消除 3，5 和 2，以便在结果数组中任意两个相邻值的和为奇数。

**趋近**两个数之和为奇数，如果其中一个为奇数，另一个为偶数。这意味着，对于每对具有相同奇偶性的连续数字，去掉其中一个，哪个并不重要。所以下面的贪婪算法是有效的:

*   按顺序浏览所有元素。
*   如果当前数字与前一个数字具有相同的奇偶校验，则将其消除，否则不要消除。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Returns the minimum number of eliminations
int min_elimination(int n, int arr [])
{
    int count = 0;

    // Stores the previous element
    int prev_val = arr[0];

    // Stores the new value
    for (int i = 1; i < n; i++)
    {
        int curr_val = arr[i];

        // Check if the previous and current
        // values are of same parity
        if (curr_val % 2 == prev_val % 2)
            count++;

        // Previous value is now the current value
        prev_val = curr_val;
    }

    // Return the counter variable
    return count;
}

// Driver code
int main()
{
    int arr [] = { 1, 2, 3, 7, 9 };
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << min_elimination(n, arr);

    return 0;
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG {

    // Returns the minimum number of eliminations
    static int min_elimination(int n, int[] arr)
    {
        int count = 0;

        // Stores the previous element
        int prev_val = arr[0];

        // Stores the new value
        for (int i = 1; i < n; i++) {
            int curr_val = arr[i];

            // Check if the previous and current
            // values are of same parity
            if (curr_val % 2 == prev_val % 2)
                count++;

            // Previous value is now the current value
            prev_val = curr_val;
        }

        // Return the counter variable
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = new int[] { 1, 2, 3, 7, 9 };
        int n = arr.length;

        System.out.println(min_elimination(n, arr));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Returns the minimum number of eliminations
def min_elimination(n, arr):

    count = 0

    # Stores the previous element
    prev_val = arr[0]

    # Stores the new value
    for i in range (1, n):
        curr_val = arr[i];

        # Check if the previous and current
        # values are of same parity
        if (curr_val % 2 == prev_val % 2):
            count = count + 1

        # Previous value is now the current value
        prev_val = curr_val

    # Return the counter variable
    return count

# Driver code
arr = [ 1, 2, 3, 7, 9 ]
n = len(arr)

print(min_elimination(n, arr));

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Returns the minimum number of eliminations
    static int min_elimination(int n, int[] arr)
    {
        int count = 0;

        // Stores the previous element
        int prev_val = arr[0];

        // Stores the new value
        for (int i = 1; i < n; i++)
        {
            int curr_val = arr[i];

            // Check if the previous and current
            // values are of same parity
            if (curr_val % 2 == prev_val % 2)
                count++;

            // Previous value is now the current value
            prev_val = curr_val;
        }

        // Return the counter variable
        return count;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = new int[] { 1, 2, 3, 7, 9 };
        int n = arr.Length;

        Console.WriteLine(min_elimination(n, arr));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Returns the minimum number of eliminations
function min_elimination($n, $arr)
{
    $count = 0;

    // Stores the previous element
    $prev_val = $arr[0];

    // Stores the new value
    for ($i = 1; $i < $n; $i++)
    {
        $curr_val = $arr[$i];

        // Check if the previous and current
        // values are of same parity
        if ($curr_val % 2 == $prev_val % 2)
            $count++;

        // Previous value is now the
        // current value
        $prev_val = $curr_val;
    }

    // Return the counter variable
    return $count;
}

// Driver code
$arr = array( 1, 2, 3, 7, 9 );
$n = sizeof($arr);

echo min_elimination($n, $arr);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Returns the minimum number of eliminations
function min_elimination(n,arr)
{
    let count = 0;

    // Stores the previous element
    let prev_val = arr[0];

    // Stores the new value
    for (let i = 1; i < n; i++)
    {
        let curr_val = arr[i];

        // Check if the previous and current
        // values are of same parity
        if (curr_val % 2 == prev_val % 2)
            count++;

        // Previous value is now the current value
        prev_val = curr_val;
    }

    // Return the counter variable
    return count;
}

// Driver code

let arr = [1, 2, 3, 7, 9];
let n = arr.length;

document.write(min_elimination(n, arr));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(1)