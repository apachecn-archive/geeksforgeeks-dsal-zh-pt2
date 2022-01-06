# 给定数字中重复数字的计数

> 原文:[https://www . geesforgeks . org/给定数字中重复数字的计数/](https://www.geeksforgeeks.org/count-of-repeating-digits-in-a-given-number/)

给定一个数字 **N** ，任务是统计给定数字中重复数字的总数。

**示例:**

> **输入:** N = 99677
> **输出:** 2
> **解释:**
> 在给定的数字中只有 9 和 7 在重复，因此答案是 2。
> 
> **输入:** N = 12
> **输出:** 0
> **说明:**
> 在给定的数字中没有数字重复，因此答案为 0。

**天真方法:**想法是使用**两个嵌套循环**。在第一个循环中，从数字的第一个数字到最后一个数字，逐个遍历。然后，对于第一个循环中的每个数字，运行第二个循环，并搜索该数字是否也存在于数字中的任何其他位置。如果是，则将所需计数增加 1。最后，打印计算出的计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**思路是使用 [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) 存储数字的频率，然后对频率大于 1 的数字进行计数。按照以下步骤解决问题:

*   创建一个大小为 10 的数组来存储数字 0–9 的计数。最初将每个索引存储为 0。
*   现在，对于数字 N 的每个数字，递增数组中该索引的计数。
*   遍历数组并计算值大于 1 的索引。
*   最后，打印这个计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the count of
// repeating digits of the given number
int countRepeatingDigits(int N)
{
    // Initialize a variable to store
    // count of Repeating digits
    int res = 0;

    // Initialize cnt array to
    // store digit count

    int cnt[10] = { 0 };

    // Iterate through the digits of N
    while (N > 0) {

        // Retrieve the last digit of N
        int rem = N % 10;

        // Increase the count of digit
        cnt[rem]++;

        // Remove the last digit of N
        N = N / 10;
    }

    // Iterate through the cnt array
    for (int i = 0; i < 10; i++) {

        // If frequency of digit
        // is greater than 1
        if (cnt[i] > 1) {

            // Increment the count
            // of Repeating digits
            res++;
        }
    }

    // Return count of repeating digit
    return res;
}

// Driver Code
int main()
{
    // Given array arr[]
    int N = 12;

    // Function Call
    cout << countRepeatingDigits(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that returns the count of
// repeating digits of the given number
static int countRepeatingDigits(int N)
{
    // Initialize a variable to store
    // count of Repeating digits
    int res = 0;

    // Initialize cnt array to
    // store digit count

    int cnt[] = new int[10];

    // Iterate through the digits of N
    while (N > 0)
    {

        // Retrieve the last digit of N
        int rem = N % 10;

        // Increase the count of digit
        cnt[rem]++;

        // Remove the last digit of N
        N = N / 10;
    }

    // Iterate through the cnt array
    for (int i = 0; i < 10; i++)
    {

        // If frequency of digit
        // is greater than 1
        if (cnt[i] > 1)
        {

            // Increment the count
            // of Repeating digits
            res++;
        }
    }

    // Return count of repeating digit
    return res;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int N = 12;

    // Function Call
    System.out.println(countRepeatingDigits(N));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that returns the count of
# repeating digits of the given number
def countRepeatingDigits(N):

    # Initialize a variable to store
    # count of Repeating digits
    res = 0

    # Initialize cnt array to
    # store digit count
    cnt = [0] * 10

    # Iterate through the digits of N
    while (N > 0):

        # Retrieve the last digit of N
        rem = N % 10

        # Increase the count of digit
        cnt[rem] += 1

        # Remove the last digit of N
        N = N // 10

    # Iterate through the cnt array
    for i in range(10):

        # If frequency of digit
        # is greater than 1
        if (cnt[i] > 1):

            # Increment the count
            # of Repeating digits
            res += 1

    # Return count of repeating digit
    return res

# Driver Code

# Given array arr[]
N = 12

# Function call
print(countRepeatingDigits(N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that returns the count of
// repeating digits of the given number
static int countRepeatingDigits(int N)
{
    // Initialize a variable to store
    // count of Repeating digits
    int res = 0;

    // Initialize cnt array to
    // store digit count
    int []cnt = new int[10];

    // Iterate through the digits of N
    while (N > 0)
    {

        // Retrieve the last digit of N
        int rem = N % 10;

        // Increase the count of digit
        cnt[rem]++;

        // Remove the last digit of N
        N = N / 10;
    }

    // Iterate through the cnt array
    for (int i = 0; i < 10; i++)
    {

        // If frequency of digit
        // is greater than 1
        if (cnt[i] > 1)
        {

            // Increment the count
            // of Repeating digits
            res++;
        }
    }

    // Return count of repeating digit
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int N = 12;

    // Function Call
    Console.WriteLine(countRepeatingDigits(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that returns the count of
// repeating digits of the given number
function countRepeatingDigits(N)
{

    // Initialize a variable to store
    // count of Repeating digits
    var res = 0;

    // Initialize cnt array to
    // store digit count

    var cnt = Array(10).fill(0);

    // Iterate through the digits of N
    while (N > 0) {

        // Retrieve the last digit of N
        var rem = N % 10;

        // Increase the count of digit
        cnt[rem]++;

        // Remove the last digit of N
        N = N / 10;
    }

    // Iterate through the cnt array
    for (var i = 0; i < 10; i++) {

        // If frequency of digit
        // is greater than 1
        if (cnt[i] > 1) {

            // Increment the count
            // of Repeating digits
            res++;
        }
    }

    // Return count of repeating digit
    return res;
}

// Driver Code
// Given array arr[]
var N = 12;

// Function Call
document.write( countRepeatingDigits(N));

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

#### 方法 2:使用内置的 python 函数:

*   将整数转换为字符串。
*   使用计数器功能计算字符的频率。
*   如果频率大于 1，增加计数

下面是实现:

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import Counter

# Function that returns the count of
# repeating digits of the given number
def countRepeatingDigits(N):

    # converting integer to string
    number = str(N)

    # initializing count = 0
    count = 0
    frequency = Counter(number)

    # Traversing frequency
    for i in frequency:
        if(frequency[i] > 1):

            # increase the count
            count = count+1
    return count

# Driver Code

# Given array arr[]
N = 1232145

# Function call
print(countRepeatingDigits(N))

# This code is contributed by vikkycirus
```

**Output**

```
2
```