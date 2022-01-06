# 在给定范围内用单位数字 k 计数

> 原文:[https://www . geesforgeks . org/count-numbers-unit-digit-k-给定范围/](https://www.geeksforgeeks.org/count-numbers-unit-digit-k-given-range/)

这里给定一个从低到高的范围，给定一个数字 k，你必须找出一个数字与 k 有相同位数的计数
**例:**

```
Input: low = 2, high = 35, k = 2   
Output: 4
Numbers are 2, 12, 22, 32  

Input: low = 3, high = 30, k = 3 
Output: 3
Numbers are  3, 13, 23
```

一种**简单的方法**是遍历给定范围内的所有数字，检查每个数字的最后一个数字，如果最后一个数字等于 k，则递增结果

## C++

```
// Simple CPP program to count numbers with
// last digit as k in given range.
#include <bits/stdc++.h>
using namespace std;

// Returns count of numbers with k as last
// digit.
int counLastDigitK(int low, int high, int k)
{
    int count = 0;
    for (int i = low; i <= high; i++)
        if (i % 10 == k)
            count++;  
    return count;
}

// Driver Program
int main()
{
    int low = 3, high = 35, k = 3;
    cout << counLastDigitK(low, high, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to count numbers with
// last digit as k in given range.
import java.util.*;
import java.lang.*;

public class GfG
{
    // Returns count of numbers with
    // k as last digit.
    public static int counLastDigitK(int low,
                                int high, int k)
    {
        int count = 0;
        for (int i = low; i <= high; i++)
            if (i % 10 == k)
                count++;
        return count;
    }

    // driver function
    public static void main(String args[])
    {
        int low = 3, high = 35, k = 3;
        System.out.println(counLastDigitK(low, high, k));
    }
}

// This code is contributed by Sagar Shukla
```

## 蟒蛇 3

```
# Simple python program to count numbers with
# last digit as k in given range.

# Returns count of numbers with k as last
# digit.
def counLastDigitK(low, high, k):
    count = 0
    for i in range(low, high+1):
        if (i % 10 == k):
            count+=1
    return count

# Driver Program
low = 3
high = 35
k = 3
print(counLastDigitK(low, high, k))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// Simple C# program to count numbers with
// last digit as k in given range.
using System;

public class GfG
{
    // Returns count of numbers with
    // k as last digit.
    public static int counLastDigitK(int low,
                                int high, int k)
    {
        int count = 0;
        for (int i = low; i <= high; i++)
            if (i % 10 == k)
                count++;
        return count;
    }

    // Driver function
    public static void Main()
    {
        int low = 3, high = 35, k = 3;
        Console.WriteLine(counLastDigitK(low, high, k));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to count numbers with
// last digit as k in given range.

// Returns count of numbers with
// k as last digit.
function counLastDigitK($low, $high, $k)
{
    $count = 0;
    for ($i = $low; $i <= $high; $i++)
        if ($i % 10 == $k)
            $count++;
    return $count;
}

    // Driver Code
    $low = 3;
    $high = 35;
    $k = 3;
    echo counLastDigitK($low, $high, $k);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// java script  PHP program to count numbers with
// last digit as k in given range.

// Returns count of numbers with
// k as last digit.
function counLastDigitK(low, high, k)
{
    let count = 0;
    for (let i = low; i <= high; i++)
        if (i % 10 == k)
            count++;
    return count;
}

    // Driver Code
    let low = 3;
    let high = 35;
    let k = 3;
    document.write( counLastDigitK(low, high, k));

// This code is contributed
// by sravan kumar
</script>
```

**输出:**

```
4
```

**时间复杂度:** O(高–低)

一个**高效的解决方案**是基于每 10 个连续数字中，每个数字作为最后一个数字出现一次。

## C++

```
// Efficient CPP program to count numbers 
// with last digit as k in given range.
#include <bits/stdc++.h>
using namespace std;

// Returns count of numbers with k as last
// digit.
int countLastDigitK(long long low,
        long long high, long long K)
{

  long long mlow = 10 * ceil(low/10.0);
  long long mhigh = 10 * floor(high/10.0);

  int count = (mhigh - mlow)/10;
  if (high % 10 >= K)
    count++;
  if (low % 10 <=K && (low%10))
    count++;

  return count;
}

// Driver Code
int main()
{
    int low = 3, high = 35, k = 3;
    cout << countLastDigitK(low, high, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to count numbers
// with last digit as k in given range.
import java.util.*;
import java.lang.*;

public class GfG
{
    // Returns count of numbers with
    // k as last digit.
    public static int counLastDigitK(int low,
                             int high, int k)
    {
        int mlow = 10 * (int)
                      Math.ceil(low/10.0);
        int mhigh = 10 * (int)
                      Math.floor(high/10.0);
        int count = (mhigh - mlow)/10;
        if (high % 10 >= k)
            count++;
        if (low % 10 <= k && (low%10) > 0)
            count++;
        return count;
    }

    // driver function
    public static void main(String argc[])
    {
        int low = 3, high = 35, k = 3;
        System.out.println(counLastDigitK(low, high, k));
    }
}

// This code is contributed by Sagar Shukla
```

## 蟒蛇 3

```
import math
# Efficient python program to count numbers
# with last digit as k in given range.

# Returns count of numbers with k as last
# digit.
def counLastDigitK(low, high, k):
    mlow = 10 * math.ceil(low/10.0)
    mhigh = 10 * int(high/10.0)

    count = (mhigh - mlow)/10
    if (high % 10 >= k):
        count += 1
    if (low % 10 <= k and \
        (low%10) > 0):
        count += 1
    return int(count)

# Driver Code
low = 3
high = 35
k = 3
print(counLastDigitK(low, high, k))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// Efficient Java program to count numbers
// with last digit as k in given range.
using System;

public class GfG
{
    // Returns count of numbers with
    // k as last digit.
    public static int counLastDigitK(int low,
                                int high, int k)
    {
        int mlow = 10 * Convert.ToInt32(
                  Math.Ceiling(low/10.0));
        int mhigh = 10 * Convert.ToInt32(
                  Math.Floor(high/10.0));
        int count = (mhigh - mlow) / 10;
        if (high % 10 >= k)
            count++;
        if (low % 10 <= k && (low%10) > 0)
            count++;
        return count;
    }

    // Driver function
    public static void Main()
    {
        int low = 3, high = 35, k = 3;
        Console.WriteLine(
          counLastDigitK(low, high, k));
    }
}

// This code is contributed by vt_m
```

## java 描述语言

```
<script>
    // Efficient Javascript program to count numbers
    // with last digit as k in given range.

    // Returns count of numbers with
    // k as last digit.
    function counLastDigitK(low, high, k)
    {
        let mlow = 10 * (Math.ceil(low/10.0));
        let mhigh = 10 * (Math.floor(high/10.0));
        let count = (mhigh - mlow) / 10;
        if (high % 10 >= k)
            count++;
        if (low % 10 <= k && (low%10) > 0)
            count++;
        return count;
    }

    let low = 3, high = 35, k = 3;
    document.write(counLastDigitK(low, high, k));

</script>
```

**Output**

```
4
```

**时间复杂度:** O(1)