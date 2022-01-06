# 计算从 1 到 N 的所有数字中未设置的总位数

> 原文:[https://www . geesforgeks . org/count-total-unset-bit-in-all-numbers-from-1-n/](https://www.geeksforgeeks.org/count-total-unset-bits-in-all-the-numbers-from-1-to-n/)

给定一个正整数 **N** ，任务是计算从 **1** 到 **N** 的所有数字的二进制表示中未置位的总位数。**注意**前导零不会被计为未设置的位。
**举例:**

> **输入:** N = 5
> **输出:** 4
> 
> <figure class="table">
> 
> | 整数 | 二进制表示法 | 未设置位的计数 |
> | --- | --- | --- |
> | one | one | Zero |
> | Two | Ten | one |
> | three | Eleven | Zero |
> | four | One hundred | Two |
> | five | One hundred and one | one |
> 
> 0 + 1 + 0 + 2 + 1 = 4
> **输入:** N = 14
> **输出:** 17
> 
> </figure>

**进场:**

1.  重复从 **1** 到 **N** 的循环。
2.  当数大于 **0** 时，除以 **2** 并检查余数。
3.  如果余数等于 **0** ，则将**计数**的值增加 **1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of unset
// bits in the binary representation of
// all the numbers from 1 to n
int countUnsetBits(int n)
{

    // To store the count of unset bits
    int cnt = 0;

    // For every integer from the range [1, n]
    for (int i = 1; i <= n; i++) {

        // A copy of the current integer
        int temp = i;

        // Count of unset bits in
        // the current integer
        while (temp) {

            // If current bit is unset
            if (temp % 2 == 0)
                cnt++;

            temp = temp / 2;
        }
    }
    return cnt;
}

// Driver code
int main()
{
    int n = 5;

    cout << countUnsetBits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count of unset
    // bits in the binary representation of
    // all the numbers from 1 to n
    static int countUnsetBits(int n)
    {

        // To store the count of unset bits
        int cnt = 0;

        // For every integer from the range [1, n]
        for (int i = 1; i <= n; i++)
        {

            // A copy of the current integer
            int temp = i;

            // Count of unset bits in
            // the current integer
            while (temp > 0)
            {

                // If current bit is unset
                if (temp % 2 == 0)
                {
                    cnt = cnt + 1;
                }

                temp = temp / 2;
            }
        }
        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(countUnsetBits(n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of unset
# bits in the binary representation of
# all the numbers from 1 to n
def countUnsetBits(n) :

    # To store the count of unset bits
    cnt = 0;

    # For every integer from the range [1, n]
    for i in range(1, n + 1) :

        # A copy of the current integer
        temp = i;

        # Count of unset bits in
        # the current integer
        while (temp) :

            # If current bit is unset
            if (temp % 2 == 0) :
                cnt += 1;

            temp = temp // 2;

    return cnt;

# Driver code
if __name__ == "__main__" :

    n = 5;

    print(countUnsetBits(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of unset
    // bits in the binary representation of
    // all the numbers from 1 to n
    static int countUnsetBits(int n)
    {

        // To store the count of unset bits
        int cnt = 0;

        // For every integer from the range [1, n]
        for (int i = 1; i <= n; i++)
        {

            // A copy of the current integer
            int temp = i;

            // Count of unset bits in
            // the current integer
            while (temp > 0)
            {

                // If current bit is unset
                if (temp % 2 == 0)
                    cnt = cnt + 1;

                temp = temp / 2;
            }
        }
        return cnt;
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        Console.Write(countUnsetBits(n));
    }
}

// This code is contributed by Sanjit_Prasad
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of unset
// bits in the binary representation of
// all the numbers from 1 to n
function countUnsetBits(n)
{

    // To store the count of unset bits
    var cnt = 0;

    // For every integer from the range [1, n]
    for (var i = 1; i <= n; i++) {

        // A copy of the current integer
        var temp = i;

        // Count of unset bits in
        // the current integer
        while (temp) {

            // If current bit is unset
            if (temp % 2 == 0)
                cnt++;

            temp = parseInt(temp / 2);
        }
    }
    return cnt;
}

// Driver code
var n = 5;
document.write( countUnsetBits(n));

</script>
```

**Output:** 

```
4
```

时间复杂度:O(n * log n)

辅助空间:0(1)