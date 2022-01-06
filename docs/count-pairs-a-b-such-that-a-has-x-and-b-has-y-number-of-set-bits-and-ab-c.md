# 对(A，B)进行计数，使得 A 具有 X，B 具有 Y 数量的设定位，并且 A+B = C

> 原文:[https://www . geesforgeks . org/count-pairs-a-b-so-a-has-x-and-b-has-y-set-bits-and-ab-c/](https://www.geeksforgeeks.org/count-pairs-a-b-such-that-a-has-x-and-b-has-y-number-of-set-bits-and-ab-c/)

给定两个数字 x，y，表示设定位数。还给出了一个数字 c。任务是打印我们可以形成两个数字 A 和 B 的方式数，这样 A 有 x 个设置位，B 有 y 个设置位，A+B = c。
**示例** :

```
Input: X = 1, Y = 1, C = 3 
Output: 2 
So two possible ways are (A = 2 and B = 1) and (A = 1 and B = 2)

Input: X = 2, Y = 2, C = 20 
Output: 3 
```

**递归方式:**上述问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)解决。递归计算对的总数。会有 4 种可能。我们从最右边的比特位置开始。

1.  如果 C 的位位置是 1，那么在该索引处有四种可能得到 1。
    *   如果进位是 0，那么我们可以使用 X 中的 1 位和 Y 中的 0 位，反之亦然，这样就不会为下一步生成进位。
    *   如果进位是 1，那么我们可以使用来自每个的 1 个设置位，为下一步生成进位，否则我们使用来自 X 和 Y 的不生成进位的不设置位。
2.  如果 C 的位位置是 0，那么在该位位置有四种可能得到 0。
    *   如果进位是 1，那么我们可以使用 X 的 1 个置位位和 Y 的 0 个置位，反之亦然，这为下一步生成进位 1。
    *   如果进位是 0，那么我们可以分别使用 X 和 Y 中的 1 和 1，这为下一步生成进位 1。我们还可以使用无设置位，这不会为下一步生成进位。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to generate
