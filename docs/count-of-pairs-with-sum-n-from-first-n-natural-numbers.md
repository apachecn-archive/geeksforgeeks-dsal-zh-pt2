# 前 N 个自然数的和为 N 的对的计数

> 原文:[https://www . geesforgeks . org/从第一个 n 个自然数开始的 n 对计数/](https://www.geeksforgeeks.org/count-of-pairs-with-sum-n-from-first-n-natural-numbers/)

给定一个整数 **N** ，任务是统计第一个 **N** 自然数中的对数，和等于 **N** 。

**示例:**

> **输入:** N = 8
> **输出:** 3
> **解释:**
> 总和为 8 的所有可能对为{ (1，7)，(2，6)，(3，5)}
> 
> **输入:**N = 9
> T3】输出: 4

**天真方法:**
解决问题最简单的方法就是用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)。按照以下步骤解决问题:

*   初始设置 **i = 0** 和**j = N–1**。
*   迭代直到 **i > = j** ，对于每对 **i，j** ，检查它们的和是否等于 **N** 。如果是，增加对的**计数**。
*   分别通过 **1** 增加和减少 **i** 和 **j** 移动到下一对。
*   最后，打印获得的对的**计数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

int numberOfPairs(int n)
{

    // Stores the count of
    // pairs
    int count = 0;
    // Set the two pointers
    int i = 1, j = n - 1;

    while (i < j) {

        // Check if the sum of
        // pairs is equal to N
        if (i + j == n) {
            // Increase the count
            // of pairs
            count++;
        }

        // Move to the next pair
        i++;
        j--;
    }

    return count;
}

// Driver Code
int main()
{
    int n = 8;
    cout << numberOfPairs(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate the value of count
public static int numberOfPairs(int n)
{

    // Stores the count of pairs
    int count = 0;

    // Set the two pointers
    int i = 1, j = n - 1;

    while (i < j)
    {

        // Check if the sum of
        // pairs is equal to N
        if (i + j == n)
        {

            // Increase the count
            // of pairs
            count++;
        }

        // Move to the next pair
        i++;
        j--;
    }
    return count;
}

// Driver code
public static void main (String[] args)
{
    int n = 8;

    System.out.println(numberOfPairs(n));
}
}

// This code is contributed by piyush3010
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
def numberOfPairs(n):

  # Stores the count
  # of pairs
  count = 0

  # Set the two pointers
  i = 1
  j = n - 1

  while(i < j):

    # Check if the sum
    # of pirs is equal to n
    if (i + j) == n:

      # Increase the count of pairs
      count += 1

      # Move to the next pair
      i += 1
      j -= 1

  return count

# Driver code
if __name__=='__main__':

  n = 8
  print(numberOfPairs(n))

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to calculate the value of count
public static int numberOfPairs(int n)
{

    // Stores the count of pairs
    int count = 0;

    // Set the two pointers
    int i = 1, j = n - 1;

    while (i < j)
    {

        // Check if the sum of
        // pairs is equal to N
        if (i + j == n)
        {

            // Increase the count
            // of pairs
            count++;
        }

        // Move to the next pair
        i++;
        j--;
    }
    return count;
}

// Driver code
public static void Main (string[] args)
{
    int n = 8;

    Console.Write(numberOfPairs(n));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
function numberOfPairs(n)
{

    // Stores the count of
    // pairs
    let count = 0;

    // Set the two pointers
    let i = 1, j = n - 1;

    while (i < j)
    {

        // Check if the sum of
        // pairs is equal to N
        if (i + j == n)
        {

            // Increase the count
            // of pairs
            count++;
        }

        // Move to the next pair
        i++;
        j--;
    }
    return count;
}

// Driver code
let n = 8;

document.write(numberOfPairs(n));

// This code is contributed by divyesh072019

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效进场:**
要优化以上进场，我们只需要观察 **N** 是 ***偶数*** 还是 ***奇数。*** 如果 **N** 为偶数，则可能的对数为**N/2–1。**否则为 **N/2。**

> 插图:
> 
> N = 8
> 所有可能的对是(1，7)、(2，6)和(3，5)
> 因此，可能对的计数= 3 = 8/2–1
> 
> N = 9
> 所有可能的对是(1，8)、(2，7)、(3，6)和(4，5)
> 因此，可能对的计数= 4 = 9/2

下面是上述方法的实现:

## C++

```
// C++ program to count the number
// of pairs among the first N
// natural numbers with sum N
#include <iostream>
using namespace std;

// Function to return the
// count of pairs
int numberOfPairs(int n)
{
    // If n is even
    if (n % 2 == 0)

        // Count of pairs
        return n / 2 - 1;

    // Otherwise
    else
        return n / 2;
}

// Driver Code
int main()
{
    int n = 8;
    cout << numberOfPairs(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of pairs among the first N
// natural numbers with sum N
import java.io.*;

class GFG{

// Function to calculate the value of count
public static int numberOfPairs(int n)
{

    // If n is even
    if (n % 2 == 0)

        // Count of pairs
        return n / 2 - 1;

    // Otherwise
    else
        return n / 2;
}

// Driver code
public static void main (String[] args)
{
    int n = 8;

    System.out.println(numberOfPairs(n));
}
}

// This code is contributed by piyush3010
```

## 蟒蛇 3

```
# Python3 program to count the number
# of pairs among the first N
# natural numbers with sum N

# Function to calculate the value of count
def numberOfPairs(n):

    # If n is even
    if (n % 2 == 0):

        # Count of pairs
        return n // 2 - 1;

    # Otherwise
    else:
        return n // 2;

# Driver code
n = 8;

print(numberOfPairs(n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to count the number
// of pairs among the first N
// natural numbers with sum N
using System;
class GFG{

// Function to calculate the value of count
public static int numberOfPairs(int n)
{

    // If n is even
    if (n % 2 == 0)

        // Count of pairs
        return n / 2 - 1;

    // Otherwise
    else
        return n / 2;
}

// Driver code
public static void Main (string[] args)
{
    int n = 8;

    Console.Write(numberOfPairs(n));
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// Javascript program to count the number
// of pairs among the first N
// natural numbers with sum N

// Function to return the
// count of pairs
function numberOfPairs(n)
{

    // If n is even
    if (n % 2 == 0)

        // Count of pairs
        return (n / 2 - 1);

    // Otherwise
    else
        return (n / 2);
}

// Driver code
let n = 8;

document.write(numberOfPairs(n));

// This code is contributed by rameshtravel07

</script>
```

**Output**

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)