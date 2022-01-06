# 计算总和严格大于剩余元素总和的子阵列

> 原文:[https://www . geeksforgeeks . org/计算严格大于剩余元素总和的子数组数/](https://www.geeksforgeeks.org/count-the-subarray-with-sum-strictly-greater-than-the-sum-of-remaining-elements/)

给定一个由正整数 **N** 组成的数组**arr【】**，任务是对所有子阵进行计数，其中子阵元素之和严格大于剩余元素之和。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 6
> **说明:**
> 子阵为:
> {1，2，3，4 }–子阵之和= 10，剩余元素之和{5} = 5
> {1，2，3，4，5 }–子阵之和=15，剩余元素之和= 0
> {2，3，4 }–子阵之和 5 }–子阵列之和= 14，剩余元素之和{1} = 1
> {3，4，5 }–子阵列之和= 12，剩余元素之和{1，2} = 3
> {4，5 }–子阵列之和= 9，剩余元素之和{1，2，3} = 6
> 
> **输入:** arr[] = {10，9，12，6}
> **输出:** 5
> **解释:**
> 子阵列为:
> {10，9 }–子阵列之和= 19，剩余元素之和{12，6} = 18
> {10，9，12}–子阵列之和= 31，剩余元素之和{6} = 6
> {10，9，12，12 } 12 }–子阵列之和= 21，剩余元素之和{10，6} = 16
> {9，12，6 }–子阵列之和=27，剩余元素之和{10} = 10

**天真方法:**
天真方法是使用三个嵌套循环生成每个子阵列的和，并用剩余阵列元素的和来检查计算出的子阵列和。

