# 求 1 到 N 的排列，这样 A 在左半部分最小，B 在右半部分最大

> 原文:[https://www . geeksforgeeks . org/find-a-1 到 n-这样的排列-a 是左半部分中的最小值，b 是右半部分中的最大值/](https://www.geeksforgeeks.org/find-a-permutation-of-1-to-n-such-that-a-is-minimum-in-left-half-and-b-is-maximum-in-right-half/)

给定三个整数 **N** 、 **A** 和 **B** ，任务是找到从 **1** 到 **N** 的成对不同数字的排列，使得 **A** 是左半部分的最小元素， **B** 是右半部分的最大元素。还给出 **N** 为偶数。如果不存在这样的排列，打印 **-1** 。

**示例:**

> **输入:** N = 6，A = 2，B = 5
> **输出:** 6，2，4，3，5，1
> **说明:** A = 2 是左半部分的最小值。
> B = 5 是右半部分的最大值。
> 
> **输入:** N = 6，A = 1，B = 3
> **输出:** -1
> **说明:**不存在这样的排列。

**天真法(蛮力):**在这种方法中，生成 **1** 到 **N** 号码的所有排列，并逐个检查。按照以下步骤，解决这个问题:

*   [生成从 **1** 到 **N** 的所有数字排列](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)，并将其存储在数组中。
*   遍历每个排列，如果在下面的排列中 **A** 是左半部分的最小值， **B** 是右半部分的最大值，那么打印排列。
*   如果不存在这样的排列，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate next permutation
void nextPermutation(vector<int>& nums)
{
    int n = nums.size(), k, l;
    for (k = n - 2; k >= 0; k--) {
        if (nums[k] < nums[k + 1]) {
            break;
        }
    }
    if (k < 0) {
        reverse(nums.begin(), nums.end());
    }
    else {
        for (l = n - 1; l > k; l--) {
            if (nums[l] > nums[k]) {
                break;
            }
        }
        swap(nums[k], nums[l]);
        reverse(nums.begin() + k + 1, nums.end());
    }
}

// Factorial function
int factorial(int n)
{
    return (n == 1 || n == 0) ? 1 : factorial(n - 1) * n;
}

// Function to returns all the permutations
// of a given array or vector
vector<vector<int> > permute(vector<int>& nums)
{
    vector<vector<int> > permuted;
    int n = nums.size();
    int factn = factorial(n);
    for (int i = 0; i < factn; i++) {
        permuted.push_back(nums);
        nextPermutation(nums);
    }
    return permuted;
}

// Function to find the permutation
// of 1 to N numbers
// having A minimas and B maximas
void findPermutation(int n, int a, int b)
{

    // Generate the array
    // containing one permutation
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        nums[i] = i + 1;
    }

    // Generate all the permutations
    vector<vector<int> > allpermutations
        = permute(nums);

    int total = allpermutations.size();
    int ansindex = -1;

    for (int i = 0; i < total; i++) {

        // Find the minima of the left half
        // maxima of the right half
        int leftmin = allpermutations[i][0];
        int rightmax = allpermutations[i][n - 1];
        for (int j = 0; j < n / 2; j++) {
            if (allpermutations[i][j] < leftmin) {
                leftmin = allpermutations[i][j];
            }
        }

        for (int j = n / 2; j < n; j++) {
            if (allpermutations[i][j] > rightmax) {
                rightmax = allpermutations[i][j];
            }
        }
        if (leftmin == a && rightmax == b) {

            // Store the index
            // of a perfect permutation
            ansindex = i;
            break;
        }
    }

    // Print -1 if no such permutation exists
    if (ansindex == -1) {
        cout << -1;
    }
    else {

        // Print the perfect permutation if exists
        for (int i = 0; i < n; i++) {
            cout << allpermutations[ansindex][i]
                 << " ";
        }
    }
}

