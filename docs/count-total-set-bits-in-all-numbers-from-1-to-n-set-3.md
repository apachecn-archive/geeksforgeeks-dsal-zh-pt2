# 从 1 到 N 对所有数字中的总设定位进行计数|设定 3

> 原文:[https://www . geesforgeks . org/count-total-set-bit-in-all-numbers-from-1-n-set-3/](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n-set-3/)

给定一个正整数 **N** ，任务是计算从 **1** 到 **N** 的所有数字的二进制表示中的设置位总数。

**示例:**

> **输入:** N = 3
> **输出:**4
> set bits(1)+set bits(2)+set bits(3)= 1+1+2 = 4
> 
> **输入:**N = 6
> T3】输出: 9

**方法:**这个问题的解决方案已经发表在本文的[集 1](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n/) 和[集 2](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n-set-2/) 中。这里，讨论了基于动态规划的方法。

*   **基本情况:**0 中的设置位数为 0。
*   对于任何数字 n: n 和 n>>1，除了最右边的位之外，都有相同数量的设置位。

例如:n = 11 ( **101** 1)、n>>1 = 5(**101**)……11 和 5 中的相同位标为粗体。因此，假设我们已经知道设置位计数为 5，我们只需要注意最右边的位 11，即 1。setBit(11) = setBit(5) + 1 = 2 + 1 = 3

最右边的位对于奇数是 1，对于偶数是 0。

**递归关系:**set bit(n)= set bit(n>>1)+(n&1)和 setBit(0) = 0

我们可以使用自下而上的动态规划方法来解决这个问题。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// set bits in all the integers
// from the range [1, n]
int countSetBits(int n)
{

    // To store the required count
    // of the set bits
    int cnt = 0;

    // To store the count of set
    // bits in every integer
    vector<int> setBits(n + 1);

    // 0 has no set bit
    setBits[0] = 0;

    for (int i = 1; i <= n; i++) {

        setBits[i] = setBits[i >> 1] + (i & 1);
    }

    // Sum all the set bits
    for (int i = 0; i <= n; i++) {
        cnt = cnt + setBits[i];
    }

    return cnt;
}

// Driver code
int main()
{
    int n = 6;

    cout << countSetBits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of
// set bits in all the integers
// from the range [1, n]
static int countSetBits(int n)
{

    // To store the required count
    // of the set bits
    int cnt = 0;

    // To store the count of set
    // bits in every integer
    int []setBits = new int[n + 1];

    // 0 has no set bit
    setBits[0] = 0;

    // For the rest of the elements
    for (int i = 1; i <= n; i++) {

        setBits[i] = setBits[i >> 1] + (i & 1);
    }

    // Sum all the set bits
    for (int i = 0; i <= n; i++)
    {
        cnt = cnt + setBits[i];
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int n = 6;

    System.out.println(countSetBits(n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# set bits in all the integers
# from the range [1, n]
def countSetBits(n):

    # To store the required count
    # of the set bits
    cnt = 0

    # To store the count of set
    # bits in every integer
    setBits = [0 for x in range(n + 1)]

    # 0 has no set bit
    setBits[0] = 0

    # For the rest of the elements
    for i in range(1, n + 1):
        setBits[i] = setBits[i // 2] + (i & 1)

    # Sum all the set bits
    for i in range(0, n + 1):
        cnt = cnt + setBits[i]

    return cnt

# Driver code
n = 6
print(countSetBits(n))

# This code is contributed by Sanjit Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of
    // set bits in all the integers
    // from the range [1, n]
    static int countSetBits(int n)
    {

        // To store the required count
        // of the set bits
        int cnt = 0;

        // To store the count of set
        // bits in every integer
        int []setBits = new int[n + 1];

        // 0 has no set bit
        setBits[0] = 0;

        // 1 has a single set bit
        setBits[1] = 1;

        // For the rest of the elements
        for (int i = 2; i <= n; i++)
        {

            // If current element i is even then
            // it has set bits equal to the count
            // of the set bits in i / 2
            if (i % 2 == 0)
            {
                setBits[i] = setBits[i / 2];
            }

            // Else it has set bits equal to one
            // more than the previous element
            else
            {
                setBits[i] = setBits[i - 1] + 1;
            }
        }

        // Sum all the set bits
        for (int i = 0; i <= n; i++)
        {
            cnt = cnt + setBits[i];
        }
        return cnt;
    }

    // Driver code
    static public void Main ()
    {
        int n = 6;

        Console.WriteLine(countSetBits(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// set bits in all the integers
// from the range [1, n]
function countSetBits(n)
{

    // To store the required count
    // of the set bits
    var cnt = 0;

    // To store the count of set
    // bits in every integer
    var setBits = Array.from(
        {length: n + 1}, (_, i) => 0);

    // 0 has no set bit
    setBits[0] = 0;

    // 1 has a single set bit
    setBits[1] = 1;

    // For the rest of the elements
    for(i = 2; i <= n; i++)
    {

        // If current element i is even then
        // it has set bits equal to the count
        // of the set bits in i / 2
        if (i % 2 == 0)
        {
            setBits[i] = setBits[i / 2];
        }

        // Else it has set bits equal to one
        // more than the previous element
        else
        {
            setBits[i] = setBits[i - 1] + 1;
        }
    }

    // Sum all the set bits
    for(i = 0; i <= n; i++)
    {
        cnt = cnt + setBits[i];
    }
    return cnt;
}

// Driver code
var n = 6;

document.write(countSetBits(n));

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
9
```

**另一个简单易懂的解决方案:**

一个简单易于实现和理解的解决方案是不使用位操作。解决方案是使用 __builtin_popcount()直接对设置位进行计数。使用注释在代码中解释了解决方案。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// set bits in all the integers
// from the range [1, n]
int countSetBits(int n)
{

    // To store the required count
    // of the set bits
    int cnt = 0;

    // Calculate set bits in each number using
    // __builtin_popcount() and  Sum all the set bits
    for (int i = 1; i <= n; i++) {
        cnt = cnt + __builtin_popcount(i);
    }

    return cnt;
}

// Driver code
int main()
{
    int n = 6;

    cout << countSetBits(n);

    return 0;
}

// This article is contributed by Abhishek
```

**Output**

```
9
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。