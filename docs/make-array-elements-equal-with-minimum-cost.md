# 以最小成本使数组元素相等

> 原文:[https://www . geesforgeks . org/make-array-elements-equal-with-mini-cost/](https://www.geeksforgeeks.org/make-array-elements-equal-with-minimum-cost/)

给定整数数组 **arr[]** ，任务是通过以下两个操作找到使数组元素相等的最小步数–

*   从 **0** 成本的元素中加减 2
*   用 **1** 成本从元素中加或减 1

**示例:**

> **输入:** arr[] = {4，3，2，1}
> **输出:** 2
> **解释:**
> 如上例，所有数组元素都可以等于 4 或 3，其中 2 为最小成本
> 使数组元素等于 4 的成本
> **指数 0:** 由于指数 0 已经等于 4，成本为**0**
> T16】指数 1: 向元素添加 1 将花费 **1**
> **索引 2:**4–2 = 2，向元素添加 2 将花费 **0**
> **索引 3:**4–1 = 3，在数组元素中添加 2 和 1 一次，这将花费 **1** ，因为 2 可以以成本 0 添加任意次。
> 总成本= 1 + 1 = 2
> 
> **输入:** arr[] = {3，2，1}
> **输出:** 1
> **解释:**
> 如上例，所有数组元素都可以等于 3 或 1，其中 1 为最小成本
> 使数组元素等于 3 的成本
> **索引 0:** 由于索引 0 已经等于 3，因此成本为**0**
> T16】索引 1:3–3 向元素添加 1 将花费 **1**
> **指数 2:**3–1 = 2，向元素添加 2 将花费 **0**
> 总成本= 1

**逼近**:想法是利用数组任意元素加 2 会花费 0 的事实。第二个观察结果是，将 2 加到任何奇数上会得到奇数，同样，将 2 加到偶数只会得到偶数。因此，任何元素都可以以零成本等于最近的整数，但具有相同的属性，即如果它作为初始值是奇数，它将保持奇数，或者如果它作为初始值是偶数，它将保持偶数。因此，为了找到最小成本，我们可以找到数组中奇数或偶数元素的最小数量。

**算法:**

*   求数组中奇数或偶数元素的计数(比如**计数**)。
*   找出计数和(长度–计数)之间的最小值，其中**长度**是数组的长度。
*   最小值将是使所有数组元素相等所需的成本。

**举例说明:**

```
Given Array be  - {4, 2, 3, 1}
Count of Odd Elements - 2 ({3, 1})
Count of Even Elements - 2 ({4, 2})

Hence, the minimum cost required is 2 and
the array elements can be made equal 
to any integer of even or odd value
```

下面是上述方法的实现:

## C++

```
// C++ implementation to make
// array elements equal with
// minimum cost

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// cost required to make array
// elements equal
void makearrayequal(int arr[], int n)
{
    int x = 0;

    // Loop to find the
    // count of odd elements
    for (int i = 0; i < n; i++) {
        x += arr[i] & 1;
    }

    cout << min(x, n - x) << endl;
}

// Driver Code
int main()
{
    int arr[] = { 4, 3, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    makearrayequal(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to make
// array elements equal with
// minimum cost
class GFG {

    // Function to find the minimum
    // cost required to make array
    // elements equal
    static void makearrayequal(int arr[], int n)
    {
        int x = 0;

        // Loop to find the
        // count of odd elements
        for (int i = 0; i < n; i++) {
            x += (arr[i] & 1);
        }

        System.out.println(Math.min(x, n - x));
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 4, 3, 2, 1 };
        int n = arr.length;
        makearrayequal(arr, n);

    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation to make
# array elements equal with
# minimum cost

# Function to find the minimum
# cost required to make array
# elements equal
def makearrayequal(arr,  n) :
    x = 0;

    # Loop to find the
    # count of odd elements
    for i in range(n) :
        x += arr[i] & 1;

    print(min(x, n - x));

# Driver Code
if __name__ == "__main__" :

    arr = [ 4, 3, 2, 1 ];
    n = len(arr);
    makearrayequal(arr, n);

# This code is contributed by Yash_R
```

## C#

```
// C# implementation to make
// array elements equal with
// minimum cost
using System;

class GFG {

    // Function to find the minimum
    // cost required to make array
    // elements equal
    static void makearrayequal(int []arr, int n)
    {
        int x = 0;

        // Loop to find the
        // count of odd elements
        for (int i = 0; i < n; i++) {
            x += (arr[i] & 1);
        }

        Console.WriteLine(Math.Min(x, n - x));
    }

    // Driver Code
    public static void Main (string[] args)
    {
        int []arr = { 4, 3, 2, 1 };
        int n = arr.Length;
        makearrayequal(arr, n);

    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// javascript implementation to make
// array elements equal with
// minimum cost

// Function to find the minimum
// cost required to make array
// elements equal
function makearrayequal(arr , n)
{
    var x = 0;

    // Loop to find the
    // count of odd elements
    for (i = 0; i < n; i++)
    {
        x += (arr[i] & 1);
    }
    document.write(Math.min(x, n - x));
}

// Driver Code
var arr = [ 4, 3, 2, 1 ];
var n = arr.length;
makearrayequal(arr, n);

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
2
```

**性能分析:**

*   **时间复杂度:** O(N)。
*   **辅助空间:** O(1)