// Driver Code
int main()
{
    int N = 6, A = 2, B = 5;
    findPermutation(N, A, B);
    return 0;
}
```

**Output**

```
2 3 6 1 4 5 
```

***时间复杂度:** O(N！)*
***辅助空间:** O(N！)*

**高效方法(贪婪方法):**上述蛮力方法可以使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)进行优化。贪婪是一种算法范式，它一点一点地建立解决方案，总是选择下一个能带来最明显和最直接好处的方案。所以，根据 **N，A，B** 的值，把问题分解成不同的可用部分。请按照以下步骤解决此问题:

*   将变量**左**初始化为 **n-b** ，将**右**初始化为 **a-1。**
*   如果**左**或**右**大于 **n/2** ，则打印 **-1**
*   否则如果 **a** 和 **b** 小于等于 **n/2** ，则打印 **-1。**
*   否则如果 **a** 和 **b** 大于 **n/2** ，则打印 **-1。**
*   否则如果 **a** 等于 **n/2+1** ， **b** 等于 **n/2** ，则打印 **n** 至 **1** 作为答案。
*   否则，[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n)** ，并执行以下任务:
    *   如果 **n-i** 等于 **a** 或 **b** ，则打印 **a** 或 **b** 否则打印 **n-i** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the desired permutation
void getpermutation(int n, int a, int b)
{
    int left = n - b, right = a - 1;

    // When b < n/2 or a > n/2
    if (left > n / 2 || right > n / 2) {
        cout << -1;
    }

    // When a and b both are
    // in the same half
    else if (a <= n / 2 && b <= n / 2) {
        cout << -1;
    }
    else if (a > n / 2 && b > n / 2) {
        cout << -1;
    }

    // The corner case
    else if (a == n / 2 + 1 && b == n / 2) {
        for (int i = 0; i < n; i++) {
            cout << n - i << " ";
        }
    }

    // Rest other combinations
    else {
        for (int i = 0; i < n; i++) {
            if (n - i == b) {
                cout << a << " ";
            }
            else if (n - i == a) {
                cout << b << " ";
            }
            else {
                cout << n - i << " ";
            }
        }
    }

    cout << endl;
}

// Driver Code
int main()
{

    int N = 6, A = 2, B = 5;
    getpermutation(N, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to get the desired permutation
static void getpermutation(int n, int a, int b)
{
    int left = n - b, right = a - 1;

    // When b < n/2 or a > n/2
    if (left > n / 2 || right > n / 2)
    {
        System.out.print(-1);
    }

    // When a and b both are
    // in the same half
    else if (a <= n / 2 && b <= n / 2)
    {
        System.out.print(-1);
    }
    else if (a > n / 2 && b > n / 2)
    {
        System.out.print(-1);
    }

    // The corner case
    else if (a == n / 2 + 1 && b == n / 2)
    {
        for(int i = 0; i < n; i++)
        {
            System.out.print(n - i + " ");
        }
    }

    // Rest other combinations
    else
    {
        for(int i = 0; i < n; i++)
        {
            if (n - i == b)
            {
                System.out.print(a + " ");
            }
            else if (n - i == a)
            {
                System.out.print(b + " ");
            }
            else
            {
                System.out.print(n - i + " ");
            }
        }
    }
    System.out.println();
}

// Driver Code
public static void main(String args[])
{
    int N = 6, A = 2, B = 5;

    getpermutation(N, A, B);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to get the desired permutation
def getpermutation(n, a, b):

    left = n - b
    right = a - 1

    # When b < n/2 or a > n/2
    if (left > n / 2 or right > n / 2):
        print(-1)

        # When a and b both are
        # in the same half
    elif (a <= n / 2 and b <= n / 2):
        print(-1)

    elif (a > n / 2 and b > n / 2):
        print(-1)

        # The corner case
    elif (a == n / 2 + 1 and b == n / 2):
        for i in range(0, n):
            print(n - i, end=" ")

        # Rest other combinations
    else:
        for i in range(0, n):
            if (n - i == b):
                print(a, end=" ")

            elif (n - i == a):
                print(b, end=" ")

            else:
                print(n - i, end=" ")

    print()

# Driver Code
if __name__ == "__main__":

    N = 6
    A = 2
    B = 5

    getpermutation(N, A, B)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to get the desired permutation
  static void getpermutation(int n, int a, int b)
  {
    int left = n - b, right = a - 1;

    // When b < n/2 or a > n/2
    if (left > n / 2 || right > n / 2) {
      Console.Write(-1);
    }

    // When a and b both are
    // in the same half
    else if (a <= n / 2 && b <= n / 2) {
      Console.Write(-1);
    }
    else if (a > n / 2 && b > n / 2) {
      Console.Write(-1);
    }

    // The corner case
    else if (a == n / 2 + 1 && b == n / 2) {
      for (int i = 0; i < n; i++) {
        Console.Write(n - i + " ");
      }
    }

    // Rest other combinations
    else {
      for (int i = 0; i < n; i++) {
        if (n - i == b) {
          Console.Write(a + " ");
        }
        else if (n - i == a) {
          Console.Write(b + " ");
        }
        else {
          Console.Write(n - i + " ");
        }
      }
    }

    Console.WriteLine();
  }

  // Driver Code
  public static void Main()
  {

    int N = 6, A = 2, B = 5;
    getpermutation(N, A, B);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to get the desired permutation
       function getpermutation(n, a, b) {
           let left = n - b, right = a - 1;

           // When b < n/2 or a > n/2
           if (left > Math.floor(n / 2) || right > Math.floor(n / 2)) {
               document.write(-1 + " ");
           }

           // When a and b both are
           // in the same half
           else if (a <= Math.floor(n / 2) && b <= Math.floor(n / 2)) {
               document.write(-1 + " ");
           }
           else if (a > Math.floor(n / 2) && b > Math.floor(n / 2)) {
               document.write(-1 + " ");
           }

           // The corner case
           else if (a == Math.floor(n / 2) + 1 && b == Math.floor(n / 2)) {
               for (let i = 0; i < n; i++) {
                   document.write(n - i + " ");
               }
           }

           // Rest other combinations
           else {
               for (let i = 0; i < n; i++) {
                   if (n - i == b) {
                       document.write(a + " ")
                   }
                   else if (n - i == a) {
                       document.write(b + " ")
                   }
                   else {
                       document.write(n - i + " ")
                   }
               }
           }

           cout << endl;
       }

       // Driver Code

       let N = 6, A = 2, B = 5;
       getpermutation(N, A, B);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
6 2 4 3 5 1 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)