# 数组中的对(x，y)计数，使得 x < y

> 原文:[https://www . geeksforgeeks . org/对计数-x-y-in-a-so-x-y/](https://www.geeksforgeeks.org/count-of-pairs-x-y-in-an-array-such-that-x-y/)

给定一组 **N 个**不同的整数，任务是找出对的数量 **(x，y)** ，使得 **x < y** 。

**示例:**

> **输入:** arr[] = {2，4，3，1}
> **输出:** 6
> 可能的对是(1，2)，(1，3)，(1，4)，(2，3)，(2，4)和(3，4)。
> **输入:** arr[] = {5，10}
> **输出:** 1
> 唯一可能的对是(5，10)。

**天真方法:**找出每一个可能的配对，检查它是否满足给定条件。

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the number of
// pairs (x, y) such that x < y
int getPairs(int a[],int n)
{
    // To store the number of valid pairs
    int count = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // If a valid pair is found
            if (a[i] < a[j])
                count++;
        }
    }

    // Return the count of valid pairs
    return count;
}

// Driver code
int main()
{
    int a[] = { 2, 4, 3, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << getPairs(a, n);
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the number of
    // pairs (x, y) such that x < y
    static int getPairs(int a[])
    {
        // To store the number of valid pairs
        int count = 0;
        for (int i = 0; i < a.length; i++) {
            for (int j = 0; j < a.length; j++) {

                // If a valid pair is found
                if (a[i] < a[j])
                    count++;
            }
        }

        // Return the count of valid pairs
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 4, 3, 1 };
        System.out.println(getPairs(a));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of
# pairs (x, y) such that x < y
def getPairs(a):

    # To store the number of valid pairs
    count = 0
    for i in range(len(a)):
        for j in range(len(a)):

            # If a valid pair is found
            if (a[i] < a[j]):
                count += 1

    # Return the count of valid pairs
    return count

# Driver code
if __name__ == "__main__":

    a = [ 2, 4, 3, 1 ]
    print(getPairs(a))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the number of
    // pairs (x, y) such that x < y
    static int getPairs(int []a)
    {
        // To store the number of valid pairs
        int count = 0;
        for (int i = 0; i < a.Length; i++)
        {
            for (int j = 0; j < a.Length; j++)
            {

                // If a valid pair is found
                if (a[i] < a[j])
                    count++;
            }
        }

        // Return the count of valid pairs
        return count;
    }

    // Driver code
    public static void Main()
    {
        int []a = { 2, 4, 3, 1 };
        Console.WriteLine(getPairs(a));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of
// pairs (x, y) such that x < y
function getPairs($a)
{
    // To store the number of valid pairs
    $count = 0;
    for ($i = 0; $i < sizeof($a); $i++)
    {
        for ($j = 0; $j < sizeof($a); $j++)
        {

            // If a valid pair is found
            if ($a[$i] < $a[$j])
                $count++;
        }
    }

    // Return the count of valid pairs
    return $count;
}

// Driver code
$a = array(2, 4, 3, 1);
echo getPairs($a);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function to return the number of
    // pairs (x, y) such that x < y
    function getPairs(a)
    {
        // To store the number of valid pairs
        let count = 0;
        for (let i = 0; i < a.length; i++) {
            for (let j = 0; j < a.length; j++) {

                // If a valid pair is found
                if (a[i] < a[j])
                    count++;
            }
        }

        // Return the count of valid pairs
        return count;
    }

    // Driver code
    let a=[ 2, 4, 3, 1 ];
    document.write(getPairs(a));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(n <sup>2</sup>

**有效方法:**对于一个元素 **x** 。为了找到形式 **(x，y1)** 、 **(x，y2)** 、…、 **(x，yn)** 的有效对的计数，我们需要计数大于 **x** 的元素。对于最小的元素，会有大于它的**n–1**元素。同样，第二小元素可以形成**n–2**对，以此类推。因此，有效对的期望计数将是**(n–1)+(n–2)+…。+1 = n *(n–1)/2**，其中 **n** 是数组的长度。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// pairs (x, y) such that x < y
int getPairs(int a[])
{
    // Length of the array
    int n = sizeof(a[0]);

    // Calculate the number valid pairs
    int count = (n * (n - 1)) / 2;

    // Return the count of valid pairs
    return count;
}

// Driver code
int main()
{
    int a[] = { 2, 4, 3, 1 };
    cout << getPairs(a);
    return 0;
}

// This code is contributed
// by SHUBHAMSINGH10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the number of
    // pairs (x, y) such that x < y
    static int getPairs(int a[])
    {
        // Length of the array
        int n = a.length;

        // Calculate the number of valid pairs
        int count = (n * (n - 1)) / 2;

        // Return the count of valid pairs
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 4, 3, 1 };
        System.out.println(getPairs(a));
    }
}
```

## 计算机编程语言

```
# Python implementation of the approach

# Function to return the number of
# pairs (x, y) such that x < y
def getPairs(a):

    # Length of the array
    n = len(a)

    # Calculate the number of valid pairs
    count = (n * (n - 1)) // 2

    # Return the count of valid pairs
    return count

# Driver code
a = [2, 4, 3, 1]
print(getPairs(a))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function to return the number of
    // pairs (x, y) such that x < y
    static int getPairs(int []a)
    {
        // Length of the array
        int n = a.Length;

        // Calculate the number of valid pairs
        int count = (n * (n - 1)) / 2;

        // Return the count of valid pairs
        return count;
    }

    // Driver code
    public static void Main()
    {
        int []a = { 2, 4, 3, 1 };
        Console.Write(getPairs(a));
    }
}

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the number of
    // pairs (x, y) such that x < y
    function getPairs(a)
    {
        // Length of the array
        let n = a.length;

        // Calculate the number of valid pairs
        let count = parseInt((n * (n - 1)) / 2, 10);

        // Return the count of valid pairs
        return count;
    }

    let a = [ 2, 4, 3, 1 ];
      document.write(getPairs(a));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(1)