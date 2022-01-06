# 乘积为完美立方体的子阵列计数

> 原文:[https://www . geeksforgeeks . org/子阵列计数-将产品视为完美立方体/](https://www.geeksforgeeks.org/count-of-subarrays-having-product-as-a-perfect-cube/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是计算[个子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，其元素的乘积等于一个[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。

**示例:**

> **输入:** arr[] = {1，8，4，2}
> **输出:** 6
> **解释:**
> 元素乘积等于一个完美立方体的子阵有:
> 
> *   {1}.因此，子阵列的乘积= 1 (= (1) <sup>3</sup> )。
> *   {1, 8}.因此，子阵列的乘积= 8 ( = 2 <sup>3</sup> )。
> *   {8}.因此，子阵列的乘积= 8 = (2 <sup>3</sup> )。
> *   {4, 2}.因此，子阵列的乘积= 8 (= 2 <sup>3</sup> )。
> *   {8, 4, 2}.因此，子阵列的乘积= 64 (= 4 <sup>3</sup> )。
> *   {1, 8, 4, 2}.因此，子阵列的乘积= 64 (= 4 <sup>3</sup> )。
> 
> 因此，总数是 6。
> 
> **输入:** arr[] = {10，10，10 }
> T3】输出: 1

**天真方法:**最简单的方法是[从给定的阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中生成所有可能的子阵列，并计算那些子阵列元素的[乘积为完美立方体](https://www.geeksforgeeks.org/perfect-cube/)的子阵列。检查所有[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is perfect cube or not
bool perfectCube(int N)
{
    int cube_root;

    // Find the cube_root
    cube_root = (int)round(pow(N, 1.0 / 3.0));

    // If cube of cube_root is
    // same as N, then return true
    if (cube_root * cube_root * cube_root == N) {
        return true;
    }

    // Otherwise
    return false;
}

// Function to count subarrays
// whose product is a perfect cube
void countSubarrays(int a[], int n)
{
    // Store the required result
    int ans = 0;

    // Traverse all the subarrays
    for (int i = 0; i < n; i++) {
        int prod = 1;
        for (int j = i; j < n; j++) {

            prod = prod * a[j];

            // If product of the current
            // subarray is a perfect cube
            if (perfectCube(prod))

                // Increment count
                ans++;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 8, 4, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    countSubarrays(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
public class GFG
{
  public static void main(String args[])
  {
    int arr[] = { 1, 8, 4, 2 };
    int N = arr.length;
    countSubarrays(arr, N);
  }

  // Function to count subarrays
  // whose product is a perfect cube
  static void countSubarrays(int a[], int n)
  {

    // Store the required result
    int ans = 0;

    // Traverse all the subarrays
    for (int i = 0; i < n; i++)
    {
      int prod = 1;
      for (int j = i; j < n; j++)
      {

        prod = prod * a[j];

        // If product of the current
        // subarray is a perfect cube
        if (perfectCube(prod))

          // Increment count
          ans++;
      }
    }

    // Print the result
    System.out.println(ans);
  }

  // Function to check if a number
  // is perfect cube or not
  static boolean perfectCube(int N)
  {
    int cube_root;

    // Find the cube_root
    cube_root = (int)Math.round(Math.pow(N, 1.0 / 3.0));

    // If cube of cube_root is
    // same as N, then return true
    if (cube_root * cube_root * cube_root == N)
    {
      return true;
    }

    // Otherwise
    return false;
  }
}

// This code is contributed by abhinavjain194.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if a number
# is perfect cube or not
def perfectCube(N):

    # Find the cube_root
    cube_root = round(pow(N, 1 / 3))

    # If cube of cube_root is
    # same as N, then return true
    if (cube_root * cube_root * cube_root == N):
        return True

    # Otherwise
    return False

# Function to count subarrays
# whose product is a perfect cube
def countSubarrays(a, n):

    # Store the required result
    ans = 0

    # Traverse all the subarrays
    for i in range(n):
        prod = 1
        for j in range(i, n):

            prod = prod * a[j]

            # If product of the current
            # subarray is a perfect cube
            if (perfectCube(prod)):

                # Increment count
                ans += 1

    # Print the result
    print(ans)

# Driver Code
if __name__ == "__main__":

    arr = [1, 8, 4, 2]
    N = len(arr)

    countSubarrays(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 8, 4, 2 };
    int N = arr.Length;
    countSubarrays(arr, N);
}

  // Function to count subarrays
  // whose product is a perfect cube
  static void countSubarrays(int[] a, int n)
  {

    // Store the required result
    int ans = 0;

    // Traverse all the subarrays
    for (int i = 0; i < n; i++)
    {
      int prod = 1;
      for (int j = i; j < n; j++)
      {

        prod = prod * a[j];

        // If product of the current
        // subarray is a perfect cube
        if (perfectCube(prod))

          // Increment count
          ans++;
      }
    }

    // Print the result
    Console.Write(ans);
  }

  // Function to check if a number
  // is perfect cube or not
  static bool perfectCube(int N)
  {
    int cube_root;

    // Find the cube_root
    cube_root = (int)Math.Round(Math.Pow(N, 1.0 / 3.0));

    // If cube of cube_root is
    // same as N, then return true
    if (cube_root * cube_root * cube_root == N)
    {
      return true;
    }

    // Otherwise
    return false;
  }
}

// This code is contributed by souravghosh0416.
```

## java 描述语言

```
<script>
  // Function to count subarrays
  // whose product is a perfect cube
  function countSubarrays(a , n)
  {

    // Store the required result
    var ans = 0;

    // Traverse all the subarrays
    for (i = 0; i < n; i++)
    {
      var prod = 1;
      for (j = i; j < n; j++)
      {

        prod = prod * a[j];

        // If product of the current
        // subarray is a perfect cube
        if (perfectCube(prod))

          // Increment count
          ans++;
      }
    }

    // Print the result
    document.write(ans);
  }

  // Function to check if a number
  // is perfect cube or not
  function perfectCube(N)
  {
    var cube_root;

    // Find the cube_root
    cube_root = parseInt(Math.round(Math.pow(N, 1.0 / 3.0)));

    // If cube of cube_root is
    // same as N, then return true
    if (cube_root * cube_root * cube_root == N)
    {
      return true;
    }

    // Otherwise
    return false;
  }

  var arr = [ 1, 8, 4, 2 ];
  var N = arr.length;
  countSubarrays(arr, N);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中存储[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) **模 3** 的数量，同时[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并相应地计数完美立方体来优化。按照以下步骤解决问题:

*   初始化一个变量，比如说 **ans、**来存储需要的结果，以及一个带有 **0s** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **V** 来存储给定数组**arr【】**中每个元素的**质因数 mod 3** 的频率。
*   初始化一个 [Hashmap](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) ，说 **M，**存储质因数当前状态的频率，在 **HashMap 中通过 **1** 增加 **V** 。**
*   使用变量 **i** 遍历数组 **arr[]** 执行以下步骤:
    *   将**的质因数 mod 3 的频率存储在 **V** 中。**
    *   按 **M** 中 **V** 的频率增加**和**的值，然后增加 **M** 中 **V** 的值。
*   完成上述步骤后。打印**和**的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1e5

// Function to store the prime
// factorization of a number
void primeFactors(vector<int>& v, int n)
{
    for (int i = 2; i * i <= n; i++) {

        // If N is divisible by i
        while (n % i == 0) {

            // Increment v[i] by 1 and
            // calculate it modulo by 3
            v[i]++;
            v[i] %= 3;

            // Divide the number by i
            n /= i;
        }
    }

    // If the number is not equal to 1
    if (n != 1) {

        // Increment v[n] by 1
        v[n]++;

        // Calculate it modulo 3
        v[n] %= 3;
    }
}

// Function to count the number of
// subarrays whose product is a perfect cube
void countSubarrays(int arr[], int n)
{
    // Store the required result
    int ans = 0;

    // Stores the prime
    // factors modulo 3
    vector<int> v(MAX, 0);

    // Stores the occurrences
    // of the prime factors
    map<vector<int>, int> mp;
    mp[v]++;

    // Traverse the array, arr[]
    for (int i = 0; i < n; i++) {

        // Store the prime factors
        // and update the vector v
        primeFactors(v, arr[i]);

        // Update the answer
        ans += mp[v];

        // Increment current state
        // of the prime factors by 1
        mp[v]++;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 8, 4, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    countSubarrays(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

static int MAX = (int)(1e5);

// To store the arr as a Key in map
static class Key
{
    int arr[];

    Key(int arr[])
    {
        this.arr = arr;
    }

    @Override public int hashCode()
    {
        return 31 + Arrays.hashCode(arr);
    }

    @Override public boolean equals(Object obj)
    {
        if (this == obj)
            return true;
        if (obj == null ||
           (getClass() != obj.getClass()))
            return false;

        Key other = (Key)obj;

        if (!Arrays.equals(arr, other.arr))
            return false;

        return true;
    }
}

// Function to store the prime
// factorization of a number
static void primeFactors(int v[], int n)
{
    for(int i = 2; i * i <= n; i++)
    {

        // If N is divisible by i
        while (n % i == 0)
        {

            // Increment v[i] by 1 and
            // calculate it modulo by 3
            v[i]++;
            v[i] %= 3;

            // Divide the number by i
            n /= i;
        }
    }

    // If the number is not equal to 1
    if (n != 1)
    {

        // Increment v[n] by 1
        v[n]++;

        // Calculate it modulo 3
        v[n] %= 3;
    }
}

// Function to count the number of
// subarrays whose product is a perfect cube
static void countSubarrays(int arr[], int n)
{

    // Store the required result
    int ans = 0;

    // Stores the prime
    // factors modulo 3
    int v[] = new int[MAX];

    // Stores the occurrences
    // of the prime factors
    HashMap<Key, Integer> mp = new HashMap<>();
    mp.put(new Key(v), 1);

    // Traverse the array, arr[]
    for(int i = 0; i < n; i++)
    {

        // Store the prime factors
        // and update the vector v
        primeFactors(v, arr[i]);

        // Update the answer
        ans += mp.getOrDefault(new Key(v), 0);

        // Increment current state
        // of the prime factors by 1
        Key vv = new Key(v);
        mp.put(vv, mp.getOrDefault(vv, 0) + 1);
    }

    // Print the result
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 8, 4, 2 };
    int N = arr.length;

    countSubarrays(arr, N);
}
}

// This code is contributed by Kingash
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(N)*