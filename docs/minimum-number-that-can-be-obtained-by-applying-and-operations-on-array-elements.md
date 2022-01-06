# 对数组元素进行“+”和“*”运算可以得到的最小个数

> 原文:[https://www . geesforgeks . org/通过对数组元素应用和操作可以获得的最小数量/](https://www.geeksforgeeks.org/minimum-number-that-can-be-obtained-by-applying-and-operations-on-array-elements/)

给定一个由 **N** 正整数和长度为**(N–1)**的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，其中包含字符**'+**和**' ***，任务是在数组元素上应用[字符串](https://www.geeksforgeeks.org/string-data-structure/)和 **S** 中提到的算术运算后，找到能得到的最小数

**示例:**

> **输入:** A[] ={2，2，2，2}，S =“* *+”
> **输出:** 8
> **解释:**
> **运算 1:** 对前两个元素进行乘法运算运算即 arr[0]*arr[1] = 2*2 = 4。现在数组修改为{4，2，2}。
> **运算 2:** 对剩下的两个元素进行乘法运算，即 arr[1]*arr[2] = 2*2 = 4。现在数组修改为{4，4}。
> **运算 3:** 对剩余元素 arr[0] + arr[1] = 4 + 4 = 8 执行加法运算。现在数组修改为{8}。
> 因此，执行的操作的结果是 8，这是最小值。
> 
> **输入:** A[] = {1，2，3，4}，S = " *++"
> T3】输出: 9

**方法:**给定的问题可以使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)来解决。按照以下步骤解决问题:

*   将字符串 **S** 中乘法和加法运算的[计数存储在变量中，分别说 **mul** 和 **add** 。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   现在，应用于数组元素的运算可以被编码在掩码(二进制字符串)中，这样如果掩码的第 **i <sup>位</sup>位**被设置，那么它等于**“1”**，并且必须执行乘法运算。否则，执行加法。
*   初始化一个变量，说 **ans** 为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，存储结果的最小值。
*   因此，[在范围](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)**【0，2】<sup>(N–1)</sup>**中创建所有掩码，并在掩码中找到设置位的[号，并执行以下步骤:](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
    *   如果掩码中的设置位数等于 **mul** ，则将该掩码应用于数组 **A[]** ，即如果掩码的 **i <sup>第</sup>位**为 **'1'** ，则对 **i <sup>第</sup>T13】元素和 **(i + 1) <sup>第</sup>T17】元素进行乘法运算。****
    *   否则，执行加法。
    *   将 **ans** 的值更新为 **ans** 和上一步计算值的最小值。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest number
// that can  be obtained after applying
// the arithmetic operations mentioned
// in the string S
int minimumSum(int A[], int N, string S)
{
    // Stores the count of multiplication
    // operator in the string
    int mul = 0;
    for (int i = 0;
         i < (int)S.size(); i++) {
        if (S[i] == '*')
            mul += 1;
    }

    // Store the required result
    int ans = 1000000;

    // Iterate in the range to
    // create the mask
    for (int i = 0;
         i < (1 << (N - 1)); i++) {
        int cnt = 0;
        vector<char> v;

        // Checking the number of bits
        // that are set in the mask
        for (int j = 0; j < N - 1; j++) {

            if ((1 << j) & (i)) {
                cnt += 1;
                v.push_back('*');
            }
            else {
                v.push_back('+');
            }
        }

        // Check if the number of bits
        // that are set in the mask is
        // multiplication operation
        if (cnt == mul) {

            // Storing the elements
            // that is to be added
            deque<int> d;
            d.push_back(A[0]);

            // Apply the multiplications
            // operation first
            for (int j = 0; j < N - 1; j++) {

                // If sign is '*', then
                // multiply last element
                // of deque with arr[i]
                if (v[j] == '*') {

                    int x = d.back();
                    d.pop_back();
                    x = x * A[j + 1];

                    // Push last multiplied
                    // element in the deque
                    d.push_back(x);
                }
                else {

                    // If the element is to
                    // be added, then add
                    // it to the deque
                    d.push_back(A[j + 1]);
                }
            }

            int sum = 0;

            // Add all the element of
            // the deque
            while (d.size() > 0) {
                int x = d.front();
                sum += x;
                d.pop_front();
            }

            // Minimize the answer with
            // the given sum
            ans = min(ans, sum);
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int A[] = { 2, 2, 2, 2 };
    string S = "**+";
    int N = sizeof(A) / sizeof(A[0]);
    cout << minimumSum(A, N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the smallest number
// that can  be obtained after applying
// the arithmetic operations mentioned
// in the String S
static int minimumSum(int A[], int N, String S)
{

    // Stores the count of multiplication
    // operator in the String
    int mul = 0;
    for(int i = 0;
            i < (int)S.length(); i++)
    {
        if (S.charAt(i) == '*')
            mul += 1;
    }

    // Store the required result
    int ans = 1000000;

    // Iterate in the range to
    // create the mask
    for(int i = 0;
            i < (1 << (N - 1)); i++)
    {
        int cnt = 0;
        Vector<Character> v = new Vector<Character>();

        // Checking the number of bits
        // that are set in the mask
        for(int j = 0; j < N - 1; j++)
        {
            if (((1 << j) & (i)) > 0)
            {
                cnt += 1;
                v.add('*');
            }
            else
            {
                v.add('+');
            }
        }

        // Check if the number of bits
        // that are set in the mask is
        // multiplication operation
        if (cnt == mul)
        {

            // Storing the elements
            // that is to be added
            LinkedList<Integer> d = new LinkedList<Integer>();
            d.add(A[0]);

            // Apply the multiplications
            // operation first
            for(int j = 0; j < N - 1; j++)
            {

                // If sign is '*', then
                // multiply last element
                // of deque with arr[i]
                if (v.get(j) == '*')
                {
                    int x = d.getLast();
                    d.removeLast();
                    x = x * A[j + 1];

                    // Push last multiplied
                    // element in the deque
                    d.add(x);
                }
                else
                {

                    // If the element is to
                    // be added, then add
                    // it to the deque
                    d.add(A[j + 1]);
                }
            }
            int sum = 0;

            // Add all the element of
            // the deque
            while (d.size() > 0)
            {
                int x = d.peek();
                sum += x;
                d.removeFirst();
            }

            // Minimize the answer with
            // the given sum
            ans = Math.min(ans, sum);
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 2, 2, 2 };
    String S = "**+";
    int N = A.length;

    System.out.print(minimumSum(A, N, S));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the smallest number
# that can be obtained after applying
# the arithmetic operations mentioned
# in the string S
def minimumSum(A, N, S):

    # Stores the count of multiplication
    # operator in the string
    mul = 0
    for i in range(len(S)):
        if (S[i] == "*"):
            mul += 1

    # Store the required result
    ans = 1000000

    # Iterate in the range to
    # create the mask
    for i in range(1 << (N - 1)):
        cnt = 0
        v = []

        # Checking the number of bits
        # that are set in the mask
        for j in range(N - 1):
            if ((1 << j) & i):
                cnt += 1
                v.append("*")
            else:
                v.append("+")

        # Check if the number of bits
        # that are set in the mask is
        # multiplication operation
        if (cnt == mul):

            # Storing the elements
            # that is to be added
            d = []
            d.append(A[0])

            # Apply the multiplications
            # operation first
            for j in range(N - 1):

                # If sign is '*', then
                # multiply last element
                # of deque with arr[i]
                if (v[j] == "*"):
                    x = d[len(d) - 1]
                    d.pop()
                    x = x * A[j + 1]

                    # append last multiplied
                    # element in the deque
                    d.append(x)
                else:

                    # If the element is to
                    # be added, then add
                    # it to the deque
                    d.append(A[j + 1])

            sum = 0

            # Add all the element of
            # the deque
            while (len(d) > 0):
                x = d[0]
                sum += x
                d.pop(0)

            # Minimize the answer with
            # the given sum
            ans = min(ans, sum)

    return ans

# Driver Code
A = [ 2, 2, 2, 2 ]
S = "**+"
N = len(A)

print(minimumSum(A, N, S))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function to find the smallest number
// that can  be obtained after applying
// the arithmetic operations mentioned
// in the String S
static int minimumSum(int []A, int N, String S)
{

    // Stores the count of multiplication
    // operator in the String
    int mul = 0;
    for(int i = 0;
            i < (int)S.Length; i++)
    {
        if (S[i] == '*')
            mul += 1;
    }

    // Store the required result
    int ans = 1000000;

    // Iterate in the range to
    // create the mask
    for(int i = 0;
            i < (1 << (N - 1)); i++)
    {
        int cnt = 0;
        List<char> v = new List<char>();

        // Checking the number of bits
        // that are set in the mask
        for(int j = 0; j < N - 1; j++)
        {
            if (((1 << j) & (i)) > 0)
            {
                cnt += 1;
                v.Add('*');
            }
            else
            {
                v.Add('+');
            }
        }

        // Check if the number of bits
        // that are set in the mask is
        // multiplication operation
        if (cnt == mul)
        {

            // Storing the elements
            // that is to be added
            List<int> d = new List<int>();
            d.Add(A[0]);

            // Apply the multiplications
            // operation first
            for(int j = 0; j < N - 1; j++)
            {

                // If sign is '*', then
                // multiply last element
                // of deque with arr[i]
                if (v[j] == '*')
                {
                    int x = d[d.Count-1];
                    d.RemoveAt(d.Count-1);
                    x = x * A[j + 1];

                    // Push last multiplied
                    // element in the deque
                    d.Add(x);
                }
                else
                {

                    // If the element is to
                    // be added, then add
                    // it to the deque
                    d.Add(A[j + 1]);
                }
            }
            int sum = 0;

            // Add all the element of
            // the deque
            while (d.Count > 0)
            {
                int x = d[0];
                sum += x;
                d.RemoveAt(0);
            }

            // Minimize the answer with
            // the given sum
            ans = Math.Min(ans, sum);
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 2, 2, 2, 2 };
    String S = "**+";
    int N = A.Length;

    Console.Write(minimumSum(A, N, S));
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the smallest number
// that can  be obtained after applying
// the arithmetic operations mentioned
// in the string S
function minimumSum(A, N, S)
{

    // Stores the count of multiplication
    // operator in the string
    let mul = 0;
    for(let i = 0; i < S.length; i++)
    {
        if (S[i] == "*")
            mul += 1;
    }

    // Store the required result
    let ans = 1000000;

    // Iterate in the range to
    // create the mask
    for(let i = 0; i < 1 << (N - 1); i++)
    {
        let cnt = 0;
        let v = [];

        // Checking the number of bits
        // that are set in the mask
        for(let j = 0; j < N - 1; j++)
        {
            if ((1 << j) & i)
            {
                cnt += 1;
                v.push("*");
            } else
            {
                v.push("+");
            }
        }

        // Check if the number of bits
        // that are set in the mask is
        // multiplication operation
        if (cnt == mul)
        {

            // Storing the elements
            // that is to be added
            let d = [];
            d.push(A[0]);

            // Apply the multiplications
            // operation first
            for(let j = 0; j < N - 1; j++)
            {

                // If sign is '*', then
                // multiply last element
                // of deque with arr[i]
                if (v[j] == "*")
                {
                    let x = d[d.length - 1];
                    d.pop();
                    x = x * A[j + 1];

                    // Push last multiplied
                    // element in the deque
                    d.push(x);
                }
                else
                {
                    // If the element is to
                    // be added, then add
                    // it to the deque
                    d.push(A[j + 1]);
                }
            }

            let sum = 0;

            // Add all the element of
            // the deque
            while (d.length > 0)
            {
                let x = d[0];
                sum += x;
                d.shift();
            }

            // Minimize the answer with
            // the given sum
            ans = Math.min(ans, sum);
        }
    }
    return ans;
}

// Driver Code
let A = [ 2, 2, 2, 2 ];
let S = "**+";
let N = A.length;

document.write(minimumSum(A, N, S));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(2<sup>(N–1)</sup>* N)*
***辅助空间:** O(N)*