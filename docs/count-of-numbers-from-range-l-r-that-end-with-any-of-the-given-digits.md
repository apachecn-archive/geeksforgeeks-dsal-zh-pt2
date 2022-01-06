# 从范围[L，R]开始以任意给定数字结束的数字计数

> 原文:[https://www . geesforgeks . org/从范围 l-r-以任意给定数字结尾的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-from-range-l-r-that-end-with-any-of-the-given-digits/)

给定一个范围**【L，R】**，任务是从最后一位数字为 **2** 、 **3** 或 **9** 的范围中找出数字的个数。
**举例:**

> **输入:** L = 1，R = 3
> **输出:** 2
> 2 和 3 是唯一有效的数字。
> **输入:** L = 11，R = 33
> **输出:** 8

**方法:**初始化计数器计数= 0，并对范围内的每个元素运行循环，如果当前元素以任何给定的数字结束，则递增计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count
// of the required numbers
int countNums(int l, int r)
{
    int cnt = 0;

    for (int i = l; i <= r; i++)
    {

        // Last digit of the current number
        int lastDigit = (i % 10);

        // If the last digit is equal to
        // any of the given digits
        if ((lastDigit % 10) == 2 || (lastDigit % 10) == 3
            || (lastDigit % 10) == 9)
        {
            cnt++;
        }
    }

    return cnt;
}

// Driver code
int main()
{
    int l = 11, r = 33;
    cout << countNums(l, r) ;
}

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count
    // of the required numbers
    static int countNums(int l, int r)
    {
        int cnt = 0;

        for (int i = l; i <= r; i++) {

            // Last digit of the current number
            int lastDigit = (i % 10);

            // If the last digit is equal to
            // any of the given digits
            if ((lastDigit % 10) == 2 || (lastDigit % 10) == 3
                || (lastDigit % 10) == 9) {
                cnt++;
            }
        }

        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int l = 11, r = 33;
        System.out.print(countNums(l, r));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of the required numbers
def countNums(l, r) :
    cnt = 0;

    for i in range(l, r + 1) :

        # Last digit of the current number
        lastDigit = (i % 10);

        # If the last digit is equal to
        # any of the given digits
        if ((lastDigit % 10) == 2 or (lastDigit % 10) == 3
            or (lastDigit % 10) == 9) :

            cnt += 1;

    return cnt;

# Driver code
if __name__ == "__main__" :

    l = 11; r = 33;

    print(countNums(l, r)) ;

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of the required numbers
    static int countNums(int l, int r)
    {
        int cnt = 0;

        for (int i = l; i <= r; i++)
        {

            // Last digit of the current number
            int lastDigit = (i % 10);

            // If the last digit is equal to
            // any of the given digits
            if ((lastDigit % 10) == 2 ||
                (lastDigit % 10) == 3 ||
                (lastDigit % 10) == 9)
            {
                cnt++;
            }
        }
        return cnt;
    }

    // Driver code
    public static void Main()
    {
        int l = 11, r = 33;
        Console.Write(countNums(l, r));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the count
    // of the required numbers
    function countNums(l, r)
    {
        let cnt = 0;

        for (let i = l; i <= r; i++) {

            // Last digit of the current number
            let lastDigit = (i % 10);

            // If the last digit is equal to
            // any of the given digits
            if ((lastDigit % 10) == 2 || (lastDigit % 10) == 3
                || (lastDigit % 10) == 9) {
                cnt++;
            }
        }

        return cnt;
    }

    let l = 11, r = 33;
      document.write(countNums(l, r));

</script>
```

**Output:** 

```
8
```