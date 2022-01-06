# 要相加得到 N 的位置为 9 的最小数字

> 原文:[https://www . geesforgeks . org/最小数字加 1-place-as-9-to-add-get-n/](https://www.geeksforgeeks.org/minimum-numbers-with-ones-place-as-9-to-be-added-to-get-n/)

给定一个整数 **N** ，任务是找出需要相加得到 **N** 的最小个数。(所有这些数字都必须有 **9** 作为数字)

**示例:**

> **输入:**N = 27
> T3】输出: 3
> 27 = 9 + 9 + 9
> 
> **输入:** N = 109
> **输出:** 1
> 109 本身有 9 为一位数。

**进场:**

*   检查 **N** 的一位数，根据一位数可以很容易地找到需要相加的最小个数。
*   如果一个人的数字是 **9:** 答案会是 **1** ，因为这个数字本身就有 **9** 作为自己的位置数字。
*   如果某人的数字是:
    1.  **1:** 9 必须加 9 次(即 9 * 9 = 81)。
    2.  **2:** 9 必须加 8 次(即 9 * 8 = 72)。
    3.  **3:** 9 要加 7 次(即 9 * 7 = 63)。
    4.  **4:** 9 必须加 6 次(即 9 * 6 = 54)。
    5.  **5:** 9 要加 5 次(即 9 * 5 = 45)。
    6.  **6:** 9 要加 4 次(即 9 * 4 = 36)。
    7.  **7:** 9 要加 3 次(即 9 * 3 = 27)。
    8.  **8:** 9 要加 2 次(即 9 * 2 = 18)。
    9.  **0:** 9 必须加 10 次(即 9 * 10 = 90)。
*   这里的观察是，只需添加上述所有情况的最小倍数计数。这是因为把自己的数字说成 **4** ，6 个数字中的所有 **9** (自己的位置)都可以用，结果可以从 **N** 中减去，说是 **M** 。现在， **M** 会有 **0** 在自己的位置上。所以，就用 **5** 号作为 **9** ，用第六号作为 **(M + 9)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count
// of numbers(with one's digit 9)
// that sum up to N
int findMin(int N)
{
    // Fetch one's digit
    int digit = N % 10;

    // Apply Cases mentioned in approach
    switch (digit) {
    case 0:
        if (N >= 90)
            return 10;
        break;
    case 1:
        if (N >= 81)
            return 9;
        break;
    case 2:
        if (N >= 72)
            return 8;
        break;
    case 3:
        if (N >= 63)
            return 7;
        break;
    case 4:
        if (N >= 54)
            return 6;
        break;
    case 5:
        if (N >= 45)
            return 5;
        break;
    case 6:
        if (N >= 36)
            return 4;
        break;
    case 7:
        if (N >= 27)
            return 3;
        break;
    case 8:
        if (N >= 18)
            return 2;
        break;
    case 9:
        if (N >= 9)
            return 1;
        break;
    }

    // If no possible answer exists
    return -1;
}

// Driver code
int main()
{
    int N = 27;

    cout << findMin(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find minimum count
    // of numbers(with one's digit 9)
    // that sum up to N
    static int findMin(int N)
    {
        // Fetch one's digit
        int digit = N % 10;

        // Apply Cases mentioned in approach
        switch (digit)
        {
            case 0:
                if (N >= 90)
                    return 10;
                break;
            case 1:
                if (N >= 81)
                    return 9;
                break;
            case 2:
                if (N >= 72)
                    return 8;
                break;
            case 3:
                if (N >= 63)
                    return 7;
                break;
            case 4:
                if (N >= 54)
                    return 6;
                break;
            case 5:
                if (N >= 45)
                    return 5;
                break;
            case 6:
                if (N >= 36)
                    return 4;
                break;
            case 7:
                if (N >= 27)
                    return 3;
                break;
            case 8:
                if (N >= 18)
                    return 2;
                break;
            case 9:
                if (N >= 9)
                    return 1;
                break;
        }

        // If no possible answer exists
        return -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 27;

        System.out.println(findMin(N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find minimum count
# of numbers(with one's digit 9)
# that sum up to N
def findMin(N: int):

    # Fetch one's digit
    digit = N % 10

    # Apply Cases mentioned in approach
    if digit == 0 and N >= 90:
        return 10
    elif digit == 1 and N >= 81:
        return 9
    elif digit == 2 and N >= 72:
        return 8
    elif digit == 3 and N >= 63:
        return 7
    elif digit == 4 and N >= 54:
        return 6
    elif digit == 5 and N >= 45:
        return 5
    elif digit == 6 and N >= 36:
        return 4
    elif digit == 7 and N >= 27:
        return 3
    elif digit == 8 and N >= 18:
        return 2
    elif digit == 9 and N >= 9:
        return 1

    # If no possible answer exists
    return -1

# Driver Code
if __name__ == "__main__":
    N = 27
    print(findMin(N))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;        

class GFG
{

    // Function to find minimum count
    // of numbers(with one's digit 9)
    // that sum up to N
    static int findMin(int N)
    {
        // Fetch one's digit
        int digit = N % 10;

        // Apply Cases mentioned in approach
        switch (digit)
        {
            case 0:
                if (N >= 90)
                    return 10;
                break;
            case 1:
                if (N >= 81)
                    return 9;
                break;
            case 2:
                if (N >= 72)
                    return 8;
                break;
            case 3:
                if (N >= 63)
                    return 7;
                break;
            case 4:
                if (N >= 54)
                    return 6;
                break;
            case 5:
                if (N >= 45)
                    return 5;
                break;
            case 6:
                if (N >= 36)
                    return 4;
                break;
            case 7:
                if (N >= 27)
                    return 3;
                break;
            case 8:
                if (N >= 18)
                    return 2;
                break;
            case 9:
                if (N >= 9)
                    return 1;
                break;
        }

        // If no possible answer exists
        return -1;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int N = 27;

        Console.WriteLine(findMin(N));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find minimum count
// of numbers(with one's digit 9)
// that sum up to N
function findMin(N)
{

    // Fetch one's digit
    let digit = N % 10;

    // Apply Cases mentioned in approach
    switch (digit)
    {
        case 0:
            if (N >= 90)
                return 10;
            break;
        case 1:
            if (N >= 81)
                return 9;
            break;
        case 2:
            if (N >= 72)
                return 8;
            break;
        case 3:
            if (N >= 63)
                return 7;
            break;
        case 4:
            if (N >= 54)
                return 6;
            break;
        case 5:
            if (N >= 45)
                return 5;
            break;
        case 6:
            if (N >= 36)
                return 4;
            break;
        case 7:
            if (N >= 27)
                return 3;
            break;
        case 8:
            if (N >= 18)
                return 2;
            break;
        case 9:
            if (N >= 9)
                return 1;
            break;
    }

    // If no possible answer exists
    return -1;
}

// Driver code
let N = 27;

document.write(findMin(N));

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
3
```