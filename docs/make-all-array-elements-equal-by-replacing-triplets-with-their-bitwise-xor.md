# 用它们的按位异或

替换三元组，使所有数组元素相等

> 原文:[https://www . geeksforgeeks . org/通过按位异或替换三元组来使所有数组元素相等/](https://www.geeksforgeeks.org/make-all-array-elements-equal-by-replacing-triplets-with-their-bitwise-xor/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到所有三元组 **(i，j，k)** ，从而用它们的**按位异或**值替换三元组的元素，即用**替换 arr[i]，arr[j]，arr[k](arr[I]^ arr[j]^ arr[k])**使所有数组元素相等。如果存在多个解决方案，请打印其中任何一个。否则，打印 **-1** 。

**示例:**

> **输入:** arr[] = { 4，2，1，7，2 }
> **输出:** { (0，1，2)，(2，3，4)，(0，1，4) }
> **解释:**
> 选择一个三元组(0，1，2)并用 arr[0]替换它们^ arr[1] ^ arr[2]将 arr[]修改为{ 7，7，7，7，7，2 }
> 选择一个三元组(2，3，4)并替换它们 2 }
> 选择一个三元组(0，1，4)并用 arr[0] ^ arr[1] ^ arr[2]替换它们将 arr[]修改为{ 2，2，2，2，2 }
> 
> **输入:** arr[] = { 1，3，2，2 }
> **输出:** -1

**方法:**根据以下观察可以解决问题:

> x ^ X ^ Y = Y
> X ^ Y ^ Y = X
> 如果三元组的任意两个元素相等，那么用它们的**位异或**替换三元组的所有元素，使三元组的所有元素等于三元组的第三个元素。

按照以下步骤解决问题:

*   选择形式为{ **(0，1，2)** 、 **(2，3，4)**……}的三元组使成对的元素{ **(arr[0]、arr[1])** 、 **(arr[2]、arr[3])**……}相等。
*   从上面的观察，选择形式为{ **(0，1，N–1)**、 **(2，3，N -1)** 、… }的三元组使所有数组元素等于数组的最后一个元素。
*   最后，打印三胞胎。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find triplets such that
// replacing them with their XOR make
// all array elements equal
void checkXOR(int arr[], int N)
{
    // If N is even
    if (N % 2 == 0) {

        // Calculate xor of
        // array elements
        int xro = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update xor
            xro ^= arr[i];
        }

        // If xor is not equal to 0
        if (xro != 0) {
            cout << -1 << endl;
            return;
        }

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for (int i = 0; i < N - 3; i += 2) {
            cout << i << " " << i + 1
                 << " " << i + 2 << endl;
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for (int i = 0; i < N - 3; i += 2) {
            cout << i << " " << i + 1
                 << " " << N - 1 << endl;
        }
    }
    else {

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for (int i = 0; i < N - 2; i += 2) {
            cout << i << " " << i + 1 << " "
                 << i + 2 << endl;
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for (int i = 0; i < N - 2; i += 2) {
            cout << i << " " << i + 1
                   << " " << N - 1 << endl;
        }
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 4, 2, 1, 7, 2 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    checkXOR(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find triplets such that
// replacing them with their XOR make
// all array elements equal
static void checkXOR(int arr[], int N)
{

    // If N is even
    if (N % 2 == 0)
    {

        // Calculate xor of
        // array elements
        int xro = 0;

        // Traverse the array
        for(int i = 0; i < N; i++)
        {

            // Update xor
            xro ^= arr[i];
        }

        // If xor is not equal to 0
        if (xro != 0)
        {
            System.out.println(-1);
            return;
        }

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for(int i = 0; i < N - 3; i += 2)
        {
            System.out.println(i + " " + (i + 1) +
                                   " " + (i + 2));
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for(int i = 0; i < N - 3; i += 2)
        {
            System.out.println(i + " " + (i + 1) +
                                   " " + (N - 1));
        }
    }
    else
    {

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for(int i = 0; i < N - 2; i += 2)
        {
            System.out.println(i + " " + (i + 1) +
                                   " " + (i + 2));
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for(int i = 0; i < N - 2; i += 2)
        {
            System.out.println(i + " " + (i + 1) +
                                   " " + (N - 1));
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 4, 2, 1, 7, 2 };

    // Size of array
    int N = arr.length;

    // Function call
    checkXOR(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find triplets such that
# replacing them with their XOR make
# all array elements equal
def checkXOR(arr, N):

    # If N is even
    if (N % 2 == 0):

        # Calculate xor of
        # array elements
        xro = 0;

        # Traverse the array
        for i in range(N):

            # Update xor
            xro ^= arr[i];

        # If xor is not equal to 0
        if (xro != 0):
            print(-1);
            return;

        # Selecting the triplets such that
        # elements of the pairs (arr[0], arr[1]),
        # (arr[2], arr[3])... can be made equal
        for i in range(0, N - 3, 2):
            print(i, " ", (i + 1), " ", (i + 2), end=" ");

        # Selecting the triplets such that
        # all array elements can be made
        # equal to arr[N - 1]
        for i in range(0, N - 3, 2):
            print(i, " ", (i + 1), " ", (N - 1), end=" ");

    else:

        # Selecting the triplets such that
        # elements of the pairs (arr[0], arr[1]),
        # (arr[2], arr[3])... can be made equal
        for i in range(0, N - 2, 2):
            print(i, " ", (i + 1), " ", (i + 2));

        # Selecting the triplets such that
        # all array elements can be made
        # equal to arr[N - 1]
        for i in range(0, N - 2, 2):
            print(i, " ", (i + 1), " ", (N - 1));

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [4, 2, 1, 7, 2];

    # Size of array
    N = len(arr);

    # Function call
    checkXOR(arr, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find triplets such that
// replacing them with their XOR make
// all array elements equal
static void checkXOR(int[] arr, int N)
{

    // If N is even
    if (N % 2 == 0)
    {

        // Calculate xor of
        // array elements
        int xro = 0;

        // Traverse the array
        for(int i = 0; i < N; i++)
        {

            // Update xor
            xro ^= arr[i];
        }

        // If xor is not equal to 0
        if (xro != 0)
        {
            Console.WriteLine(-1);
            return;
        }

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for(int i = 0; i < N - 3; i += 2)
        {
            Console.WriteLine(i + " " + (i + 1) +
                                  " " + (i + 2));
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for(int i = 0; i < N - 3; i += 2)
        {
            Console.WriteLine(i + " " + (i + 1) +
                                  " " + (N - 1));
        }
    }
    else
    {

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for(int i = 0; i < N - 2; i += 2)
        {
            Console.WriteLine(i + " " + (i + 1) +
                                  " " + (i + 2));
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for(int i = 0; i < N - 2; i += 2)
        {
            Console.WriteLine(i + " " + (i + 1) +
                                  " " + (N - 1));
        }
    }
}

// Driver code
public static void Main()
{

    // Given array
    int[] arr = { 4, 2, 1, 7, 2 };

    // Size of array
    int N = arr.Length;

    // Function call
    checkXOR(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find triplets such that
// replacing them with their XOR make
// all array elements equal
function checkXOR(arr, N)
{
    // If N is even
    if (N % 2 == 0) {

        // Calculate xor of
        // array elements
        let xro = 0;

        // Traverse the array
        for (let i = 0; i < N; i++) {

            // Update xor
            xro ^= arr[i];
        }

        // If xor is not equal to 0
        if (xro != 0) {
            document.write(-1 + "<br>");
            return;
        }

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for (let i = 0; i < N - 3; i += 2) {
            document.write(i + " " + (i + 1)
                 + " " + (i + 2) + "<br>");
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for (let i = 0; i < N - 3; i += 2) {
            document.write(i + " " + (i + 1)
                 + " " + (N - 1) + "<br>");
        }
    }
    else {

        // Selecting the triplets such that
        // elements of the pairs (arr[0], arr[1]),
        // (arr[2], arr[3])... can be made equal
        for (let i = 0; i < N - 2; i += 2) {
            document.write(i + " " + (i + 1) + " "
                 + (i + 2) + "<br>");
        }

        // Selecting the triplets such that
        // all array elements can be made
        // equal to arr[N - 1]
        for (let i = 0; i < N - 2; i += 2) {
            document.write(i + " " + (i + 1)
                   + " " + (N - 1) + "<br>");
        }
    }
}

// Driver Code
    // Given array
    let arr = [ 4, 2, 1, 7, 2 ];

    // Size of array
    let N = arr.length;

    // Function call
    checkXOR(arr, N);

</script>
```

**Output:** 

```
0 1 2
2 3 4
0 1 4
2 3 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)