// all combinations of bits
int func(int third, int seta, int setb,
         int carry, int number)
{

    // find if C has no more set bits on left
    int shift = (number >> third);

    // if no set bits are left for C
    // and there are no set bits for A and B
    // and the carry is 0, then
    // this combination is possible
    if (shift == 0 and seta == 0 and setb == 0 and carry == 0)
        return 1;

    // if no set bits are left for C and
    // requirement of set bits for A and B have exceeded
    if (shift == 0 or seta < 0 or setb < 0)
        return 0;

    // Find if the bit is 1 or 0 at
    // third index to the left
    int mask = shift & 1;

    int ans = 0;

    // carry = 1 and bit set = 1
    if ((mask) && carry) {

        // since carry is 1, and we need 1 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        ans += func(third + 1, seta, setb, 0, number)
                + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 1
    else if (mask && !carry) {

        // since carry is 0, and we need 1 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        ans += func(third + 1, seta - 1, setb, 0, number)
                + func(third + 1, seta, setb - 1, 0, number);
    }

    // carry = 1 and bit set = 0
    else if (!mask && carry) {

        // since carry is 1, and we need 0 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        ans += func(third + 1, seta - 1, setb, 1, number)
                  + func(third + 1, seta, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 0
    else if (!mask && !carry) {

        // since carry is 0, and we need 0 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        ans += func(third + 1, seta, setb, 0, number)
                  + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // Return ans
    return ans;
}

// Function to count ways
int possibleSwaps(int a, int b, int c)
{
    // Call func
    return func(0, a, b, 0, c);
}

// Driver Code
int main()
{

    int x = 2, y = 2, c = 20;

    cout << possibleSwaps(x, y, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

public class GFG{

// Recursive function to generate
// all combinations of bits
static int func(int third, int seta, int setb,
         int carry, int number)
{

    // find if C has no more set bits on left
    int shift = (number >> third);

    // if no set bits are left for C
    // and there are no set bits for A and B
    // and the carry is 0, then
    // this combination is possible
    if (shift == 0 && seta == 0 && setb == 0 && carry == 0)
        return 1;

    // if no set bits are left for C and
    // requirement of set bits for A and B have exceeded
    if (shift == 0 || seta < 0 || setb < 0)
        return 0;

    // Find if the bit is 1 or 0 at
    // third index to the left
    int mask = (shift & 1);

    int ans = 0;

    // carry = 1 and bit set = 1
    if ((mask) == 1 && carry == 1) {

        // since carry is 1, and we need 1 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        ans += func(third + 1, seta, setb, 0, number)
                + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 1
    else if (mask == 1 && carry == 0) {

        // since carry is 0, and we need 1 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        ans += func(third + 1, seta - 1, setb, 0, number)
                + func(third + 1, seta, setb - 1, 0, number);
    }

    // carry = 1 and bit set = 0
    else if (mask == 0 && carry == 1) {

        // since carry is 1, and we need 0 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        ans += func(third + 1, seta - 1, setb, 1, number)
                  + func(third + 1, seta, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 0
    else if (mask == 0 && carry == 0) {

        // since carry is 0, and we need 0 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        ans += func(third + 1, seta, setb, 0, number)
                  + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // Return ans
    return ans;
}

// Function to count ways
static int possibleSwaps(int a, int b, int c)
{
    // Call func
    return func(0, a, b, 0, c);
}

// Driver Code
public static void main(String args[])
{

    int x = 2, y = 2, c = 20;

    System.out.println(possibleSwaps(x, y, c));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# implementation of above approach
using System;
public class GFG {

  // Recursive function to generate
  // all combinations of bits
  static int func(int third, int seta, int setb,
                  int carry, int number)
  {

    // find if C has no more set bits on left
    int shift = (number >> third);

    // if no set bits are left for C
    // and there are no set bits for A and B
    // and the carry is 0, then
    // this combination is possible
    if (shift == 0 && seta == 0 && setb == 0 && carry == 0)
      return 1;

    // if no set bits are left for C and
    // requirement of set bits for A and B have exceeded
    if (shift == 0 || seta < 0 || setb < 0)
      return 0;

    // Find if the bit is 1 or 0 at
    // third index to the left
    int mask = (shift & 1);

    int ans = 0;

    // carry = 1 and bit set = 1
    if ((mask) == 1 && carry == 1) {

      // since carry is 1, and we need 1 at C's bit position
      // we can use 0 and 0
      // or 1 and 1 at A and B bit position
      ans += func(third + 1, seta, setb, 0, number) +
        func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 1
    else if (mask == 1 && carry == 0) {

      // since carry is 0, and we need 1 at C's bit position
      // we can use 1 and 0
      // or 0 and 1 at A and B bit position
      ans += func(third + 1, seta - 1, setb, 0, number) +
        func(third + 1, seta, setb - 1, 0, number);
    }

    // carry = 1 and bit set = 0
    else if (mask == 0 && carry == 1) {

      // since carry is 1, and we need 0 at C's bit position
      // we can use 1 and 0
      // or 0 and 1 at A and B bit position
      ans += func(third + 1, seta - 1, setb, 1, number) +
        func(third + 1, seta, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 0
    else if (mask == 0 && carry == 0) {

      // since carry is 0, and we need 0 at C's bit position
      // we can use 0 and 0
      // or 1 and 1 at A and B bit position
      ans += func(third + 1, seta, setb, 0, number) +
        func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // Return ans
    return ans;
  }

  // Function to count ways
  static int possibleSwaps(int a, int b, int c) {
    // Call func
    return func(0, a, b, 0, c);
  }

  // Driver Code
  public static void Main(String []args) {

    int x = 2, y = 2, c = 20;

    Console.WriteLine(possibleSwaps(x, y, c));
  }
}

// This code is contributed by umadevi9616
```

**Output**

```
3
```

**高效途径:**上述问题可以使用[位掩码 DP](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/) 解决。

1.  初始化大小为 *64 * 64 * 64 * 2* 的 **4-D** DP 数组，因为 10^18 最多有 64 个带-1 的设置位
2.  DP 数组的第一个状态存储 C 从右开始遍历的位数。第二个状态存储从 X 中使用的设置位的数量，第三个状态存储从 y 中使用的设置位的数量。第四个状态是进位位，它指的是我们执行加法操作时生成的进位。
3.  复发将有 4 种可能性。我们从最右边的比特位置开始。
4.  如果 C 的位位置是 1，那么在该索引处有四种可能得到 1。
    *   如果进位是 0，那么我们可以使用 X 中的 1 位和 Y 中的 0 位，反之亦然，这样就不会为下一步生成进位。
    *   如果进位是 1，那么我们可以使用来自每个的 1 个设置位，为下一步生成进位，否则我们使用来自 X 和 Y 的不生成进位的不设置位。
5.  如果 C 的位位置是 0，那么在该位位置有四种可能得到 0。
    *   如果进位是 1，那么我们可以使用 X 的 1 个置位位和 Y 的 0 个置位，反之亦然，这为下一步生成进位 1。
    *   如果进位是 0，那么我们可以分别使用 X 和 Y 中的 1 和 1，这为下一步生成进位 1。我们还可以使用无设置位，这不会为下一步生成进位。
6.  所有可能性的总和存储在 **dp【第三】【seta】【setb】【进位】**中，以避免再次访问相同的状态。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Initial DP array
int dp[64][64][64][2];

// Recursive function to generate
// all combinations of bits
int func(int third, int seta, int setb,
         int carry, int number)
{

    // if the state has already been visited
    if (dp[third][seta][setb][carry] != -1)
        return dp[third][seta][setb][carry];

    // find if C has no more set bits on left
    int shift = (number >> third);

    // if no set bits are left for C
    // and there are no set bits for A and B
    // and the carry is 0, then
    // this combination is possible
    if (shift == 0 and seta == 0 and setb == 0 and carry == 0)
        return 1;

    // if no set bits are left for C and
    // requirement of set bits for A and B have exceeded
    if (shift == 0 or seta < 0 or setb < 0)
        return 0;

    // Find if the bit is 1 or 0 at
    // third index to the left
    int mask = shift & 1;

    dp[third][seta][setb][carry] = 0;

    // carry = 1 and bit set = 1
    if ((mask) && carry) {

        // since carry is 1, and we need 1 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        dp[third][seta][setb][carry]
                += func(third + 1, seta, setb, 0, number)
                + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 1
    else if (mask && !carry) {

        // since carry is 0, and we need 1 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        dp[third][seta][setb][carry]
                += func(third + 1, seta - 1, setb, 0, number)
                + func(third + 1, seta, setb - 1, 0, number);
    }

    // carry = 1 and bit set = 0
    else if (!mask && carry) {

        // since carry is 1, and we need 0 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        dp[third][seta][setb][carry]
                  += func(third + 1, seta - 1, setb, 1, number)
                  + func(third + 1, seta, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 0
    else if (!mask && !carry) {

        // since carry is 0, and we need 0 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        dp[third][seta][setb][carry]
                  += func(third + 1, seta, setb, 0, number)
                  + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    return dp[third][seta][setb][carry];
}

// Function to count ways
int possibleSwaps(int a, int b, int c)
{

    memset(dp, -1, sizeof(dp));

    // function call that returns the
    // answer
    int ans = func(0, a, b, 0, c);

    return ans;
}

// Driver Code
int main()
{

    int x = 2, y = 2, c = 20;

    cout << possibleSwaps(x, y, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GfG {

// Initial DP array
static int dp[][][][] = new int[64][64][64][2];

// Recursive function to generate
// all combinations of bits
static int func(int third, int seta, int setb,
                int carry, int number)
{

    // if the state has already been visited
    if (dp[third][seta][setb][carry] != -1)
        return dp[third][seta][setb][carry];

    // find if C has no more set bits on left
    int shift = (number >> third);

    // if no set bits are left for C
    // and there are no set bits for A and B
    // and the carry is 0, then
    // this combination is possible
    if (shift == 0 && seta == 0 && setb == 0 && carry == 0)
        return 1;

    // if no set bits are left for C and
    // requirement of set bits for A and B have exceeded
    if (shift == 0 || seta < 0 || setb < 0)
        return 0;

    // Find if the bit is 1 or 0 at
    // third index to the left
    int mask = shift & 1;

    dp[third][seta][setb][carry] = 0;

    // carry = 1 and bit set = 1
    if ((mask == 1) && carry == 1) {

        // since carry is 1, and we need 1 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        dp[third][seta][setb][carry]
                            += func(third + 1, seta, setb, 0, number)
                            + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 1
    else if (mask == 1 && carry == 0) {

        // since carry is 0, and we need 1 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        dp[third][seta][setb][carry]
                                    += func(third + 1, seta - 1, setb, 0, number)
                                    + func(third + 1, seta, setb - 1, 0, number);
    }

    // carry = 1 and bit set = 0
    else if (mask == 0 && carry == 1) {

        // since carry is 1, and we need 0 at C's bit position
        // we can use 1 and 0
        // or 0 and 1 at A and B bit position
        dp[third][seta][setb][carry] += func(third + 1, seta - 1, setb, 1, number)
                                    + func(third + 1, seta, setb - 1, 1, number);
    }

    // carry = 0 and bit set = 0
    else if (mask == 0 && carry == 0) {

        // since carry is 0, and we need 0 at C's bit position
        // we can use 0 and 0
        // or 1 and 1 at A and B bit position
        dp[third][seta][setb][carry] += func(third + 1, seta, setb, 0, number)
                                    + func(third + 1, seta - 1, setb - 1, 1, number);
    }

    return dp[third][seta][setb][carry];
}

// Function to count ways
static int possibleSwaps(int a, int b, int c)
{
    for(int q = 0; q < 64; q++)
    {
        for(int r = 0; r < 64; r++)
        {
            for(int p = 0; p < 64; p++)
            {
                for(int d = 0; d < 2; d++)
                {
                    dp[q][r][p][d] = -1;
                }
            }
        }
    }

    // function call that returns the
    // answer
    int ans = func(0, a, b, 0, c);

    return ans;
}

// Driver Code
public static void main(String[] args)
{

    int x = 2, y = 2, c = 20;

    System.out.println(possibleSwaps(x, y, c));
}
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Initial DP array
dp = [[[[-1, -1] for i in range(64)]
                 for j in range(64)]
                 for k in range(64)]

# Recursive function to generate
# all combinations of bits
def func(third, seta, setb, carry, number):

    # if the state has already been visited
    if dp[third][seta][setb][carry] != -1:
        return dp[third][seta][setb][carry]

    # find if C has no more set bits on left
    shift = number >> third

    # if no set bits are left for C
    # and there are no set bits for A and B
    # and the carry is 0, then
    # this combination is possible
    if (shift == 0 and seta == 0 and
        setb == 0 and carry == 0):
        return 1

    # if no set bits are left for C and
    # requirement of set bits for A and B have exceeded
    if (shift == 0 or seta < 0 or setb < 0):
        return 0

    # Find if the bit is 1 or 0 at
    # third index to the left
    mask = shift & 1

    dp[third][seta][setb][carry] = 0

    # carry = 1 and bit set = 1
    if (mask) and carry:

        # since carry is 1, and we need 1 at
        # C's bit position we can use 0 and 0
        # or 1 and 1 at A and B bit position
        dp[third][seta][setb][carry] +=\
                func(third + 1, seta, setb, 0, number) + \
                func(third + 1, seta - 1, setb - 1, 1, number)

    # carry = 0 and bit set = 1
    elif mask and not carry:

        # since carry is 0, and we need 1 at C's
        # bit position we can use 1 and 0
        # or 0 and 1 at A and B bit position
        dp[third][seta][setb][carry] +=\
                func(third + 1, seta - 1, setb, 0, number) + \
                func(third + 1, seta, setb - 1, 0, number)

    # carry = 1 and bit set = 0
    elif not mask and carry:

        # since carry is 1, and we need 0 at C's
        # bit position we can use 1 and 0
        # or 0 and 1 at A and B bit position
        dp[third][seta][setb][carry] +=\
                func(third + 1, seta - 1, setb, 1, number) + \
                func(third + 1, seta, setb - 1, 1, number)

    # carry = 0 and bit set = 0
    elif not mask and not carry:

        # since carry is 0, and we need 0 at C's
        # bit position we can use 0 and 0
        # or 1 and 1 at A and B bit position
        dp[third][seta][setb][carry] += \
                func(third + 1, seta, setb, 0, number) + \
                func(third + 1, seta - 1, setb - 1, 1, number)

    return dp[third][seta][setb][carry]

# Function to count ways
def possibleSwaps(a, b, c):

    # function call that returns the answer
    ans = func(0, a, b, 0, c)
    return ans

# Driver Code
if __name__ == "__main__":

    x, y, c = 2, 2, 20
    print(possibleSwaps(x, y, c))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Initial DP array
static int [,,,]dp = new int[64, 64, 64, 2];

// Recursive function to generate
// all combinations of bits
static int func(int third, int seta, int setb,
                int carry, int number)
{

    // if the state has already been visited
    if (third > -1 && seta > -1 &&
         setb > -1 && carry > -1)
        if(dp[third, seta, setb, carry] != -1)
            return dp[third, seta, setb, carry];

    // find if C has no more set bits on left
    int shift = (number >> third);

    // if no set bits are left for C
    // and there are no set bits for A and B
    // and the carry is 0, then
    // this combination is possible
    if (shift == 0 && seta == 0 && 
         setb == 0 && carry == 0)
        return 1;

    // if no set bits are left for C and
    // requirement of set bits for A and
    // B have exceeded
    if (shift == 0 || seta < 0 || setb < 0)
        return 0;

    // Find if the bit is 1 or 0 at
    // third index to the left
    int mask = shift & 1;

    dp[third, seta, setb, carry] = 0;

    // carry = 1 and bit set = 1
    if ((mask == 1) && carry == 1)
    {

        // since carry is 1, and we need 1 at
        // C's bit position, we can use 0 and 0
        // or 1 and 1 at A and B bit position
        dp[third, seta,
           setb, carry] += func(third + 1, seta,
                                setb, 0, number) +
                           func(third + 1, seta - 1,
                                setb - 1, 1, number);
    }

    // carry = 0 and bit set = 1
    else if (mask == 1 && carry == 0)
    {

        // since carry is 0, and we need 1 at
        // C's bit position, we can use 1 and 0
        // or 0 and 1 at A and B bit position
        dp[third, seta,
           setb, carry] += func(third + 1, seta - 1,
                                  setb, 0, number) +
                           func(third + 1, seta,
                                setb - 1, 0, number);
    }

    // carry = 1 and bit set = 0
    else if (mask == 0 && carry == 1)
    {

        // since carry is 1, and we need 0 at
        // C's bit position, we can use 1 and 0
        // or 0 and 1 at A and B bit position
        dp[third, seta,
           setb, carry] += func(third + 1, seta - 1,
                                setb, 1, number) +
                           func(third + 1, seta,
                                setb - 1, 1, number);
    }

    // carry = 0 and bit set = 0
    else if (mask == 0 && carry == 0)
    {

        // since carry is 0, and we need 0 at
        // C's bit position, we can use 0 and 0
        // or 1 and 1 at A and B bit position
        dp[third, seta,
           setb, carry] += func(third + 1, seta,
                                setb, 0, number) +
                           func(third + 1, seta - 1,
                                setb - 1, 1, number);
    }
    return dp[third, seta, setb, carry];
}

// Function to count ways
static int possibleSwaps(int a, int b, int c)
{
    for(int q = 0; q < 64; q++)
    {
        for(int r = 0; r < 64; r++)
        {
            for(int p = 0; p < 64; p++)
            {
                for(int d = 0; d < 2; d++)
                {
                    dp[q, r, p, d] = -1;
                }
            }
        }
    }

    // function call that returns the
    // answer
    int ans = func(0, a, b, 0, c);

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int x = 2, y = 2, c = 20;

    Console.WriteLine(possibleSwaps(x, y, c));
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
3
```