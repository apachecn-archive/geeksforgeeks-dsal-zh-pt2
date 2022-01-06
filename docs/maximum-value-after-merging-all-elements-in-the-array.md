# 合并数组中所有元素后的最大值

> 原文:[https://www . geesforgeks . org/合并数组中所有元素后的最大值/](https://www.geeksforgeeks.org/maximum-value-after-merging-all-elements-in-the-array/)

给定一个大小为 **N** 的数组**。任务是合并数组中的所有元素，并找到最大可能值。可以将数组中的两个元素合并，如下所述。** 

> **如果 I 和 j 是数组的两个索引(i ≠ j)。将 jth 元素合并到 ith 元素中，使 a[i]成为 a[I]–a[j]，并从数组中移除 a[j]。**

****例:**** 

> ****输入:** a[] = {2 1 2 1} (n == 4)
> **输出:** 4
> 将第 3 个元素合并为第 2 个元素然后数组变为{2，-1，1}
> 将第 3 个元素合并为第 2 个元素然后数组变为{2，-2}
> 将 2rd 元素合并为 1nd 元素然后数组变为{4}
> **输入:** a[] = {1，3，5，-2， -6}
> **输出:** 17
> 将第 4 个元素合并为第 3 个元素，然后数组变为{1，3，-7，-6}
> 将 2rd 元素合并为第 3 个元素，然后数组变为{1，-10，-6}
> 将第 2 个元素合并为第 1 个元素，然后数组变为{11，-6}
> 将 2rd 元素合并为第 1 个元素，然后数组变为{17}**

****进场:**** 

*   **如果数组同时包含正元素和负元素，则将数组所有元素的绝对值相加**
*   **如果数组只包含正元素。然后从所有其他元素的总和中减去最少的元素**
*   **如果数组只包含负元素。首先，将所有元素替换为它们的绝对值。然后从所有其他元素的总和中减去最少的元素**

**以下是上述方法的实现:** 

## **C++**

```
// CPP program to maximum value after
// merging all elements in the array
#include <bits/stdc++.h>
using namespace std;

// Function to maximum value after
// merging all elements in the array
int Max_sum(int a[], int n)
{
    // To check if positive and negative
    // elements present or not
    int pos = 0, neg = 0;

    for(int i = 0; i < n; i++)
    {
        // Check for positive integer
        if(a[i] > 0)
            pos = 1;

        // Check for negative integer
        else if(a[i] < 0)
            neg = 1;

        // If both positive and negative
        // elements are present
        if(pos == 1 and neg == 1)
            break;
    }

    // To store maximum value possible
    int sum = 0;

    if(pos==1 and neg==1)
    {
        for(int i=0; i < n ; i++)
            sum += abs(a[i]);
    }

    else if(pos == 1)
    {
        // To find minimum value
        int mini = a[0];
        sum = a[0];
        for(int i=1; i < n; i++)
        {
            mini = min(mini, a[i]);
            sum += a[i];
        }   

        // Remove minimum element
        sum -= 2*mini;
    }   

    else if(neg == 1)
    {
        // Replace with absolute values
        for(int i = 0; i < n; i++)
            a[i] = abs(a[i]);

        // To find minimum value
        int mini = a[0];
        sum = a[0];
        for(int i=1; i < n; i++)
        {
            mini = min(mini, a[i]);
            sum += a[i];
        }   

        // Remove minimum element
        sum -= 2*mini;

    }

    // Return the required sum
    return sum;
}

// Driver code
int main()
{
    int a[] = {1, 3, 5, -2, -6};

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << Max_sum(a, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to maximum value after
// merging all elements in the array
import java.io.*;

class GFG
{

// Function to maximum value after
// merging all elements in the array
static int Max_sum(int a[], int n)
{
    // To check if positive and negative
    // elements present or not
    int pos = 0, neg = 0;

    for(int i = 0; i < n; i++)
    {
        // Check for positive integer
        if(a[i] > 0)
            pos = 1;

        // Check for negative integer
        else if(a[i] < 0)
            neg = 1;

        // If both positive and negative
        // elements are present
        if((pos == 1) && (neg == 1))
            break;
    }

    // To store maximum value possible
    int sum = 0;

    if((pos == 1) && (neg == 1))
    {
        for(int i = 0; i < n ; i++)
            sum += Math.abs(a[i]);
    }

    else if(pos == 1)
    {
        // To find minimum value
        int mini = a[0];
        sum = a[0];
        for(int i = 1; i < n; i++)
        {
            mini = Math.min(mini, a[i]);
            sum += a[i];
        }

        // Remove minimum element
        sum -= 2*mini;
    }

    else if(neg == 1)
    {
        // Replace with absolute values
        for(int i = 0; i < n; i++)
            a[i] = Math.abs(a[i]);

        // To find minimum value
        int mini = a[0];
        sum = a[0];
        for(int i = 1; i < n; i++)
        {
            mini = Math.min(mini, a[i]);
            sum += a[i];
        }

        // Remove minimum element
        sum -= 2*mini;

    }

    // Return the required sum
    return sum;
}

// Driver code
public static void main (String[] args)
{

    int []a = {1, 3, 5, -2, -6};
    int n = a.length;
    // Function call
    System.out.println (Max_sum(a, n));
}
}

// This code is contributed by ajit.
```

## **蟒蛇 3**

```
# Python 3 program to maximum value after
# merging all elements in the array

# Function to maximum value after
# merging all elements in the array
def Max_sum(a, n):
    # To check if positive and negative
    # elements present or not
    pos = 0
    neg = 0

    for i in range(n):
        # Check for positive integer
        if(a[i] > 0):
            pos = 1

        # Check for negative integer
        elif(a[i] < 0):
            neg = 1

        # If both positive and negative
        # elements are present
        if(pos == 1 and neg == 1):
            break

    # To store maximum value possible
    sum = 0

    if(pos==1 and neg==1):
        for i in range(n):
            sum += abs(a[i])

    elif(pos == 1):
        # To find minimum value
        mini = a[0]
        sum = a[0]
        for i in range(1,n,1):
            mini = min(mini, a[i])
            sum += a[i]

        # Remove minimum element
        sum -= 2*mini

    elif(neg == 1):
        # Replace with absolute values
        for i in range(n):
            a[i] = abs(a[i])

        # To find minimum value
        mini = a[0]
        sum = a[0]
        for i in range(1,n):
            mini = min(mini, a[i])
            sum += a[i]

        # Remove minimum element
        sum -= 2*mini

    # Return the required sum
    return sum

# Driver code
if __name__ == '__main__':
    a = [1, 3, 5, -2, -6]

    n = len(a)

    # Function call
    print(Max_sum(a, n))

# This code is contributed by
# Surendra_Gangwar
```

## **C#**

```
// C# program to maximum value after
// merging all elements in the array
using System;

class GFG
{

    // Function to maximum value after
    // merging all elements in the array
    static int Max_sum(int[] a, int n)
    {
        // To check if positive and negative
        // elements present or not
        int pos = 0, neg = 0;

        for (int i = 0; i < n; i++)
        {
            // Check for positive integer
            if (a[i] > 0)
                pos = 1;

            // Check for negative integer
            else if (a[i] < 0)
                neg = 1;

            // If both positive and negative
            // elements are present
            if ((pos == 1) && (neg == 1))
                break;
        }

        // To store maximum value possible
        int sum = 0;

        if ((pos == 1) && (neg == 1))
        {
            for (int i = 0; i < n; i++)
                sum += Math.Abs(a[i]);
        }

        else if (pos == 1)
        {
            // To find minimum value
            int mini = a[0];
            sum = a[0];
            for (int i = 1; i < n; i++)
            {
                mini = Math.Min(mini, a[i]);
                sum += a[i];
            }

            // Remove minimum element
            sum -= 2 * mini;
        }

        else if (neg == 1)
        {
            // Replace with absolute values
            for (int i = 0; i < n; i++)
                a[i] = Math.Abs(a[i]);

            // To find minimum value
            int mini = a[0];
            sum = a[0];
            for (int i = 1; i < n; i++)
            {
                mini = Math.Min(mini, a[i]);
                sum += a[i];
            }

            // Remove minimum element
            sum -= 2 * mini;

        }

        // Return the required sum
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {

        int[] a = { 1, 3, 5, -2, -6 };
        int n = a.Length;

        // Function call
        Console.WriteLine(Max_sum(a, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## **java 描述语言**

```
<script>
// Javascript program to maximum value after
// merging all elements in the array

// Function to maximum value after
// merging all elements in the array
function Max_sum(a, n)
{
    // To check if positive and negative
    // elements present or not
    let pos = 0, neg = 0;

    for(let i = 0; i < n; i++)
    {
        // Check for positive integer
        if(a[i] > 0)
            pos = 1;

        // Check for negative integer
        else if(a[i] < 0)
            neg = 1;

        // If both positive and negative
        // elements are present
        if(pos == 1 && neg == 1)
            break;
    }

    // To store maximum value possible
    let sum = 0;

    if(pos==1 && neg==1)
    {
        for(let i=0; i < n ; i++)
            sum += Math.abs(a[i]);
    }

    else if(pos == 1)
    {
        // To find minimum value
        let mini = a[0];
        sum = a[0];
        for(let i=1; i < n; i++)
        {
            mini = Math.min(mini, a[i]);
            sum += a[i];
        }   

        // Remove minimum element
        sum -= 2*mini;
    }   

    else if(neg == 1)
    {
        // Replace with absolute values
        for(let i = 0; i < n; i++)
            a[i] = Math.abs(a[i]);

        // To find minimum value
        let mini = a[0];
        sum = a[0];
        for(let i=1; i < n; i++)
        {
            mini = Math.min(mini, a[i]);
            sum += a[i];
        }   

        // Remove minimum element
        sum -= 2*mini;

    }

    // Return the required sum
    return sum;
}

// Driver code
    let a = [1, 3, 5, -2, -6];

    let n = a.length;

    // Function call
    document.write(Max_sum(a, n));

</script>
```

****输出:**** 

```
17
```