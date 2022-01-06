# 通过将相邻元素替换为它们的异或

使数组元素相等

> 原文:[https://www . geesforgeks . org/make-array-elements-equal-通过用它们的-xor 替换相邻元素/](https://www.geeksforgeeks.org/make-array-elements-equal-by-replacing-adjacent-elements-with-their-xor/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**，任务是检查是否有可能减少至少长度为 2 的数组，使得数组中的所有元素相等。在操作中，选择任意索引 I，并用它们的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值替换 A[i]和 A[i+1]。

**示例:**

> **输入:** A[] = {0，2，2}
> **输出:**是
> **解释:**对 i=0(基于零的索引)应用给定的操作。因此，将 A[0]和 A[1]替换为 A[0]^A[1]即 0^2- > 2。得到的数组是{2，2}，所有元素都相等。
> 
> **输入:** A[] = {2，3，1，10}
> **输出:**否
> **说明:**数组不可能有所有相等的元素

**天真方法:**上述问题可以通过观察给定的数组可以简化为两个相等元素或三个相等元素的数组来解决。以下是解决上述问题的分步方法:

*   创建一个[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，其中第 **i <sup>第</sup>T5】索引存储从数组 **A[]** 的索引 **0** 到 **i** 的元素的**异或**。**
*   情况 1:数组可以简化为两个相等的元素
    *   假设得到的数组是 ***{X，X}** 。*由于数组所有元素的 XOR 将保持不变，因此 **X^X=0=XOR( A[0…N-1])** 。通过检查数组所有元素的异或是否为 **0** ，可以很容易地处理这种情况。
*   情况 2:数组可以简化为三个相等的元素
    *   这种情况可以通过迭代 **(i，j)** 的所有可能值来处理，使得 **0 < = i < j < =N-1** 并检查是否存在 **(i，j)** 的值，使得**异或(A[0…i]) =异或(A[i+1…j]) =异或(A[j+1…N])** 。

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to make all the array elements equal
// using the given operation
void possibleEqualArray(int A[], int N)
{
    // Stores the prefix XOR array
    vector<int> pref(N);
    pref[0] = A[0];

    for (int i = 1; i < N; i++) {

        // Calculate prefix[i]
        pref[i] = pref[i - 1] ^ A[i];
    }

    // Case 1, check if the XOR of
    // the input array is 0
    if (pref[N - 1] == 0) {
        cout << "YES";
        return;
    }

    // Case 2
    // Iterate over all the ways to
    // divide the array into three
    // non empty subarrays
    int cur_xor = 0;

    for (int i = N - 1; i >= 0; i--) {

        cur_xor ^= A[i];

        for (int j = 0; j < i; j++) {

            if (j) {

                // XOR of Middle Block
                int middle_xor
 = pref[j - 1] ^ pref[i - 1];

                // XOR of Left Block
                int left_xor = pref[j - 1];

                // XOR of Right Block
                int right_xor = cur_xor;

                if (left_xor == middle_xor
                    && middle_xor == right_xor) {
                    cout << "YES";
                    return;
                }
            }
        }
    }

    // Not Possible
    cout << "NO";
}

// Driver Code
int main()
{
    int A[] = { 0, 2, 2 };
    int N = sizeof(A) / sizeof(int);

    // Function Call
    possibleEqualArray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to check if it is possible
  // to make all the array elements equal
  // using the given operation
  static void possibleEqualArray(int A[], int N)
  {

    // Stores the prefix XOR array
    int[] pref= new int[N];
    pref[0] = A[0];

    for (int i = 1; i < N; i++) {

      // Calculate prefix[i]
      pref[i] = pref[i - 1] ^ A[i];
    }

    // Case 1, check if the XOR of
    // the input array is 0
    if (pref[N - 1] == 0) {
      System.out.println("YES");
      return;
    }

    // Case 2
    // Iterate over all the ways to
    // divide the array into three
    // non empty subarrays
    int cur_xor = 0;

    for (int i = N - 1; i >= 0; i--) {

      cur_xor ^= A[i];

      for (int j = 0; j < i; j++) {

        if (j!=0) {

          // XOR of Middle Block
          int middle_xor
            = pref[j - 1] ^ pref[i - 1];

          // XOR of Left Block
          int left_xor = pref[j - 1];

          // XOR of Right Block
          int right_xor = cur_xor;

          if (left_xor == middle_xor
              && middle_xor == right_xor) {
            System.out.println( "YES");
            return;
          }
        }
      }
    }

    // Not Possible
    System.out.println( "NO");
  }

  // Driver code
  public static void main (String[] args)
  {
    int A[] = { 0, 2, 2 };
    int N = A.length;

    // Function Call
    possibleEqualArray(A, N);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 Program of the above approach

# Function to check if it is possible
# to make all the array elements equal
# using the given operation
def possibleEqualArray(A, N):

    # Stores the prefix XOR array
    pref = [0 for i in range(N)]
    pref[0] = A[0]

    for i in range(1, N, 1):

        # Calculate prefix[i]
        pref[i] = pref[i - 1] ^ A[i]

    # Case 1, check if the XOR of
    # the input array is 0
    if (pref[N - 1] == 0):
        print("YES")
        return

    # Case 2
    # Iterate over all the ways to
    # divide the array into three
    # non empty subarrays
    cur_xor = 0
    i = N - 1
    while(i >= 0):
        cur_xor ^= A[i]

        for j in range(i):
            if (j):
                # XOR of Middle Block
                middle_xor = pref[j - 1] ^ pref[i - 1]

                # XOR of Left Block
                left_xor = pref[j - 1]

                # XOR of Right Block
                right_xor = cur_xor

                if (left_xor == middle_xor and middle_xor == right_xor):
                    print("YES")
                    return

        i -= 1

    # Not Possible
    print("NO")

# Driver Code
if __name__ == '__main__':
    A = [0, 2, 2]
    N = len(A)

    # Function Call
    possibleEqualArray(A, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to check if it is possible
  // to make all the array elements equal
  // using the given operation
  static void possibleEqualArray(int []A, int N)
  {

    // Stores the prefix XOR array
    int[] pref= new int[N];
    pref[0] = A[0];

    for (int i = 1; i < N; i++) {

      // Calculate prefix[i]
      pref[i] = pref[i - 1] ^ A[i];
    }

    // Case 1, check if the XOR of
    // the input array is 0
    if (pref[N - 1] == 0) {
      Console.WriteLine("YES");
      return;
    }

    // Case 2
    // Iterate over all the ways to
    // divide the array into three
    // non empty subarrays
    int cur_xor = 0;

    for (int i = N - 1; i >= 0; i--) {

      cur_xor ^= A[i];

      for (int j = 0; j < i; j++) {

        if (j!=0) {

          // XOR of Middle Block
          int middle_xor
            = pref[j - 1] ^ pref[i - 1];

          // XOR of Left Block
          int left_xor = pref[j - 1];

          // XOR of Right Block
          int right_xor = cur_xor;

          if (left_xor == middle_xor
              && middle_xor == right_xor) {
            Console.WriteLine( "YES");
            return;
          }
        }
      }
    }

    // Not Possible
    Console.WriteLine( "NO");
  }

  // Driver code
  public static void Main(String[] args)
  {
    int []A = { 0, 2, 2 };
    int N = A.Length;

    // Function Call
    possibleEqualArray(A, N);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program of the above approach

// Function to check if it is possible
// to make all the array elements equal
// using the given operation
function possibleEqualArray(A, N) {
  // Stores the prefix XOR array
  let pref = new Array(N);
  pref[0] = A[0];

  for (let i = 1; i < N; i++) {
    // Calculate prefix[i]
    pref[i] = pref[i - 1] ^ A[i];
  }

  // Case 1, check if the XOR of
  // the input array is 0
  if (pref[N - 1] == 0) {
    document.write("YES");
    return;
  }

  // Case 2
  // Iterate over all the ways to
  // divide the array into three
  // non empty subarrays
  let cur_xor = 0;

  for (let i = N - 1; i >= 0; i--) {
    cur_xor ^= A[i];

    for (let j = 0; j < i; j++) {
      if (j) {
        // XOR of Middle Block
        let middle_xor = pref[j - 1] ^ pref[i - 1];

        // XOR of Left Block
        let left_xor = pref[j - 1];

        // XOR of Right Block
        let right_xor = cur_xor;

        if (left_xor == middle_xor && middle_xor == right_xor) {
          document.write("YES");
          return;
        }
      }
    }
  }

  // Not Possible
  document.write("NO");
}

// Driver Code

let A = [0, 2, 2];
let N = A.length;

// Function Call
possibleEqualArray(A, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
YES
```

**时间复杂度:***O(N<sup>2</sup>)*
**空间复杂度:** *O(N)*

**高效方法:**上述方法可以通过观察来优化，即在数组可以简化为三个相等元素的情况下，得到的数组可以表示为 ***{X，X，X}** 。*由于*，***(x^x^x)= xor(a[0…n-1])**意味着 **X = XOR(A[0…N-1])** 。案例 1 可以像天真的方法一样处理。案例 2 可以通过以下方式解决:

*   通过 **0** 初始化 **cnt** 和 **cur_XOR** ，将 A[]所有元素的 XOR 存储在 **tot_XOR** 中。
*   迭代数组 **A[]** ，跟踪**异或**直到 **cur_XOR** 中的当前元素。
*   如果 **cur_XOR = tot_XOR** ，将 **cnt** 增加 **1** 并初始化 **cur_XOR = 0** 。
*   遍历整个数组后，如果 **cnt > 2** 的值相等，则可以使用给定的运算使数组的所有元素相等。**T3】**

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to make all the array elements equal
// using the given operation
void possibleEqualArray(int A[], int N)
{
    // Stores the XOR of all
    // elements of array A[]
    int tot_XOR = 0;
    for (int i = 0; i < N; i++) {
        tot_XOR ^= A[i];
    }

    // Case 1, check if the XOR of
    // the array A[] is 0
    if (tot_XOR == 0) {
        cout << "YES";
        return;
    }

    // Case 2

    // Maintains the XOR till
    // the current element
    int cur_XOR = 0;
    int cnt = 0;

    // Iterate over the array
    for (int i = 0; i < N; i++) {
        cur_XOR ^= A[i];

        // If the current XOR is equal
        // to the total XOR increment
        // the count and initialize
        // current XOR as 0
        if (cur_XOR == tot_XOR) {
            cnt++;
            cur_XOR = 0;
        }
    }

    // Print Answer
    if (cnt > 2) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }
}

// Driver Code
int main()
{
    int A[] = { 0, 2, 2 };
    int N = sizeof(A) / sizeof(int);

    // Function Call
    possibleEqualArray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program of the above approach
import java.util.*;

class GFG{

// Function to check if it is possible
// to make all the array elements equal
// using the given operation
static void possibleEqualArray(int A[], int N)
{

    // Stores the XOR of all
    // elements of array A[]
    int tot_XOR = 0;
    for (int i = 0; i < N; i++) {
        tot_XOR ^= A[i];
    }

    // Case 1, check if the XOR of
    // the array A[] is 0
    if (tot_XOR == 0) {
        System.out.print("YES");
        return;
    }

    // Case 2

    // Maintains the XOR till
    // the current element
    int cur_XOR = 0;
    int cnt = 0;

    // Iterate over the array
    for (int i = 0; i < N; i++) {
        cur_XOR ^= A[i];

        // If the current XOR is equal
        // to the total XOR increment
        // the count and initialize
        // current XOR as 0
        if (cur_XOR == tot_XOR) {
            cnt++;
            cur_XOR = 0;
        }
    }

    // Print Answer
    if (cnt > 2) {
        System.out.print("YES");
    }
    else {
        System.out.print("NO");
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 0, 2, 2 };
    int N =( A.length);

    // Function Call
    possibleEqualArray(A, N);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 Program of the above approach

# Function to check if it is possible
# to make all the array elements equal
# using the given operation
def possibleEqualArray(A, N):

    # Stores the XOR of all
    # elements of array A[]
    tot_XOR = 0
    for i in range(N):
        tot_XOR ^= A[i]

    # Case 1, check if the XOR of
    # the array A[] is 0
    if (tot_XOR == 0):
        print("YES")
        return
    # Case 2

    # Maintains the XOR till
    # the current element
    cur_XOR = 0
    cnt = 0

    # Iterate over the array
    for i in range(N):
        cur_XOR ^= A[i]

        # If the current XOR is equal
        # to the total XOR increment
        # the count and initialize
        # current XOR as 0
        if (cur_XOR == tot_XOR):
            cnt += 1
            cur_XOR = 0

    # Print Answer
    if (cnt > 2):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':
    A = [0, 2, 2]
    N = len(A)

    # Function Call
    possibleEqualArray(A, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# Program of the above approach
using System;

class GFG{

// Function to check if it is possible
// to make all the array elements equal
// using the given operation
static void possibleEqualArray(int []A, int N)
{

    // Stores the XOR of all
    // elements of array A[]
    int tot_XOR = 0;
    for (int i = 0; i < N; i++) {
        tot_XOR ^= A[i];
    }

    // Case 1, check if the XOR of
    // the array A[] is 0
    if (tot_XOR == 0) {
        Console.Write("YES");
        return;
    }

    // Case 2

    // Maintains the XOR till
    // the current element
    int cur_XOR = 0;
    int cnt = 0;

    // Iterate over the array
    for (int i = 0; i < N; i++) {
        cur_XOR ^= A[i];

        // If the current XOR is equal
        // to the total XOR increment
        // the count and initialize
        // current XOR as 0
        if (cur_XOR == tot_XOR) {
            cnt++;
            cur_XOR = 0;
        }
    }

    // Print Answer
    if (cnt > 2) {
        Console.Write("YES");
    }
    else {
        Console.Write("NO");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 0, 2, 2 };
    int N =( A.Length);

    // Function Call
    possibleEqualArray(A, N);

}
}

// This code is contributed by shivanisinghss2110.
```

## java 描述语言

```
<script>
// JavaScript Program of the above approach
// Function to check if it is possible
// to make all the array elements equal
// using the given operation
function possibleEqualArray( A,  N)
{

    // Stores the XOR of all
    // elements of array A[]
    var tot_XOR = 0;
    for (var i = 0; i < N; i++) {
        tot_XOR ^= A[i];
    }

    // Case 1, check if the XOR of
    // the array A[] is 0
    if (tot_XOR == 0) {
       document.write("YES");
        return;
    }

    // Case 2

    // Maintains the XOR till
    // the current element
    var cur_XOR = 0;
    var cnt = 0;

    // Iterate over the array
    for (var i = 0; i < N; i++) {
        cur_XOR ^= A[i];

        // If the current XOR is equal
        // to the total XOR increment
        // the count and initialize
        // current XOR as 0
        if (cur_XOR == tot_XOR) {
            cnt++;
            cur_XOR = 0;
        }
    }

    // Print Answer
    if (cnt > 2) {
       document.write("YES");
    }
    else {
       document.write("NO");
    }
}

// Driver Code
    var A = [ 0, 2, 2 ];
    var N =( A.length);

    // Function Call
    possibleEqualArray(A, N);

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
YES
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*