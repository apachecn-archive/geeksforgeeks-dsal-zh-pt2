# 将排序后的数组分成 K 个部分，每个部分的最大和最小差值之和最小

> 原文:[https://www . geesforgeks . org/divide-a-sorted-array-in-k-parts-with-sum-divide-divide-a-divide-a-sorted-array-in-k-parts-with-sum-divide-divide-in-max-min-minimum-in-part-minimum-in-in](https://www.geeksforgeeks.org/divide-a-sorted-array-in-k-parts-with-sum-of-difference-of-max-and-min-minimized-in-each-part/)

给定大小为 **N** 的升序排序数组**arr【】**和整数 **K** ，任务是将给定数组划分为 **K** 个非空子数组，使得每个子数组的最大值和最小值之差之和最小。

**示例:**

> **输入:** arr[] = {4，8，15，16，23，42}，K = 3
> **输出:** 12
> **解释:**
> 给定的数组可以按照以下方式拆分为三个子数组:
> {4，8}，{15，16，23}，{42}
> 这里，每个子数组中的最小和最大元素的差之和分别为:
> 
> **输入:** arr[] = {1，2，3，4，5}，K = 5
> T3】输出: 0

**方法:**需要做的一个观察是，我们清楚地知道，只有当我们选择相邻元素作为子阵列的最大和最小元素时，子阵列的最大和最小元素之差的和才是最小的。所以:

*   假设我们必须将数组分成 K + 1 个部分，这样第一部分将是 arr[0 … i <sub>1</sub> -1]，第二部分将是 arr[i <sub>1</sub> … i <sub>2</sub> -1]，依此类推。
*   因此，K 个部分之间的差值之和将是:

> sum = arr[I<sub>1</sub>-1]–arr[0]+arr[I<sub>2</sub>-1]–arr[I<sub>1</sub>+…。+arr[n]–arr[I<sub>K</sub>]

*   重新排列上述值后，我们得到:

> sum =-arr[0]–(arr[I<sub>1</sub>–arr[I<sub>1</sub>–1】)–(arr[I<sub>2</sub>–arr[I<sub>2</sub>–1)]–……-(arr[I<sub>K</sub>–arr[I<sub>K</sub>–1])+arr[N–1]

*   显然，要计算的值是由数组中相邻元素之间的差形成的。如果这个差是最大的，那么总和将是最小的。
*   因此，其思想是迭代数组并将数组中相邻元素之间的差异存储在另一个数组中。
*   现在，按降序排列这个数组。我们知道应该取最大差值来得到最小差值。
*   因此，从数组的第一个和最后一个元素的差值中减去第一个**K–1**值。这给出了由该阵列形成的 K 个子阵列的剩余差的总和。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum
// sum of differences possible for
// the given array when the array
// is divided into K subarrays
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum
// sum of differences possible for
// the given array when the array
// is divided into K subarrays
int calculate_minimum_split(int n, int a[], int k)
{

    // Array to store the differences
    // between two adjacent elements
    int p[n - 1];

    // Iterating through the array
    for(int i = 1; i < n; i++)

        // Storing differences to p
        p[i - 1] = a[i] - a[i - 1];

    // Sorting p in descending order
    sort(p, p + n - 1, greater<int>());

    // Sum of the first k-1 values of p
    int min_sum = 0;
    for(int i = 0; i < k - 1; i++)
        min_sum += p[i];

    // Computing the result
    int res = a[n - 1] - a[0] - min_sum;

    return res;
}

// Driver code
int main()
{
    int arr[6] = { 4, 8, 15, 16, 23, 42 };
    int k = 3;
    int n = sizeof(arr) / sizeof(int);

    cout << calculate_minimum_split(n, arr, k);
}

// This code is contributed by ishayadav181
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// sum of differences possible for
// the given array when the array
// is divided into K subarrays
import java.util.*;

class GFG{

// Function to find the minimum
// sum of differences possible for
// the given array when the array
// is divided into K subarrays
static int calculate_minimum_split(int n, int a[],
                                   int k)
{

    // Array to store the differences
    // between two adjacent elements
    Integer[] p = new Integer[n - 1];

    // Iterating through the array
    for(int i = 1; i < n; i++)

        // Storing differences to p
        p[i - 1] = a[i] - a[i - 1];

    // Sorting p in descending order
    Arrays.sort(p, new Comparator<Integer>()
    {
        public int compare(Integer a, Integer b)
        {
            return b - a;
        }
    });

    // Sum of the first k-1 values of p
    int min_sum = 0;
    for(int i = 0; i < k - 1; i++)
        min_sum += p[i];

    // Computing the result
    int res = a[n - 1] - a[0] - min_sum;

    return res;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 8, 15, 16, 23, 42 };
    int k = 3;
    int n = arr.length;

    System.out.println(calculate_minimum_split(
                       n, arr, k));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# sum of differences possible for
# the given array when the array
# is divided into K subarrays

# Function to find the minimum
# sum of differences possible for
# the given array when the array
# is divided into K subarrays
def calculate_minimum_split(a, k):

    # Array to store the differences
    # between two adjacent elements
    p =[]
    n = len(a)

    # Iterating through the array
    for i in range(1, n):

        # Appending differences to p
        p.append(a[i]-a[i-1])

    # Sorting p in descending order
    p.sort(reverse = True)

    # Sum of the first k-1 values of p
    min_sum = sum(p[:k-1])

    # Computing the result
    res = a[n-1]-a[0]-min_sum

    return res

if __name__ == "__main__":
    arr = [4, 8, 15, 16, 23, 42]
    K = 3

    print(calculate_minimum_split(arr, K))
```

## C#

```
// C# program to find the minimum 
// sum of differences possible for 
// the given array when the array 
// is divided into K subarrays 
using System;

class GFG{

// Function to find the minimum 
// sum of differences possible for 
// the given array when the array 
// is divided into K subarrays 
static int calculate_minimum_split(int n, int[] a,
                                   int k) 
{ 

    // Array to store the differences 
    // between two adjacent elements 
    int[] p = new int[n - 1]; 

    // Iterating through the array 
    for(int i = 1; i < n; i++) 

        // Storing differences to p 
        p[i - 1] = a[i] - a[i - 1]; 

    // Sorting p in descending order 
    Array.Sort(p);
    Array.Reverse(p);

    // Sum of the first k-1 values of p 
    int min_sum = 0; 
    for(int i = 0; i < k - 1; i++) 
        min_sum += p[i]; 

    // Computing the result 
    int res = a[n - 1] - a[0] - min_sum; 

    return res; 
} 

// Driver code
static void Main()
{
    int[] arr = { 4, 8, 15, 16, 23, 42 }; 
    int k = 3; 
    int n = arr.Length; 

    Console.Write(calculate_minimum_split(
                  n, arr, k));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript program to find the minimum
// sum of differences possible for
// the given array when the array
// is divided into K subarrays

// Function to find the minimum
// sum of differences possible for
// the given array when the array
// is divided into K subarrays
function calculate_minimum_split(n, a, k)
{

    // Array to store the differences
    // between two adjacent elements
    let p = Array.from({length: n-1}, (_, i) => 0);

    // Iterating through the array
    for(let i = 1; i < n; i++)

        // Storing differences to p
        p[i - 1] = a[i] - a[i - 1];

    // Sorting p in descending order
    p.sort((a, b) => a - b);
    p.reverse();

    // Sum of the first k-1 values of p
    let min_sum = 0;
    for(let i = 0; i < k - 1; i++)
        min_sum += p[i];

    // Computing the result
    let res = a[n - 1] - a[0] - min_sum;

    return res;
}

// Driver Code

       let arr = [ 4, 8, 15, 16, 23, 42 ];
    let k = 3;
    let n = arr.length;

    document.write(calculate_minimum_split(
                       n, arr, k));

</script>
```

**Output:** 

```
12
```

**时间复杂度:** *O(N * log(N))* ，其中 N 是数组的大小。

**辅助空间:**T2【O(N)T4】