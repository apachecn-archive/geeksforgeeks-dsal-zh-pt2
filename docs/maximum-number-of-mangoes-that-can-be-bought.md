# 可以购买的芒果最大数量

> 原文:[https://www . geesforgeks . org/最大可购买芒果数量/](https://www.geeksforgeeks.org/maximum-number-of-mangoes-that-can-be-bought/)

给定两个整数 **W** 和 **C** ，代表西瓜和硬币的数量，任务是在每个芒果花费 **1** 西瓜和 **X** 硬币和 **y** 硬币可以卖一个西瓜的情况下，找到可以购买的最大芒果数量。

**示例:**

> **输入:** W = 10，C = 10，X = 1，Y = 1
> **输出:** 10
> **说明:**最理想的方式是用 10 个西瓜和 10 个硬币买 10 个芒果。因此，可以购买的最大芒果数量是 10 个。
> 
> **输入:** W = 4，C = 8，X = 4，Y = 4
> **输出:** 3
> **说明:**最优的方式是卖一个西瓜。然后，硬币的数量增加 4 枚。因此，硬币总数变成了 12 枚。因此，3 个西瓜和 12 个硬币可以用来买 3 个芒果。因此，可以购买的芒果的最大数量是 3 个。

**进场:**这个问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。这个想法是在搜索空间中找到芒果的最大数量。按照以下步骤解决问题:

*   将变量**和**初始化为 **0** ，以存储所需的结果。
*   将两个变量 **l** 初始化为 **0** ， **r** 初始化为 **W** ，以存储[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的搜索空间的边界区域。
*   [在](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **l≤r** 时循环，并执行以下步骤:
    *   将中间值存储在变量**中间**中，作为 **(l+r)/2** 。
    *   检查**中间**个芒果是否可以用 **W** 、 **C** 、 **x** 和 **y** 的给定值购买。
    *   如果为真，则将 **ans** 更新为 **mid** ，通过将 **l** 更新为 **mid+1** 来搜索 **mid** 的右边部分。否则，将 **r** 的值更新为**中间 1** 。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if mid number
// of mangoes can be bought
bool check(int n, int m, int x, int y, int vl)
{
    // Store the coins
    int temp = m;

    // If watermelons needed are greater
    // than given watermelons
    if (vl > n)
        return false;

    // Store remaining watermelons if vl
    // watermelons are used to buy mangoes
    int ex = n - vl;

    // Store the value of coins if these
    // watermelon get sold
    ex *= y;

    // Increment coins by ex
    temp += ex;

    // Number of mangoes that can be buyed
    // if only x coins needed for one mango
    int cr = temp / x;

    // If the condition is satisfied,
    // return true
    if (cr >= vl)
        return true;

    // Otherwise return false
    return false;
}

// Function to find the maximum number of mangoes
// that can be bought by selling watermelons
int maximizeMangoes(int n, int m, int x, int y)
{
    // Initialize the boundary values
    int l = 0, r = n;

    // Store the required result
    int ans = 0;

    // Binary Search
    while (l <= r) {

        // Store the mid value
        int mid = l + (r - l) / 2;

        // Check if it is possible to
        // buy mid number of mangoes
        if (check(n, m, x, y, mid)) {
            ans = mid;
            l = mid + 1;
        }

        // Otherwise, update r to mid -1
        else
            r = mid - 1;
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int W = 4, C = 8, x = 4, y = 4;

    // Function Call
    cout << maximizeMangoes(W, C, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if mid number
// of mangoes can be bought
static boolean check(int n, int m, int x,
                     int y, int vl)
{

    // Store the coins
    int temp = m;

    // If watermelons needed are greater
    // than given watermelons
    if (vl > n)
        return false;

    // Store remaining watermelons if vl
    // watermelons are used to buy mangoes
    int ex = n - vl;

    // Store the value of coins if these
    // watermelon get sold
    ex *= y;

    // Increment coins by ex
    temp += ex;

    // Number of mangoes that can be buyed
    // if only x coins needed for one mango
    int cr = temp / x;

    // If the condition is satisfied,
    // return true
    if (cr >= vl)
        return true;

    // Otherwise return false
    return false;
}

// Function to find the maximum number
// of mangoes that can be bought by
// selling watermelons
static int maximizeMangoes(int n, int m,
                           int x, int y)
{

    // Initialize the boundary values
    int l = 0, r = n;

    // Store the required result
    int ans = 0;

    // Binary Search
    while (l <= r)
    {

        // Store the mid value
        int mid = l + (r - l) / 2;

        // Check if it is possible to
        // buy mid number of mangoes
        if (check(n, m, x, y, mid))
        {
            ans = mid;
            l = mid + 1;
        }

        // Otherwise, update r to mid -1
        else
            r = mid - 1;
    }

    // Return the result
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int W = 4, C = 8, x = 4, y = 4;

    // Function Call
    System.out.println(maximizeMangoes(W, C, x, y));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if mid number
# of mangoes can be bought
def check(n, m, x, y, vl):

    # Store the coins
    temp = m

    # If watermelons needed are greater
    # than given watermelons
    if (vl > n):
        return False

    # Store remaining watermelons if vl
    # watermelons are used to buy mangoes
    ex = n - vl

    # Store the value of coins if these
    # watermelon get sold
    ex *= y

    # Increment coins by ex
    temp += ex

    # Number of mangoes that can be buyed
    # if only x coins needed for one mango
    cr = temp // x

    # If the condition is satisfied,
    # return true
    if (cr >= vl):
        return True

    # Otherwise return false
    return False

# Function to find the maximum number of mangoes
# that can be bought by selling watermelons
def maximizeMangoes(n, m, x, y):

    # Initialize the boundary values
    l = 0
    r = n

    # Store the required result
    ans = 0

    # Binary Search
    while (l <= r):

        # Store the mid value
        mid = l + (r - l) // 2

        # Check if it is possible to
        # buy mid number of mangoes
        if (check(n, m, x, y, mid)):
            ans = mid
            l = mid + 1

        # Otherwise, update r to mid -1
        else:
            r = mid - 1

    # Return the result
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    W = 4
    C = 8
    x = 4
    y = 4

    # Function Call
    print(maximizeMangoes(W, C, x, y))

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if mid number
// of mangoes can be bought
static bool check(int n, int m, int x,
                  int y, int vl)
{

    // Store the coins
    int temp = m;

    // If watermelons needed are greater
    // than given watermelons
    if (vl > n)
        return false;

    // Store remaining watermelons if vl
    // watermelons are used to buy mangoes
    int ex = n - vl;

    // Store the value of coins if these
    // watermelon get sold
    ex *= y;

    // Increment coins by ex
    temp += ex;

    // Number of mangoes that can be buyed
    // if only x coins needed for one mango
    int cr = temp / x;

    // If the condition is satisfied,
    // return true
    if (cr >= vl)
        return true;

    // Otherwise return false
    return false;
}

// Function to find the maximum number of mangoes
// that can be bought by selling watermelons
static int maximizeMangoes(int n, int m, int x, int y)
{

    // Initialize the boundary values
    int l = 0, r = n;

    // Store the required result
    int ans = 0;

    // Binary Search
    while (l <= r)
    {

        // Store the mid value
        int mid = l + (r - l) / 2;

        // Check if it is possible to
        // buy mid number of mangoes
        if (check(n, m, x, y, mid))
        {
            ans = mid;
            l = mid + 1;
        }

        // Otherwise, update r to mid -1
        else
            r = mid - 1;
    }

    // Return the result
    return ans;
}

// Driver Code
public static void Main()
{

    // Given Input
    int W = 4, C = 8, x = 4, y = 4;

    // Function Call
    Console.Write(maximizeMangoes(W, C, x, y));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if mid number
// of mangoes can be bought
function check(n, m,  x, y,vl)
{
    // Store the coins
    var temp = m;

    // If watermelons needed are greater
    // than given watermelons
    if (vl > n)
        return false;

    // Store remaining watermelons if vl
    // watermelons are used to buy mangoes
    var ex = n - vl;

    // Store the value of coins if these
    // watermelon get sold
    ex *= y;

    // Increment coins by ex
    temp += ex;

    // Number of mangoes that can be buyed
    // if only x coins needed for one mango
    var cr = parseInt(temp / x);

    // If the condition is satisfied,
    // return true
    if (cr >= vl)
        return true;

    // Otherwise return false
    return false;
}

// Function to find the maximum number of mangoes
// that can be bought by selling watermelons
function maximizeMangoes(n, m, x, y)
{
    // Initialize the boundary values
    var l = 0, r = n;

    // Store the required result
    var ans = 0;

    // Binary Search
    while (l <= r) {

        // Store the mid value
        var mid = l + parseInt((r - l) / 2);

        // Check if it is possible to
        // buy mid number of mangoes
        if (check(n, m, x, y, mid)) {
            ans = mid;
            l = mid + 1;
        }

        // Otherwise, update r to mid -1
        else
            r = mid - 1;
    }

    // Return the result
    return ans;
}
var W = 4, C = 8, x = 4, y = 4;

// Function Call
document.write( maximizeMangoes(W, C, x, y));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(log(W))*
***辅助空间:** O(1)*