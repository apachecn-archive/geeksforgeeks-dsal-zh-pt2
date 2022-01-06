# 可以翻转的 0 的最大数量，使得数组没有相邻的 1

> 原文:[https://www . geesforgeks . org/可翻转的最大 0 数-这样阵列就没有相邻的 1/](https://www.geeksforgeeks.org/maximum-number-of-0s-that-can-be-flipped-such-that-array-has-no-adjacent-1s/)

给定一个二进制数组 **arr** ，任务是找到可以翻转的 0 的最大数量，使得该数组没有相邻的 1，即该数组在连续的索引处不包含任何两个 1。
**例:**

> **输入:** arr[] = {1，0，0，0，1}
> **输出:** 1
> **说明:**
> 索引 2 处的 0 可以替换为 1。
> **输入:** arr[] = {1，0，0，1}
> **输出:** 0
> **解释:**
> 没有 0(零)可以被 1 代替，因此没有两个连续的索引有 1。

**进场:**

*   迭代数组，对于每个有 0 的索引，检查其相邻的两个索引是否有 0。对于数组的最后一个和第一个索引，分别检查相邻的左索引和右索引。
*   对于满足上述条件的每个这样的索引，增加计数。
*   在最后打印最终计数作为所需答案

下面的代码是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Maximum number of 0s that
// can be replaced by 1
int canReplace(int array[], int n)
{
    int i = 0, count = 0;

    while (i < n)
    {

        // Check for three consecutive 0s
        if (array[i] == 0 &&
            (i == 0 || array[i - 1] == 0) &&
            (i == n - 1|| array[i + 1] == 0))
        {

            // Flip the bit
            array[i] = 1;

            // Increase the count
            count++;
        }
        i++;
    }
    return count;
}

// Driver's Code
int main()
{
    int array[5] = { 1, 0, 0, 0, 1 };    

    cout << canReplace(array, 5);
}

// This code is contributed by spp____
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class geeks {

    // Maximum number of 0s that
    // can be replaced by 1
    public static int canReplace(
        int[] array)
    {
        int i = 0, count = 0;

        while (i < array.length) {

            // Check for three consecutive 0s
            if (array[i] == 0
                && (i == 0
                    || array[i - 1] == 0)
                && (i == array.length - 1
                    || array[i + 1] == 0)) {

                // Flip the bit
                array[i] = 1;

                // Increase the count
                count++;
            }
            i++;
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] array = { 1, 0, 0, 0, 1 };
        System.out.println(canReplace(array));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Maximum number of 0s that
# can be replaced by 1
def canReplace(arr, n):

    i = 0
    count = 0

    while (i < n):

        # Check for three consecutive 0s
        if (arr[i] == 0 and
                (i == 0 or arr[i - 1] == 0) and
                (i == n - 1 or arr[i + 1] == 0)):

            # Flip the bit
            arr[i] = 1

            # Increase the count
            count += 1

        i += 1
    return count

# Driver code
if __name__ == '__main__':

    arr = [ 1, 0, 0, 0, 1]

    print(canReplace(arr, 5))

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Maximum number of 0s that
// can be replaced by 1
public static int canReplace(int[] array)
{
    int i = 0, count = 0;
    while (i < array.Length)
    {

        // Check for three consecutive 0s
        if (array[i] == 0 &&
           (i == 0 || array[i - 1] == 0) &&
           (i == array.Length - 1 || array[i + 1] == 0))
        {

            // Flip the bit
            array[i] = 1;

            // Increase the count
            count++;
        }
        i++;
    }

    return count;
}

// Driver code
public static void Main(String []args)
{
    int[] array = { 1, 0, 0, 0, 1 };

    Console.WriteLine(canReplace(array));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Maximum number of 0s that
// can be replaced by 1
function canReplace(array, n)
{
    var i = 0, count = 0;

    while (i < n)
    {

        // Check for three consecutive 0s
        if (array[i] == 0 &&
            (i == 0 || array[i - 1] == 0) &&
            (i == n - 1|| array[i + 1] == 0))
        {

            // Flip the bit
            array[i] = 1;

            // Increase the count
            count++;
        }
        i++;
    }
    return count;
}

// Driver's Code
    array = [1, 0, 0, 0, 1]    

    document.write(canReplace(array, 5));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*T4】