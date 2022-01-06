# 位大小最多为 X 且按位“或”等于 X 的对的计数

> 原文:[https://www . geesforgeks . org/最多具有 x 位大小的对计数和按位或等于 x/](https://www.geeksforgeeks.org/count-of-pairs-having-bit-size-at-most-x-and-bitwise-or-equal-to-x/)

给定一个**数 X** ，计算可能的对数 **(a，b)** ，使得 a 和 b 的[位或](https://www.geeksforgeeks.org/bitwise-or-or-of-a-range/)等于 X，a 和 b 中的位数都小于等于 X 中的位数

**例:**

> **输入:** X = 6
> **输出:** 9
> **解释:**
> 可能的(a，b)对是(4，6)，(6，4)，(6，6)，(6，2)，(4，2)，(6，0)，(2，6)，(2，6)，(2，6)，(2，4)，(0，6)。
> **输入:** X = 21
> **输出:** 27
> **说明:**
> 总共有 27 对可能。

**方法:**要解决上述问题，请遵循以下步骤:

*   遍历给定数字 x 的每一位
*   **如果该位为 1** ，那么从按位或的真值表中，我们知道在数字 a 和 b 中，给定的位有 3 种可能的组合，即(0，1)，(1，0)，(1，1)即 3 种可能的方式。
*   **如果该位为 0** ，那么从按位“或”的真值表中，我们知道在数字 a 和 b 中给定的位只有一种可能的组合，即(0，0)。
*   所以我们的答案是 3 ^(x 中的位数)。

以下是上述方法的实现:

## C++

```
// C++ implementation to Count number of
// possible pairs of (a, b) such that
// their Bitwise OR gives the value X

#include <iostream>
using namespace std;

// Function to count the pairs
int count_pairs(int x)
{
    // Initializing answer with 1
    int ans = 1;

    // Iterating through bits of x
    while (x > 0) {

        // check if bit is 1
        if (x % 2 == 1)

            // multiplying ans by 3
            // if bit is 1
            ans = ans * 3;

        x = x / 2;
    }
    return ans;
}

// Driver code
int main()
{
    int X = 6;

    cout << count_pairs(X)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count number of
// possible pairs of (a, b) such that
// their Bitwise OR gives the value X
class GFG{

// Function to count the pairs
static int count_pairs(int x)
{

    // Initializing answer with 1
    int ans = 1;

    // Iterating through bits of x
    while (x > 0)
    {

        // Check if bit is 1
        if (x % 2 == 1)

            // Multiplying ans by 3
            // if bit is 1
            ans = ans * 3;

        x = x / 2;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int X = 6;

    System.out.print(count_pairs(X) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to count number of
# possible pairs of (a, b) such that
# their Bitwise OR gives the value X

# Function to count the pairs
def count_pairs(x):

    # Initializing answer with 1
    ans = 1;

    # Iterating through bits of x
    while (x > 0):

        # Check if bit is 1
        if (x % 2 == 1):

            # Multiplying ans by 3
            # if bit is 1
            ans = ans * 3;

        x = x // 2;

    return ans;

# Driver code
if __name__ == '__main__':

    X = 6;

    print(count_pairs(X));

# This code is contributed by amal kumar choubey
```

## C#

```
// C# implementation to count number of
// possible pairs of (a, b) such that
// their Bitwise OR gives the value X
using System;
class GFG{

  // Function to count the pairs
  static int count_pairs(int x)
  {

    // Initializing answer with 1
    int ans = 1;

    // Iterating through bits of x
    while (x > 0)
    {

      // Check if bit is 1
      if (x % 2 == 1)

        // Multiplying ans by 3
        // if bit is 1
        ans = ans * 3;

      x = x / 2;
    }
    return ans;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int X = 6;

    Console.Write(count_pairs(X) + "\n");
  }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// javascript implementation to count number of
// possible pairs of (a, b) such that
// their Bitwise OR gives the value X   
// Function to count the pairs
    function count_pairs(x) {

        // Initializing answer with 1
        var ans = 1;

        // Iterating through bits of x
        while (x > 0) {

            // Check if bit is 1
            if (x % 2 == 1)

                // Multiplying ans by 3
                // if bit is 1
                ans = ans * 3;

            x = parseInt(x / 2);
        }
        return ans;
    }

    // Driver code

        var X = 6;

        document.write(count_pairs(X) + "\n");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(log(X))*