1.  第一个循环表示子阵列的开始。
2.  第二个循环表示子阵列的结束。
3.  在第二个循环中，我们有 for 循环来计算子数组和以及剩余的数组元素和。
4.  当 subarray_sum 严格大于 restrict _ sum 时，递增计数器。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// sub-arrays with sum strictly greater
// than the remaining elements of array
int Count_subarray(int arr[], int n)
{
    int subarray_sum, remaining_sum, count = 0;

    // For loop for beginning point of a subarray
    for (int i = 0; i < n; i++) {

        // For loop for ending point of the subarray
        for (int j = i; j < n; j++) {

            // Initialise subarray_sum and
            // remaining_sum to 0
            subarray_sum = 0;
            remaining_sum = 0;

            // For loop to calculate
            // the sum of generated subarray
            for (int k = i; k <= j; k++) {
                subarray_sum += arr[k];
            }
            // For loop to calculate the
            // sum remaining array element
            for (int l = 0; l < i; l++) {
                remaining_sum += arr[l];
            }
            for (int l = j + 1; l < n; l++) {
                remaining_sum += arr[l];
            }
            // Checking for condition when
            // subarray sum is strictly greater than
            // remaining sum of array element
            if (subarray_sum > remaining_sum) {
                count += 1;
            }
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 10, 9, 12, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << Count_subarray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to count the number of
// sub-arrays with sum strictly greater
// than the remaining elements of array
static int Count_subarray(int arr[], int n)
{
    int subarray_sum, remaining_sum, count = 0;

    // For loop for beginning point of a subarray
    for (int i = 0; i < n; i++)
    {

        // For loop for ending point of the subarray
        for (int j = i; j < n; j++)
        {

            // Initialise subarray_sum and
            // remaining_sum to 0
            subarray_sum = 0;
            remaining_sum = 0;

            // For loop to calculate
            // the sum of generated subarray
            for (int k = i; k <= j; k++)
            {
                subarray_sum += arr[k];
            }

            // For loop to calculate the
            // sum remaining array element
            for (int l = 0; l < i; l++)
            {
                remaining_sum += arr[l];
            }
            for (int l = j + 1; l < n; l++)
            {
                remaining_sum += arr[l];
            }

            // Checking for condition when
            // subarray sum is strictly greater than
            // remaining sum of array element
            if (subarray_sum > remaining_sum)
            {
                count += 1;
            }
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 10, 9, 12, 6 };
    int n = arr.length;
    System.out.print(Count_subarray(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to count the number of
# sub-arrays with sum strictly greater
# than the remaining elements of array
def Count_subarray(arr, n):
    subarray_sum, remaining_sum, count = 0, 0, 0;

    # For loop for beginning point of a subarray
    for i in range(n):

        # For loop for ending point of the subarray
        for j in range(i, n):

            # Initialise subarray_sum and
            # remaining_sum to 0
            subarray_sum = 0;
            remaining_sum = 0;

            # For loop to calculate
            # the sum of generated subarray
            for k in range(i, j + 1):
                subarray_sum += arr[k];

            # For loop to calculate the
            # sum remaining array element
            for l in range(i):
                remaining_sum += arr[l];
            for l in range(j + 1, n):
                remaining_sum += arr[l];

            # Checking for condition when
            # subarray sum is strictly greater than
            # remaining sum of array element
            if (subarray_sum > remaining_sum):
                count += 1;

    return count;

# Driver code
if __name__ == '__main__':
    arr = [ 10, 9, 12, 6];
    n = len(arr);
    print(Count_subarray(arr, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to count the number of
// sub-arrays with sum strictly greater
// than the remaining elements of array
static int Count_subarray(int []arr, int n)
{
    int subarray_sum, remaining_sum, count = 0;

    // For loop for beginning point of a subarray
    for (int i = 0; i < n; i++)
    {

        // For loop for ending point of the subarray
        for (int j = i; j < n; j++)
        {

            // Initialise subarray_sum and
            // remaining_sum to 0
            subarray_sum = 0;
            remaining_sum = 0;

            // For loop to calculate
            // the sum of generated subarray
            for (int k = i; k <= j; k++)
            {
                subarray_sum += arr[k];
            }

            // For loop to calculate the
            // sum remaining array element
            for (int l = 0; l < i; l++)
            {
                remaining_sum += arr[l];
            }
            for (int l = j + 1; l < n; l++)
            {
                remaining_sum += arr[l];
            }

            // Checking for condition when
            // subarray sum is strictly greater than
            // remaining sum of array element
            if (subarray_sum > remaining_sum)
            {
                count += 1;
            }
        }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 10, 9, 12, 6 };
    int n = arr.Length;
    Console.Write(Count_subarray(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of
// the above approach

// Function to count the number of
// sub-arrays with sum strictly greater
// than the remaining elements of array
function Count_subarray(arr, n)
{
   var subarray_sum, remaining_sum,
       count = 0;

    var i,j,k,l;
    // For loop for beginning
    // point of a subarray
    for(i = 0; i < n; i++) {

        // For loop for ending point
        // of the subarray
        for (j = i; j < n; j++) {

            // Initialise subarray_sum and
            // remaining_sum to 0
            subarray_sum = 0;
            remaining_sum = 0;

            // For loop to calculate
            // the sum of generated subarray
            for(k = i; k <= j; k++) {
                subarray_sum += arr[k];
            }
            // For loop to calculate the
            // sum remaining array element
            for (l = 0; l < i; l++) {
                remaining_sum += arr[l];
            }
            for (l = j + 1; l < n; l++) {
                remaining_sum += arr[l];
            }
            // Checking for condition when
            // subarray sum is strictly
            // greater than
            // remaining sum of array element
            if (subarray_sum > remaining_sum)
            {
                count += 1;
            }
        }
    }
    return count;
}

// Driver code
    var arr =  [10, 9, 12, 6];
    var n = arr.length;
    document.write(Count_subarray(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N <sup>3</sup> )

**有效方法:**
有效的解决方案是使用给定数组 arr[]的总和，这有助于计算子数组 _sum 和剩余 _sum。

1.  计算给定数组的总和。
2.  运行一个 for 循环，其中循环变量 **i** 表示子阵列的起始索引。
3.  另一个循环，其中每 **j** 表示子阵列的结束索引，并为每第 j 个索引计算子阵列 _sum。
4.  subarray_sum=arr[i]+arr[i+1]+…..+arr[j]
    剩余 _ 总和=总计 _ 总和–子阵列 _ 总和
5.  然后，当子阵列和严格大于阵列元素的剩余和时，检查条件并增加计数器。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

int Count_subarray(int arr[], int n)
{
    int total_sum = 0, subarray_sum,
        remaining_sum, count = 0;

    // Calculating total sum of given array
    for (int i = 0; i < n; i++) {
        total_sum += arr[i];
    }

    // For loop for beginning point of a subarray
    for (int i = 0; i < n; i++) {
        // initialise subarray_sum to 0
        subarray_sum = 0;

        // For loop for calculating
        // subarray_sum and remaining_sum
        for (int j = i; j < n; j++) {

            // Calculating subarray_sum
            // and corresponding remaining_sum
            subarray_sum += arr[j];
            remaining_sum = total_sum - subarray_sum;

            // Checking for the condition when
            // subarray sum is strictly greater than
            // the remaining sum of the array element
            if (subarray_sum > remaining_sum) {
                count += 1;
            }
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 10, 9, 12, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << Count_subarray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

static int Count_subarray(int arr[], int n)
{
    int total_sum = 0, subarray_sum,
        remaining_sum, count = 0;

    // Calculating total sum of given array
    for (int i = 0; i < n; i++)
    {
        total_sum += arr[i];
    }

    // For loop for beginning point of a subarray
    for (int i = 0; i < n; i++)
    {
        // initialise subarray_sum to 0
        subarray_sum = 0;

        // For loop for calculating
        // subarray_sum and remaining_sum
        for (int j = i; j < n; j++)
        {

            // Calculating subarray_sum
            // and corresponding remaining_sum
            subarray_sum += arr[j];
            remaining_sum = total_sum - subarray_sum;

            // Checking for the condition when
            // subarray sum is strictly greater than
            // the remaining sum of the array element
            if (subarray_sum > remaining_sum)
            {
                count += 1;
            }
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 10, 9, 12, 6 };
    int n = arr.length;
    System.out.print(Count_subarray(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

def Count_subarray(arr, n) :

    total_sum = 0;
    count = 0;

    # Calculating total sum of given array
    for i in range(n) :
        total_sum += arr[i];

    # For loop for beginning point of a subarray
    for i in range(n) :

        # initialise subarray_sum to 0
        subarray_sum = 0;

        # For loop for calculating
        # subarray_sum and remaining_sum
        for j in range(i, n) :

            # Calculating subarray_sum
            # and corresponding remaining_sum
            subarray_sum += arr[j];
            remaining_sum = total_sum - subarray_sum;

            # Checking for the condition when
            # subarray sum is strictly greater than
            # the remaining sum of the array element
            if (subarray_sum > remaining_sum) :
                count += 1;

    return count;

# Driver code
if __name__ == "__main__" :

    arr = [ 10, 9, 12, 6 ];
    n = len(arr);
    print(Count_subarray(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static int Count_subarray(int []arr, int n)
    {
        int total_sum = 0, subarray_sum,
            remaining_sum, count = 0;

        // Calculating total sum of given array
        for (int i = 0; i < n; i++)
        {
            total_sum += arr[i];
        }

        // For loop for beginning point of a subarray
        for (int i = 0; i < n; i++)
        {
            // initialise subarray_sum to 0
            subarray_sum = 0;

            // For loop for calculating
            // subarray_sum and remaining_sum
            for (int j = i; j < n; j++)
            {

                // Calculating subarray_sum
                // and corresponding remaining_sum
                subarray_sum += arr[j];
                remaining_sum = total_sum - subarray_sum;

                // Checking for the condition when
                // subarray sum is strictly greater than
                // the remaining sum of the array element
                if (subarray_sum > remaining_sum)
                {
                    count += 1;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 10, 9, 12, 6 };
        int n = arr.Length;
        Console.WriteLine(Count_subarray(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the above approach   
function Count_subarray(arr, n)
{
        var total_sum = 0, subarray_sum, remaining_sum, count = 0;

        // Calculating total sum of given array
        for (i = 0; i < n; i++)
        {
            total_sum += arr[i];
        }

        // For loop for beginning point of a subarray
        for (i = 0; i < n; i++)
        {

            // initialise subarray_sum to 0
            subarray_sum = 0;

            // For loop for calculating
            // subarray_sum and remaining_sum
            for (j = i; j < n; j++)
            {

                // Calculating subarray_sum
                // and corresponding remaining_sum
                subarray_sum += arr[j];
                remaining_sum = total_sum - subarray_sum;

                // Checking for the condition when
                // subarray sum is strictly greater than
                // the remaining sum of the array element
                if (subarray_sum > remaining_sum)
                {
                    count += 1;
                }
            }
        }
        return count;
    }

    // Driver code   
        var arr = [ 10, 9, 12, 6 ];
        var n = arr.length;
        document.write(Count_subarray(arr, n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N <sup>2</sup> )