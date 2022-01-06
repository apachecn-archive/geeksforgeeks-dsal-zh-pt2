# 最大化保留至少一件黑色和一件白色衬衫所需的箱子

> 原文:[https://www . geesforgeks . org/maximize-box-需要保留至少一件黑白衬衫/](https://www.geeksforgeeks.org/maximize-boxes-required-to-keep-at-least-one-black-and-one-white-shirt/)

给定三个数字 **W** 、 **B** 和 **O** 分别代表白色、黑色和其他颜色衬衫的数量，任务是找到所需的最大盒子数量，使得每个盒子包含三件衬衫，这三件衬衫由使用给定数量衬衫的至少一件白色和黑色衬衫组成。

**示例:**

> **输入:** W = 3，B = 3，O = 1
> **输出:** 2
> **说明:**
> 下面是各个盒子里衬衫的分布:
> **盒子 1:** 白衬衫 1 件，黑衬衫 1 件，其他颜色衬衫 1 件。
> **第 2 格:**白衬衫 2 件，黑衬衫 1 件。
> **第 3 盒:** 1 件黑色衬衫
> 由于只有 2 盒满足给定条件，即给定数量衬衫的最大可能盒数。因此，打印 2。
> 
> **输入:** W = 4，B = 6，O = 0
> T3】输出: 3

**方法:**给定的问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。其思想是在由[下限和上限](https://www.geeksforgeeks.org/lower-and-upper-bound-theory/)形成的搜索空间中搜索最大数量的盒子。可以观察到箱数的[下界](https://www.geeksforgeeks.org/lower_bound-in-cpp/)和[上界](https://www.geeksforgeeks.org/upper_bound-in-cpp/)分别为 **0** 和最小的 **W** 和 **B** 。按照以下步骤解决问题:

*   初始化一个变量，说**和**为 **0** 来存储需要的结果。
*   初始化两个变量，说**低**为 **0** ，说**高**为 **(W，B)** 的[最小值。](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)
*   [循环直到](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)的值**低**小于**高**并执行以下步骤:
    *   在一个变量中找到**低**和**高**的中间值，说**中**。
    *   检查最大框数是否可以等于**中的**，然后将 **ans** 的值更新为**中的**，通过更新**低的**的值来更新右半部分的搜索空间。
    *   否则，通过更新**高值**将搜索空间更新到左半部分。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of boxes such that each box contains
// three shirts comprising of at least
// one white and black shirt
void numberofBoxes(int W, int B, int O)
{
    // Stores the low and high pointers
    // for binary search
    int low = 0, high = min(W, B);

    // Store the required answer
    int ans = 0;

    // Loop while low <= high
    while (low <= high) {

        // Store the mid value
        int mid = low + (high - low) / 2;

        // Check if the mid number of
        // boxes can be used
        if (((W >= mid) and (B >= mid))
            and ((W - mid) + (B - mid) + O)
                    >= mid) {

            // Update answer and recur
            // for the right half
            ans = mid;
            low = mid + 1;
        }

        // Else, recur for the left half
        else
            high = mid - 1;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int W = 3, B = 3, O = 1;
    numberofBoxes(W, B, O);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum number
// of boxes such that each box contains
// three shirts comprising of at least
// one white and black shirt
static void numberofBoxes(int W, int B, int O)
{

    // Stores the low and high pointers
    // for binary search
    int low = 0, high = Math.min(W, B);

    // Store the required answer
    int ans = 0;

    // Loop while low <= high
    while (low <= high)
    {

        // Store the mid value
        int mid = low + (high - low) / 2;

        // Check if the mid number of
        // boxes can be used
        if (((W >= mid) && (B >= mid)) &&
            ((W - mid) + (B - mid) + O) >= mid)
        {

            // Update answer and recur
            // for the right half
            ans = mid;
            low = mid + 1;
        }

        // Else, recur for the left half
        else
            high = mid - 1;
    }

    // Print the result
    System.out.println(ans);
}

// Driver Code
public static void main(String args[])
{
    int W = 3, B = 3, O = 1;

    numberofBoxes(W, B, O);
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number
# of boxes such that each box contains
# three shirts comprising of at least
# one white and black shirt
def numberofBoxes(W, B, O):

    # Stores the low and high pointers
    # for binary search
    low = 0
    high = min(W, B)

    # Store the required answer
    ans = 0

    # Loop while low <= high
    while (low <= high):

        # Store the mid value
        mid = low + (high - low) // 2

        # Check if the mid number of
        # boxes can be used
        if (((W >= mid) and (B >= mid)) and ((W - mid) + (B - mid) + O) >= mid):
            # Update answer and recur
            # for the right half
            ans = mid
            low = mid + 1

        # Else, recur for the left half
        else:
            high = mid - 1

    # Print result
    print (ans)

# Driver Code
if __name__ == '__main__':
    W = 3
    B = 3
    O = 1
    numberofBoxes(W, B, O)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach

using System;
class GFG {

    // Function to find the maximum number
    // of boxes such that each box contains
    // three shirts comprising of at least
    // one white and black shirt
    static void numberofBoxes(int W, int B, int O)
    {
        // Stores the low and high pointers
        // for binary search
        int low = 0, high = Math.Min(W, B);

        // Store the required answer
        int ans = 0;

        // Loop while low <= high
        while (low <= high) {

            // Store the mid value
            int mid = low + (high - low) / 2;

            // Check if the mid number of
            // boxes can be used
            if (((W >= mid) &&(B >= mid))
                    &&((W - mid) + (B - mid) + O)
                >= mid) {

                // Update answer and recur
                // for the right half
                ans = mid;
                low = mid + 1;
            }

            // Else, recur for the left half
            else
                high = mid - 1;
        }

        // Print the result
        Console.Write(ans);
    }

    // Driver Code
    public static void Main()
    {
        int W = 3, B = 3, O = 1;
        numberofBoxes(W, B, O);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum number
// of boxes such that each box contains
// three shirts comprising of at least
// one white and black shirt
function numberofBoxes(W, B, O)
{

    // Stores the low and high pointers
    // for binary search
    let low = 0, high = Math.min(W, B);

    // Store the required answer
    let ans = 0;

    // Loop while low <= high
    while (low <= high)
    {

        // Store the mid value
        let mid = low + Math.floor((high - low) / 2);

        // Check if the mid number of
        // boxes can be used
        if (((W >= mid) && (B >= mid)) &&
            ((W - mid) + (B - mid) + O) >= mid)
        {

            // Update answer and recur
            // for the right half
            ans = mid;
            low = mid + 1;
        }

        // Else, recur for the left half
        else
            high = mid - 1;
    }

    // Print the result
    document.write(ans);
}

// Driver Code
let W = 3, B = 3, O = 1;
numberofBoxes(W, B, O);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log(min(W，B))*
***辅助空间:** O(1)*