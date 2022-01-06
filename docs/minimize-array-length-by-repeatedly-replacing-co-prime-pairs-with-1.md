# 通过用 1 重复替换同素对来最小化数组长度

> 原文:[https://www . geesforgeks . org/通过用-1 替换-co-prime-pairs 来最小化数组长度/](https://www.geeksforgeeks.org/minimize-array-length-by-repeatedly-replacing-co-prime-pairs-with-1/)

给定一个由 **N** 元素组成的数组**arr【】**，任务是通过用 **1** 替换任意两个[互质](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)数组元素来最小化数组长度。
**示例:**

> **输入:** arr[] = {2，3，5}
> **输出:** 1
> **解释:**
> 将{2，3}替换为 1 将数组修改为{1，5}。
> 将{1，5}替换为 1 会将数组修改为{1}。
> **输入:** arr[] = {6，9，15}
> **输出:** 3
> **说明:**数组中不存在互质对。因此，不可能减少。

**天真方法:**最简单的方法是迭代数组并检查互素对。如果找到了，替换为搜索下一个互质对，以此类推。

***时间复杂度:**O(N<sup>3</sup>* log**N)*** *****辅助空间:** O(1)*** 

****高效方法:**该方法基于以下事实:**

> **1 是每个数字的互质**

**这个想法是找出数组中是否存在**任何共质数对**。如果找到了，那么所有的数组元素都可以根据上面的事实减少到 1。因此，如果找到任何同素对，那么，所需的答案将是 1，否则，答案将是数组的初始大小。**

> ****说明:**
> For arr[] = {2，4，6，8，9}
> 这里，由于存在互质对{2，9}，将它们替换为 1 会将数组修改为{1，4，6，8}。
> 由于 1 与每个数字是互质的，因此可以通过以下步骤进一步减少数组:
> {1，4，6，8} - > {1，6，8} - > {1，8} - > {1}
> 因此，数组可以减少到大小 1。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the final array
// length by replacing coprime pair with 1
bool hasCoprimePair(vector<int>& arr, int n)
{

    // Iterate over all pairs of element
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Check if gcd is 1
            if (__gcd(arr[i], arr[j]) == 1) {
                return true;
            }
        }
    }

    // If no coprime pair
    // found return false
    return false;
}

// Driver code
int main()
{

    int n = 3;
    vector<int> arr = { 6, 9, 15 };

    // Check if atleast one coprime
    // pair exists in the array
    if (hasCoprimePair(arr, n)) {
        cout << 1 << endl;
    }

    // If no such pair exists
    else {
        cout << n << endl;
    }
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program for the above approach
import java.util.*;
class GFG{

// Recursive function to return
// gcd of a and b 
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Function to find the final array
// length by replacing coprime pair with 1
static boolean hasCoprimePair(int []arr, int n)
{

    // Iterate over all pairs of element
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Check if gcd is 1
            if ((__gcd(arr[i], arr[j])) == 1)
            {
                return true;
            }
        }
    }

    // If no coprime pair
    // found return false
    return false;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    int []arr = { 6, 9, 15 };

    // Check if atleast one coprime
    // pair exists in the array
    if (hasCoprimePair(arr, n))
    {
        System.out.print(1 + "\n");
    }

    // If no such pair exists
    else
    {
        System.out.print(n + "\n");
    }
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 program for the above approach
import math

# Function to find the final array
# length by replacing coprime pair with 1
def hasCoprimePair(arr, n):

    # Iterate over all pairs of element
    for i in range(n - 1):
        for j in range(i + 1, n):

            # Check if gcd is 1
            if (math.gcd(arr[i], arr[j]) == 1):
                return True

    # If no coprime pair
    # found return false
    return False

# Driver code
if __name__ == "__main__":

    n = 3
    arr = [ 6, 9, 15 ]

    # Check if atleast one coprime
    # pair exists in the array
    if (hasCoprimePair(arr, n)):
        print(1)

    # If no such pair exists
    else:
        print(n)

# This code is contributed by chitranayal
```

## **C#**

```
// C# Program for the above approach
using System;
class GFG{

// Recursive function to return
// gcd of a and b 
static int __gcd(int a, int b) 
{ 
    return b == 0 ? a : __gcd(b, a % b);    
}

// Function to find the readonly array
// length by replacing coprime pair with 1
static bool hasCoprimePair(int []arr, int n)
{

    // Iterate over all pairs of element
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Check if gcd is 1
            if ((__gcd(arr[i],
                       arr[j])) == 1)
            {
                return true;
            }
        }
    }

    // If no coprime pair
    // found return false
    return false;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;
    int []arr = { 6, 9, 15 };

    // Check if atleast one coprime
    // pair exists in the array
    if (hasCoprimePair(arr, n))
    {
        Console.Write(1 + "\n");
    }

    // If no such pair exists
    else
    {
        Console.Write(n + "\n");
    }
}
}

// This code is contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>

// Javascript Program for the above approach

    // Recursive function to return
    // gcd of a and b
    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to find the final array
    // length by replacing coprime pair with 1
    function hasCoprimePair(arr , n) {

        // Iterate over all pairs of element
        for (i = 0; i < n - 1; i++) {
            for (j = i + 1; j < n; j++) {

                // Check if gcd is 1
                if ((__gcd(arr[i], arr[j])) == 1) {
                    return true;
                }
            }
        }

        // If no coprime pair
        // found return false
        return false;
    }

    // Driver code

        var n = 3;
        var arr = [ 6, 9, 15 ];

        // Check if atleast one coprime
        // pair exists in the array
        if (hasCoprimePair(arr, n)) {
            document.write(1 + "\n");
        }

        // If no such pair exists
        else {
            document.write(n + "\n");
        }
// This code contributed by gauravrajput1

</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N<sup>2</sup>* log N)*
***辅助空间:** O(1)***