# 使用给定的 a 和 b 单位可以交叉的最大元素

> 原文:[https://www . geeksforgeeks . org/使用给定的 a 和 b 单位可以交叉的最大元素/](https://www.geeksforgeeks.org/maximum-elements-which-can-be-crossed-using-given-units-of-a-and-b/)

给定一个由 **N** 个元素和两个初始值 a 和 b 组成的二元数组。如果:
我们可以穿过第 I 个元素

1.  **如果 a[i] == 0** ，那么我们可以用 b 或者 a 中的任意一个的 1 个单位来穿越第 I 个元素。
2.  如果 **a[i] == 1** ，那么如果我们从 b 用 1 个单位，a 就增加 1 个单位。如果从 a 中使用 1 个单位，则 a 或 b 都不会增加。

任务是找到使用 a 和 b 单位可以交叉的元素的最大数量。
**注**:当我们在任一步 a 增加 1 时，都不能超过 a 的原值.
**例:**

> **输入:** arr[] = {0，1，0，1，0}，a = 1，b = 2；
> **输出:** 5
> 使用 1 个单位从 a 穿越第 1 元素。(a = 0 和 b = 2)
> 使用从 b 到第二个元素的 1 个单位。(a = 1 和 b = 1)
> 使用 1 个单位从 a 到交叉第 3 个元素。(a = 0，b = 1)
> 从 b 开始使用 1 个单位来交叉第 4 个元素。(a = 1 和 b = 0)
> 使用 1 个单位从 a 到交叉第 5 个元素。(a = 0，b = 0)
> **输入:** a[] = {1，0，0，1，0，1}，a = 1，b = 2
> 用 1 个单位从 b 开始交叉第一个元素。(a = 1，b = 1)
> 用 1 个单位从 b 开始穿过第二个元素。(a = 1，b = 0)
> 用 1 个单位从 a 开始穿过第三个元素。(a = 0，b = 0)
> **输出:** 3

**逼近**:迭代数组元素，执行以下步骤:

*   如果我们没有 b 或 a 中的任何一个来传递元素，请中断。
*   否则，如果没有剩下 a，就用 b，如果 arr[i] == 1，就用 a 加 1。
*   否则，如果没有剩下 b，就用 a。
*   否则，如果 arr[i]==1，则使用 b，并将 a 增加 1，直到原始 a 的最大值。
*   否则，只需使用 a 中的 1 个单位。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number
// of elements crossed
int findElementsCrossed(int arr[], int a, int b, int n)
{
    // Keep a copy of a
    int aa = a;
    int ans = 0;

    // Iterate in the binary array
    for (int i = 0; i < n; i++) {

        // If no a and b left to use
        if (a == 0 && b == 0)
            break;

        // If there is no a
        else if (a == 0) {

            // use b and increase a by 1
            // if arr[i] is 1
            if (arr[i] == 1) {
                b -= 1;
                a = min(aa, a + 1);
            }

            // simply use b
            else
                b -= 1;
        }

        // Use a if theres no b
        else if (b == 0)
            a--;

        // Increase a and use b if arr[i] == 1
        else if (arr[i] == 1 && a < aa) {
            b -= 1;
            a = min(aa, a + 1);
        }

        // Use a
        else
            a--;
        ans++;
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 0, 1, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int a = 1;
    int b = 2;
    cout << findElementsCrossed(arr, a, b, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function to find the number
// of elements crossed
static int findElementsCrossed(int arr[],
                        int a, int b, int n)
{
    // Keep a copy of a
    int aa = a;
    int ans = 0;

    // Iterate in the binary array
    for (int i = 0; i < n; i++)
    {

        // If no a and b left to use
        if (a == 0 && b == 0)
            break;

        // If there is no a
        else if (a == 0)
        {

            // use b and increase a by 1
            // if arr[i] is 1
            if (arr[i] == 1)
            {
                b -= 1;
                a = Math.min(aa, a + 1);
            }

            // simply use b
            else
                b -= 1;
        }

        // Use a if theres no b
        else if (b == 0)
            a--;

        // Increase a and use b if arr[i] == 1
        else if (arr[i] == 1 && a < aa)
        {
            b -= 1;
            a = Math.min(aa, a + 1);
        }

        // Use a
        else
            a--;
        ans++;
    }

    return ans;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 0, 0, 1, 0, 1 };
    int n = arr.length;
    int a = 1;
    int b = 2;
    System.out.println(findElementsCrossed(arr, a, b, n));

}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the number
# of elements crossed
def findElementsCrossed(arr, a, b, n):

    # Keep a copy of a
    aa = a
    ans = 0

    # Iterate in the binary array
    for i in range(n):

        # If no a and b left to use
        if (a == 0 and b == 0):
            break

        # If there is no a
        elif (a == 0):

            # use b and increase a by 1
            # if arr[i] is 1
            if (arr[i] == 1):
                b -= 1
                a = min(aa, a + 1)

            # simply use b
            else:
                b -= 1

        # Use a if theres no b
        elif (b == 0):
            a -= 1

        # Increase a and use b if arr[i] == 1
        elif (arr[i] == 1 and a < aa):
            b -= 1
            a = min(aa, a + 1)

        # Use a
        else:
            a -= 1
        ans += 1

    return ans

# Driver code
arr = [1, 0, 0, 1, 0, 1]
n = len(arr)
a = 1
b = 2
print(findElementsCrossed(arr, a, b, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to find the number
// of elements crossed
static int findElementsCrossed(int []arr,
                        int a, int b, int n)
{
    // Keep a copy of a
    int aa = a;
    int ans = 0;

    // Iterate in the binary array
    for (int i = 0; i < n; i++)
    {

        // If no a and b left to use
        if (a == 0 && b == 0)
            break;

        // If there is no a
        else if (a == 0)
        {

            // use b and increase a by 1
            // if arr[i] is 1
            if (arr[i] == 1)
            {
                b -= 1;
                a = Math.Min(aa, a + 1);
            }

            // simply use b
            else
                b -= 1;
        }

        // Use a if theres no b
        else if (b == 0)
            a--;

        // Increase a and use b if arr[i] == 1
        else if (arr[i] == 1 && a < aa)
        {
            b -= 1;
            a = Math.Min(aa, a + 1);
        }

        // Use a
        else
            a--;
        ans++;
    }

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 0, 0, 1, 0, 1 };
    int n = arr.Length;
    int a = 1;
    int b = 2;
    Console.WriteLine(findElementsCrossed(arr, a, b, n));

}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

// Function to find the number
// of elements crossed
function findElementsCrossed($arr, $a, $b, $n)
{
    // Keep a copy of a
    $aa = $a;
    $ans = 0;

    // Iterate in the binary array
    for ($i = 0; $i < $n; $i++)
    {

        // If no a and b left to use
        if ($a == 0 && $b == 0)
            break;

        // If there is no a
        else if ($a == 0)
        {

            // use b and increase a by 1
            // if arr[i] is 1
            if ($arr[$i] == 1)
            {
                $b -= 1;
                $a = min($aa, $a + 1);
            }

            // simply use b
            else
                $b -= 1;
        }

        // Use a if theres no b
        else if ($b == 0)
            $a--;

        // Increase a and use b if arr[i] == 1
        else if ($arr[$i] == 1 && $a < $aa)
        {
            $b -= 1;
            $a = min($aa, $a + 1);
        }

        // Use a
        else
            $a--;
        $ans++;
    }

    return $ans;
}

// Driver code
$arr = array(1, 0, 0, 1, 0, 1);
$n = sizeof($arr);
$a = 1;
$b = 2;
echo findElementsCrossed($arr, $a, $b, $n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to find the number
    // of elements crossed
    function findElementsCrossed(arr , a , b , n) {
        // Keep a copy of a
        var aa = a;
        var ans = 0;

        // Iterate in the binary array
        for (i = 0; i < n; i++) {

            // If no a and b left to use
            if (a == 0 && b == 0)
                break;

            // If there is no a
            else if (a == 0) {

                // use b and increase a by 1
                // if arr[i] is 1
                if (arr[i] == 1) {
                    b -= 1;
                    a = Math.min(aa, a + 1);
                }

                // simply use b
                else
                    b -= 1;
            }

            // Use a if theres no b
            else if (b == 0)
                a--;

            // Increase a and use b if arr[i] == 1
            else if (arr[i] == 1 && a < aa) {
                b -= 1;
                a = Math.min(aa, a + 1);
            }

            // Use a
            else
                a--;
            ans++;
        }

        return ans;
    }

    // Driver code

        var arr = [ 1, 0, 0, 1, 0, 1 ];
        var n = arr.length;
        var a = 1;
        var b = 2;
        document.write(findElementsCrossed(arr, a, b, n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
3
```