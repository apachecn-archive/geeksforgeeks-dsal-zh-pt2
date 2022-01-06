# 将 x 的值最小化，将 c 的值最小化为 1 和 2

> 原文:[https://www . geesforgeks . org/minimum-value-of-x-the-minimum-value-of-a1 % E2 % 88% 92xca 2% E2 % 88% 92xc % C2 % B7 % C2 % B7 % B7 % C2 % b7an % E2 % 88% 92xc-for-value-c-as-1-and-2/](https://www.geeksforgeeks.org/minimize-value-of-x-that-minimizes-value-of-a1%e2%88%92xca2%e2%88%92xc%c2%b7%c2%b7%c2%b7an%e2%88%92xc-for-value-of-c-as-1-and-2/)

给定一个由 **N** 个元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到使 c = 1 的表达式的值最小的 **x** 的值。

> **| a<sub>1</sub>x |<sup>c</sup>+| a<sub>2</sub>x |<sup>c</sup>+| a<sub>n</sub>x |<sup>c</sup>= | a<sub>1</sub>x |+| a<sub>2</sub>x |+| a<sub>n</sub>x |**

**示例:**

> **输入** : arr[] = { 1，2，9，2，6 }
> **输出** : 2
> **解释**:最佳解决方案是选择 x = 2，它产生总和| 1-2 |+| 2-2 |+| 9-2 |+| 2-2 |+| 6-2 | = 12，这是最小可能的总和，对于所有其他值，如此获得的总和将大于 2
> 
> **输入** : arr[] = { 1，2，3，4，5 }
> 输出 : 3

**趋近**:一般情况下 **x** 的最佳选择是给定数字的[中值，中值是最优选择，因为如果 **x** 小于中值，则通过增加 **x** 使和变小，如果 **x** 大于中值，则通过减小 **x** 使和变小。因此，最优解是 **x** 为中位数。](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the possible
// values of x that minimizes the sum
void findX(int arr[], int n)
{
    // Sort the numbers
    sort(arr, arr + n);

    // Stores the median
    int x;

    // Only one median if n is odd
    if (n % 2 != 0) {
        x = arr[n / 2];
    }

    // Two medians if n is even
    // and every value between them
    // is optimal print any of them
    else {
        int a = arr[n / 2 - 1];
        int b = arr[n / 2];
        x = a;
    }

    int sum = 0;

    // Find minimum sum
    for (int i = 0; i < n; i++) {
        sum += abs(arr[i] - x);
    }

    cout << sum;
}

// Driver Code
int main()
{
    int arr1[] = { 1, 2, 9, 2, 6 };
    int n1 = sizeof(arr1) / sizeof(arr1[0]);

    findX(arr1, n1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG
{

  // Function to print the possible
// values of x that minimizes the sum
static void findX(int arr[], int n)
{

    // Sort the numbers
    Arrays.sort(arr);

    // Stores the median
    int x;

    // Only one median if n is odd
    if (n % 2 != 0) {
        x = arr[(int)Math.floor(n / 2)];
    }

    // Two medians if n is even
    // and every value between them
    // is optimal print any of them
    else {
        int a = arr[n / 2 - 1];
        int b = arr[n / 2];
        x = a;
    }

    int sum = 0;

    // Find minimum sum
    for (int i = 0; i < n; i++) {
        sum += Math.abs(arr[i] - x);
    }

   System.out.println( sum);
}

    public static void main (String[] args) {

    int arr1[] = { 1, 2, 9, 2, 6 };
    int n1 = arr1.length;

    findX(arr1, n1);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print the possible
# values of x that minimizes the sum
def findX(arr, n):

  # Sort the numbers
  arr.sort();

  # Stores the median
  x = None;

  # Only one median if n is odd
  if (n % 2 != 0):
    x = arr[n // 2];

  # Two medians if n is even
  # and every value between them
  # is optimal print any of them
  else:
    a = arr[(n // 2) - 1];
    b = arr[n // 2];
    x = a;
  sum = 0;

  # Find minimum sum
  for i in range(n):
    sum += abs(arr[i] - x);

  print(sum);

# Driver Code
arr1 = [1, 2, 9, 2, 6];
n1 = len(arr1)

findX(arr1, n1);

# This code is contributed by gfgking.
```

## C#

```
// C# code for the above approach
using System;

class GFG {

    // Function to print the possible
    // values of x that minimizes the sum
    static void findX(int[] arr, int n)
    {

        // Sort the numbers
        Array.Sort(arr);

        // Stores the median
        int x;

        // Only one median if n is odd
        if (n % 2 != 0) {
            x = arr[(int)Math.Floor((float)(n / 2))];
        }

        // Two medians if n is even
        // and every value between them
        // is optimal print any of them
        else {
            int a = arr[n / 2 - 1];

            x = a;
        }

        int sum = 0;

        // Find minimum sum
        for (int i = 0; i < n; i++) {
            sum += Math.Abs(arr[i] - x);
        }

        Console.WriteLine(sum);
    }

    public static void Main(string[] args)
    {

        int[] arr1 = { 1, 2, 9, 2, 6 };
        int n1 = arr1.Length;

        findX(arr1, n1);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the possible
// values of x that minimizes the sum
function findX(arr, n) {
  // Sort the numbers
  arr.sort((a, b) => a - b);

  // Stores the median
  let x;

  // Only one median if n is odd
  if (n % 2 != 0) {
    x = arr[Math.floor(n / 2)];
  }

  // Two medians if n is even
  // and every value between them
  // is optimal print any of them
  else {
    let a = arr[Math.floor(n / 2) - 1];
    let b = arr[Math.floor(n / 2)];
    x = a;
  }

  let sum = 0;

  // Find minimum sum
  for (let i = 0; i < n; i++) {
    sum += Math.abs(arr[i] - x);
  }

  document.write(sum);
}

// Driver Code

let arr1 = [1, 2, 9, 2, 6];
let n1 = arr1.length;

findX(arr1, n1);

// This code is contributed by gfgking.
</script>
```

**Output**

```
12
```

***时间复杂度*** : O(N*log N)
***辅助空间*** : O(1)

给定一个由 **N** 个元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到 **x** 的值，该值最小化 **c = 2** 的表达式值。

> **| a<sub>1</sub>x |<sup>c</sup>+| a<sub>2</sub>x |<sup>c</sup>+| a<sub>n</sub>x |<sup>c</sup>=(a<sub>1</sub>x)<sup>2</sup>+(a<sub>2</sub>x)<sup>2</sup>+(a<sub>n【T26】</sub>**

**示例:**

> ***输入*** : arr[] = { 1，2，9，2，6 }
> **输出** : 4
> **解释**:最好的方案是选择 x = 4 产生和(1−4)^2+(2−4)^2+(9−4)^2+(2−4)^2+(6−4)^2 = 46，这是最小可能和。
> 
> **输入** : arr[] = { 1，2，2，4，6 }
> 输出 : 3

**逼近**:一般情况下 **x** 的最佳选择是数字的**平均值。这个结果可以通过将总和展开如下得到:**

> **NX<sup>2</sup>—2x(a<sub>1</sub>+a<sub>2</sub>++a<sub>n</sub>+(a<sub>1</sub>**

最后一部分不依赖于 **x** 。其余零件形成一个功能**NX<sup>2</sup>2xs**，其中**s = a<sub>1</sub>+a<sub>2</sub>++a<sub>n</sub>。**对这个方程**应用导数 w.r.t x** 并将结果等于零，就得到 **x = s / n** ，这是**最小化**和的值。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value of x
// that minimizes the sum
void findX(int arr[], int n)
{
    // Store the sum
    double sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    // Store the average of numbers
    double x = sum / n;

    double minSum = 0;

    // Find minimum sum
    for (int i = 0; i < n; i++) {
        minSum += pow((arr[i] - x), 2);
    }

    cout << minSum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 9, 2, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findX(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;
public class GFG
{
// Function to find the value of x
// that minimizes the sum
static void findX(int []arr, int n)
{
    // Store the sum
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    // Store the average of numbers
    int x = sum / n;

    int minSum = 0;

    // Find minimum sum
    for (int i = 0; i < n; i++) {
        minSum += Math.pow((arr[i] - x), 2);
    }

    System.out.print(minSum);
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 1, 2, 9, 2, 6 };
    int n = arr.length;

    findX(arr, n);
}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to find the value of x
# that minimizes the sum
def findX(arr, n):

    # Store the sum
    sum = 0;
    for i in range(n):
        sum += arr[i];

    # Store the average of numbers
    x = sum // n;

    minSum = 0;

    # Find minimum sum
    for i in range(n):
        minSum += pow((arr[i] - x), 2);
    print(minSum);

# Driver Code
if __name__ == '__main__':
    arr = [ 1, 2, 9, 2, 6 ];
    n = len(arr);

    findX(arr, n);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{
// Function to find the value of x
// that minimizes the sum
static void findX(int []arr, int n)
{
    // Store the sum
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    // Store the average of numbers
    int x = sum / n;

    int minSum = 0;

    // Find minimum sum
    for (int i = 0; i < n; i++) {
        minSum += (int)Math.Pow((arr[i] - x), 2);
    }

    Console.Write(minSum);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 2, 9, 2, 6 };
    int n = arr.Length;

    findX(arr, n);
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to find the value of x
// that minimizes the sum
function findX(arr, n)
{
    // Store the sum
    let sum = 0;
    for (let i = 0; i < n; i++) {
        sum += arr[i];
    }

    // Store the average of numbers
    let x = sum / n;

    let minSum = 0;

    // Find minimum sum
    for (let i = 0; i < n; i++) {
        minSum += Math.pow((arr[i] - x), 2);
    }

    document.write(minSum);
}

// Driver Code
let arr = [ 1, 2, 9, 2, 6 ];
let n = arr.length;

findX(arr, n);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
46
```

***时间复杂度*** : O(N)
***辅助空间*** : O(1)