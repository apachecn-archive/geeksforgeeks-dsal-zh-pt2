# 通过用 a 或 b 的总和替换 a 或 b 来最小化操作，直到 a 或 b 超过 N

> 原文:[https://www . geeksforgeeks . org/通过用总和替换 a 或 b 来最小化操作，直到 a 或 b 超过 n/](https://www.geeksforgeeks.org/minimize-operations-till-a-or-b-exceeds-n-by-replacing-a-or-b-with-their-sum/)

给定三个整数 **a、b** 和 **N.** 的任务是找到 **a** 和 **b、**之间的**最小**加法运算，使得在应用这些运算之后，a 或 b 中的任一个变得大于 **N.** An **加法**运算被定义为用它们的**和**替换 a 或 b 中的**，并保留另一个【T18**

**示例**:

> **输入** : a = 2，b = 3，N = 20
> **输出** : 4
> **解释**:
> 
> *   加 2 和 3，2 + 3 = 5，用 5 代替 2，现在 a = 5，b = 3
> *   再次添加 a 和 b 5 + 3 = 8 用 8 替换 b，现在 a = 5，b = 8
> *   再次添加 a 和 b 5 + 8 = 13 用 13 替换 a。现在 a = 13，b = 8
> *   再次添加 a 和 b 13 + 8 = 21 用 21 替换 b，现在 a = 13，b = 21 这里，(b>=n)因此所需的最小运算量为 4
> 
> **输入** : a = 2，b = 3，N = 5
> **输出** : 1
> **说明**:用 2+3 代替 2 后，a 变成 5，b 变成 3，因此所需的最小运算为 1

**逼近**:想法是**将** a 和 b 相加，将它们的**和**存储在 a 和 b 的**最小值**中，每次直到任何一个数字**大于**n .**n .**背后的原因是每次使最小元素最大，使它们的和高，从而减少所需的操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the minimum number
// of operations required
int minOperations(int a, int b, int n)
{

    // Store the count of operations
    int count = 0;

    while (1) {

        // If any value is greater than N
        // return count
        if (n <= a or n <= b) {
            return count;
            break;
        }
        else {
            int sum = a + b;
            if (a < b)
                a = sum;
            else
                b = sum;
        }
        count++;
    }
    return count;
}

// Driver code
int main()
{
    int p = 2, q = 3, n = 20;
    cout << minOperations(p, q, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to print the minimum number
    // of operations required
    public static int minOperations(int a, int b, int n) {

        // Store the count of operations
        int count = 0;

        while (true) {

            // If any value is greater than N
            // return count
            if (n <= a || n <= b) {
                return count;
            } else {
                int sum = a + b;
                if (a < b)
                    a = sum;
                else
                    b = sum;
            }
            count++;
        }
    }

    // Driver code
    public static void main(String args[]) {
        int p = 2, q = 3, n = 20;
        System.out.println(minOperations(p, q, n));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to print the minimum number
# of operations required
def minOperations(a, b, n):

    # Store the count of operations
    count = 0

    while (1):

        # If any value is greater than N
        # return count
        if (n <= a or n <= b):
            return count
            break

        else:
            sum = a + b
            if (a < b):
                a = sum
            else:
                b = sum

        count += 1

    return count

# Driver code
if __name__ == "__main__":

    p = 2
    q = 3
    n = 20
    print(minOperations(p, q, n))

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to print the minimum number
        // of operations required
        function minOperations(a, b, n) {

            // Store the count of operations
            let count = 0;

            while (1) {

                // If any value is greater than N
                // return count
                if (n <= a || n <= b) {
                    return count;
                    break;
                }
                else {
                    let sum = a + b;
                    if (a < b)
                        a = sum;
                    else
                        b = sum;
                }
                count++;
            }
            return count;
        }

        // Driver code

        let p = 2, q = 3, n = 20;
        document.write(minOperations(p, q, n) + "<br>");

// This code is contributed by Potta Lokesh
    </script>
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to print the minimum number
    // of operations required
    public static int minOperations(int a, int b, int n) {

        // Store the count of operations
        int count = 0;

        while (true) {

            // If any value is greater than N
            // return count
            if (n <= a || n <= b) {
                return count;
            } else {
                int sum = a + b;
                if (a < b)
                    a = sum;
                else
                    b = sum;
            }
            count++;
        }
    }

    // Driver code
    public static void Main(string []args) {
        int p = 2, q = 3, n = 20;
        Console.WriteLine(minOperations(p, q, n));
    }
}

// This code is contributed by AnkThon
```

**Output**

```
4
```

***时间** **复杂度*** : O(min(log(max(a，N)，log(max(b，N)))
***辅助** **空间*** : O(1)