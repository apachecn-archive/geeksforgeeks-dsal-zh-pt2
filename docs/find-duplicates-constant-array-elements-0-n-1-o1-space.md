# 在 O(1)空间中寻找元素为 0 到 N-1 的常量数组中的重复项

> 原文:[https://www . geesforgeks . org/find-duplicates-constant-array-elements-0-n-1-O1-space/](https://www.geeksforgeeks.org/find-duplicates-constant-array-elements-0-n-1-o1-space/)

给定 n 个元素的**常数数组**，其中包含从 1 到 n-1 的元素，这些数字中的任何一个出现任意次。在 O(n)中找到这些重复数字中的任何一个，并且只使用恒定的内存空间。
**例:**

```
Input : arr[] = {1, 2, 3, 4, 5, 6, 3}
Output : 3
```

由于给定的数组是常量，下面文章中给出的方法将不起作用。

1.  [在 O(n)个时间和 O(1)个额外空间中查找重复|设置 1](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/)
2.  [用 O(n)和使用 O(1)额外空间在数组中复制| Set-2](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-2/)

1.  我们从 0 开始取两个变量 i & j
2.  我们将运行循环，直到我到达最后一个 elem 或找到重复的 elem
3.  我们将预先增加 j 值，以便将 elem 与下一个 elem 进行比较
4.  如果我们没有找到 elem，我们将增加 I，因为 j 将指向最后一个 elem，然后用 I 重新定位 j

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a duplicate
// element in an array with values in
// range from 0 to n-1.
import java.io.*;
import java.util.*;

public class GFG {

    // function to find one duplicate
    static int findduplicate(int []a, int n)
    {

        int i=0,j=0;
        while(i<n){
            if(a[i]==a[++j]) return a[j];
            if(j==n-1) {
                i++;
                j=i;
            }
        }
        return -1;
    }

    public static void main(String args[])
    {
        int []arr = {1, 2, 4, 3, 4, 5, 6, 3};
        int n = arr.length;
        System.out.print(findduplicate(arr, n));
    }
}

// This code is contributed by
// Love Raj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a duplicate
// element in an array with values in
// range from 0 to n-1.
import java.io.*;
import java.util.*;

public class GFG {

    // function to find one duplicate
    static int findduplicate(int []arr, int n)
    {

        // return -1 because in these cases
        // there can not be any repeated element
        if (n <= 1)
            return -1;

        // initialize fast and slow
        int slow = arr[0];
        int fast = arr[arr[0]];

        // loop to enter in the cycle
        while (fast != slow)
        {

            // move one step for slow
            slow = arr[slow];

            // move two step for fast
            fast = arr[arr[fast]];
        }

        // loop to find entry
        // point of the cycle
        fast = 0;
        while (slow != fast)
        {
            slow = arr[slow];
            fast = arr[fast];
        }
        return slow;
    }

    // Driver Code
    public static void main(String args[])
    {
        int []arr = {1, 2, 3, 4, 5, 6, 3};
        int n = arr.length;
        System.out.print(findduplicate(arr, n));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python 3 program to find a duplicate
# element in an array with values in
# range from 0 to n-1.

# function to find one duplicate
def findduplicate(arr, n):

    # return -1 because in these cases
    # there can not be any repeated element
    if (n <= 1):
        return -1

    # initialize fast and slow
    slow = arr[0]
    fast = arr[arr[0]]

    # loop to enter in the cycle
    while (fast != slow) :

        # move one step for slow
        slow = arr[slow]

        # move two step for fast
        fast = arr[arr[fast]]

    # loop to find entry point of the cycle
    fast = 0
    while (slow != fast):
        slow = arr[slow]
        fast = arr[fast]
    return slow

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4, 5, 6, 3 ]
    n = len(arr)
    print(findduplicate(arr, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find a duplicate
// element in an array with values in
// range from 0 to n-1.
using System;
using System.Collections.Generic;
class GFG {

    // function to find one duplicate
    static int findduplicate(int []arr, int n)
    {

        // return -1 because in these cases
        // there can not be any repeated element
        if (n <= 1)
            return -1;

        // initialize fast and slow
        int slow = arr[0];
        int fast = arr[arr[0]];

        // loop to enter in the cycle
        while (fast != slow)
        {

            // move one step for slow
            slow = arr[slow];

            // move two step for fast
            fast = arr[arr[fast]];
        }

        // loop to find entry
        // point of the cycle
        fast = 0;
        while (slow != fast)
        {
            slow = arr[slow];
            fast = arr[fast];
        }
        return slow;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 5, 6, 3};
        int n = arr.Length;
        Console.Write(findduplicate(arr, n));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a duplicate
// element in an array with values in
// range from 0 to n-1.

// function to find one duplicate
function findduplicate($arr, $n)
{
    // return -1 because in these cases
    // there can not be any repeated element
    if ($n <= 1)
        return -1;

    // initialize fast and slow
    $slow = $arr[0];
    $fast = $arr[$arr[0]];

    // loop to enter in the cycle
    while ($fast != $slow)
    {

        // move one step for slow
        $slow = $arr[$slow];

        // move two step for fast
        $fast = $arr[$arr[$fast]];
    }

    // loop to find entry point of the cycle
    $fast = 0;
    while ($slow != $fast)
    {
        $slow = $arr[$slow];
        $fast = $arr[$fast];
    }
    return $slow;
}

// Driver Code
$arr = array( 1, 2, 3, 4, 5, 6, 3 );
$n = sizeof($arr);
echo findduplicate($arr, $n);

// This code is contributed by Tushil
?>
```

## java 描述语言

```
<script>

    // Javascript program to find a duplicate
    // element in an array with values in
    // range from 0 to n-1.

    // function to find one duplicate
    function findduplicate(arr, n)
    {

        // return -1 because in these cases
        // there can not be any repeated element
        if (n <= 1)
            return -1;

        // initialize fast and slow
        let slow = arr[0];
        let fast = arr[arr[0]];

        // loop to enter in the cycle
        while (fast != slow)
        {

            // move one step for slow
            slow = arr[slow];

            // move two step for fast
            fast = arr[arr[fast]];
        }

        // loop to find entry
        // point of the cycle
        fast = 0;
        while (slow != fast)
        {
            slow = arr[slow];
            fast = arr[fast];
        }
        return slow;
    }

    let arr = [1, 2, 3, 4, 5, 6, 3];
    let n = arr.length;
    document.write(findduplicate(arr, n));

</script>
```

**输出:**

```
3
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)