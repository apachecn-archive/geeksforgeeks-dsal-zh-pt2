# 计数 1 到 N 的三元组，使得中间元素总是最大的

> 原文:[https://www . geeksforgeeks . org/count-of-triplets-of-numbers-1-to-n-so-middle-element-every-big/](https://www.geeksforgeeks.org/count-of-triplets-of-numbers-1-to-n-such-that-middle-element-is-always-largest/)

给定一个整数 **N** ，任务是计算在**【1，N】**内排列三元组( **a** 、 **b** 、 **c** )的方式数，使得中间元素总是大于左右元素。

> **示例:**
> **输入:** N = 4
> **输出:** 8
> **解释**
> 对于给定的输入 N = 4 可能的三元组的数量为:{1，3，2}、{2，3，1}、{2，4，3}、{3，4，2}、{1，4，3}、{3，4，1}、{2，4，1}、{1，4，2}。
> **输入:** 10
> **输出:** 240

**天真方法:**使用三个嵌套循环检查所有三元组是否满足给定条件，并在每次三元组满足条件时不断增加它们的计数。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O( 1 )*
**高效进场:**

1.  检查中间元素的所有可能性，并尝试找到可能排列的数量，保持它们一个接一个地固定。
2.  我们可以观察到**【3，N】**之间的所有数字都可以占据中间的槽位。

> 每个中间元素的可能排列:
> 将 3 放在中间时，只存在 2 ( = 2 * 1)个可能的排列{1，3，2}和{2，3，1}。
> 将 4 放在中间时，存在 6 ( = 3 * 2)种可能的排列方式{1，4，3}、{1，4，2}、{2，4，1}、{2，4，3}、{3，4，1}和{3，4，2}。
> 将 5 放在中间时，存在 12 ( = 4 * 3)种可能的排列。
> 。
> 。
> 。
> 在中间放置 N-1 时，(N-2) * (N-3)存在可能的排列。
> 在中间放置 N 时，(N-1) * (N-2)存在可能的排列。
> 因此，总的可能排列=**(N *(N-1)*(N-2))/3**

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find Number of triplets
// for given Number N such that
// middle element is always greater
// than left and right side element.
int findArrangement(int N)
{
    // check if arrangement is
    // possible or Not
    if (N < 3)
        return 0;

    // else return total ways
    return ((N) * (N - 1) * (N - 2)) / 3;
}

// Driver code.
int main()
{
    int N = 10;
    cout << findArrangement(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find number of triplets
// for given number N such that middle
// element is always greater than left 
// and right side element.
static int findArrangement(int N)
{

    // Check if arrangement
    // is possible or not
    if (N < 3)
        return 0;

    // Else return total ways
    return ((N) * (N - 1) * (N - 2)) / 3;
}

// Driver code
public static void main(String[] args)
{
    int N = 10;

    System.out.println(findArrangement(N));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find Number of triplets
# for given Number N such that middle
# element is always greater than left 
# and right side element.
def findArrangement(N):

    # Check if arrangement is
    # possible or Not
    if (N < 3):
        return 0;

    # Else return total ways
    return ((N) * (N - 1) * (N - 2)) // 3;

# Driver code.
N = 10;

print(findArrangement(N));

# This code is contributed by Akanksha_Rai
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find number of triplets
// for given number N such that middle
// element is always greater than left
// and right side element.
static int findArrangement(int N)
{

    // Check if arrangement
    // is possible or not
    if (N < 3)
        return 0;

    // Else return total ways
    return ((N) * (N - 1) * (N - 2)) / 3;
}

// Driver code
public static void Main()
{
    int N = 10;

    Console.Write(findArrangement(N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find number of triplets
// for given number N such that middle
// element is always greater than left 
// and right side element.
function findArrangement(N)
{

    // Check if arrangement
    // is possible or not
    if (N < 3)
        return 0;

    // Else return total ways
    return ((N) * (N - 1) * (N - 2)) / 3;
}

  // Driver Code
    let N = 10;
   document.write(findArrangement(N));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
240
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*