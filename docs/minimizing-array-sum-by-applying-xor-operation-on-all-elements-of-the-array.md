# 通过对数组的所有元素进行异或运算来最小化数组和

> 原文:[https://www . geeksforgeeks . org/通过对数组的所有元素应用异或运算来最小化数组总和/](https://www.geeksforgeeks.org/minimizing-array-sum-by-applying-xor-operation-on-all-elements-of-the-array/)

给定一个由 **N** 个整数元素组成的数组 **arr[]** ，任务是选择一个元素 **X** 并用 **X** 对数组的每个元素进行异或运算，使得数组和最小化。

> **输入:** arr[] = {3，5，7，11，15}
> **输出:** 26
> 数组元素的二进制表示为{0011，0101，0111，1011，1111}
> 我们将每个元素与 7 进行异或运算，以最小化总和。
> 3 XOR 7 = 0100(4)
> 5 XOR 7 = 0010(2)
> 7 XOR 7 = 0000(0)
> 11 XOR 7 = 1100(12)
> 15 XOR 7 = 1000(8)
> Sum = 4+2+0+12+8 = 26
> **输入:** arr[] = {1，2，3，4，5}

**方法:**任务是找到元素 **X** ，我们要用它对每个元素进行异或运算。

*   将每个数字转换为二进制形式，并根据数组中元素中每个位的位置更新数组中位(0 或 1)的频率。
*   现在，遍历数组并检查索引处的元素是否大于 n/2(对于“n”个元素，我们检查设置位在索引处是否大于 n/2)，随后，我们获得元素“X”
*   现在，对所有元素进行“X”的异或运算，并返回总和。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 25;

// Function to return the minimized sum
int getMinSum(int arr[], int n)
{
    int bits_count[MAX], max_bit = 0, sum = 0, ans = 0;

    memset(bits_count, 0, sizeof(bits_count));

    // To store the frequency
    // of bit in every element
    for (int d = 0; d < n; d++) {
        int e = arr[d], f = 0;
        while (e > 0) {
            int rem = e % 2;
            e = e / 2;
            if (rem == 1) {
                bits_count[f] += rem;
            }
            f++;
        }
        max_bit = max(max_bit, f);
    }

    // Finding element X
    for (int d = 0; d < max_bit; d++) {
        int temp = pow(2, d);
        if (bits_count[d] > n / 2)
            ans = ans + temp;
    }

    // Taking XOR of elements and finding sum
    for (int d = 0; d < n; d++) {
        arr[d] = arr[d] ^ ans;
        sum = sum + arr[d];
    }
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 3, 5, 7, 11, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getMinSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static int MAX = 25;

    // Function to return the minimized sum
    static int getMinSum(int arr[], int n)
    {
        int bits_count[] = new int[MAX],
            max_bit = 0, sum = 0, ans = 0;

        // To store the frequency
        // of bit in every element
        for (int d = 0; d < n; d++) {
            int e = arr[d], f = 0;
            while (e > 0) {
                int rem = e % 2;
                e = e / 2;
                if (rem == 1) {
                    bits_count[f] += rem;
                }
                f++;
            }
            max_bit = Math.max(max_bit, f);
        }

        // Finding element X
        for (int d = 0; d < max_bit; d++) {
            int temp = (int)Math.pow(2, d);
            if (bits_count[d] > n / 2)
                ans = ans + temp;
        }

        // Taking XOR of elements and finding sum
        for (int d = 0; d < n; d++) {
            arr[d] = arr[d] ^ ans;
            sum = sum + arr[d];
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 3, 5, 7, 11, 15 };
        int n = arr.length;
        System.out.println(getMinSum(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 25;

# Function to return the minimized sum
def getMinSum(arr, n) :
    bits_count = [0]* MAX
    max_bit = 0; sum = 0; ans = 0;

    # To store the frequency
    # of bit in every element
    for d in range(n) :
        e = arr[d]; f = 0;
        while (e > 0) :
            rem = e % 2;
            e = e // 2;
            if (rem == 1) :
                bits_count[f] += rem;

            f += 1

        max_bit = max(max_bit, f);

    # Finding element X
    for d in range(max_bit) :
        temp = pow(2, d);

        if (bits_count[d] > n // 2) :
            ans = ans + temp;

    # Taking XOR of elements and finding sum
    for d in range(n) :
        arr[d] = arr[d] ^ ans;
        sum = sum + arr[d];

    return sum

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 5, 7, 11, 15 ];
    n = len(arr);

    print(getMinSum(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    static int MAX = 25;

    // Function to return the minimized sum
    static int getMinSum(int[] arr, int n)
    {
        int[] bits_count = new int[MAX];
        int max_bit = 0, sum = 0, ans = 0;

        // To store the frequency
        // of bit in every element
        for (int d = 0; d < n; d++) {
            int e = arr[d], f = 0;
            while (e > 0) {
                int rem = e % 2;
                e = e / 2;
                if (rem == 1) {
                    bits_count[f] += rem;
                }
                f++;
            }
            max_bit = Math.Max(max_bit, f);
        }

        // Finding element X
        for (int d = 0; d < max_bit; d++) {
            int temp = (int)Math.Pow(2, d);
            if (bits_count[d] > n / 2)
                ans = ans + temp;
        }

        // Taking XOR of elements and finding sum
        for (int d = 0; d < n; d++) {
            arr[d] = arr[d] ^ ans;
            sum = sum + arr[d];
        }
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 5, 7, 11, 15 };
        int n = arr.Length;
        Console.WriteLine(getMinSum(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

const MAX = 25;

// Function to return the minimized sum
function getMinSum(arr, n)
{
    let bits_count = new Array(MAX).fill(0),
    max_bit = 0, sum = 0, ans = 0;

    // To store the frequency
    // of bit in every element
    for (let d = 0; d < n; d++) {
        let e = arr[d], f = 0;
        while (e > 0) {
            let rem = e % 2;
            e = parseInt(e / 2);
            if (rem == 1) {
                bits_count[f] += rem;
            }
            f++;
        }
        max_bit = Math.max(max_bit, f);
    }

    // Finding element X
    for (let d = 0; d < max_bit; d++) {
        let temp = Math.pow(2, d);
        if (bits_count[d] > parseInt(n / 2))
            ans = ans + temp;
    }

    // Taking XOR of elements and finding sum
    for (let d = 0; d < n; d++) {
        arr[d] = arr[d] ^ ans;
        sum = sum + arr[d];
    }
    return sum;
}

// Driver code
    let arr = [ 3, 5, 7, 11, 15 ];
    let n = arr.length;

    document.write(getMinSum(arr, n));

</script>
```

**Output:** 

```
26
```