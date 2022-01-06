# 找到一个数字 X，使得给定数组在每个元素上加上 X 后的异或为 0

> 原文:[https://www . geesforgeks . org/find-a-number-x-so-给定数组的 xor-add-x-to-element-is-0/](https://www.geeksforgeeks.org/find-a-number-x-such-that-xor-of-given-array-after-adding-x-to-each-element-is-0/)

给定一个包含正整数的奇数长度为 N 的**的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找到一个正整数 **X** 这样，将 **X** 加到**arr【】**的所有元素上，然后对所有元素进行**异或**得到 **0** 。如果不存在 **X** ，则返回 **-1** 。**

**示例:**

> **输入:** arr[] = {2，4，5}
> **输出:** 1
> **说明:**以下是在 arr[]中执行的操作，以获得所需的结果。
> 为 arr[]中的每个元素添加 1 会将 arr[]更新为 arr[] = {3，5，6}
> 现在 arr[]中所有元素的 XOR 为 3^5^6 = 0。
> 因此，1 是必选项。
> 
> **输入:** arr[] = {4，5，13}
> **输出:** -1
> **说明:**不存在满足所需条件的 x。

**方法:奇数个 1 = 1，偶数个 1 = 0 的异或**。这个想法可以用来解决给定的问题。遵循以下步骤:

*   初始化变量 **X = 0** 。
*   数组元素的二进制表示将用于元素的遍历和确定 **X** 。
*   从第 0 位到第 63 位开始传输。
*   如果在任何位位置，数组元素的设置位(1)的总数是奇数，将 2 的幂与 x 相加
*   如果迭代完成后，在任何一个位位置都有奇数个 1，那么就不存在这样的 X。否则，打印 X 作为答案。

请参见下图:

> 插图:
> 
> **病例-1 (X 种可能):**取 arr[] **=** { 2，4，5}
> 
> <figure class="table">
> 
> |   | 第 5 | 第四 | 第三 | 第二 | 第一 | 第 0 次 |
> | --- | --- | --- | --- | --- | --- | --- |
> |   |   |   |   |   |   |   |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[0] | Zero | Zero | Zero | Zero | one | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[1] | Zero | Zero | Zero | one | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[2] | Zero | Zero | Zero | one | Zero | one |
> | --- | --- | --- | --- | --- | --- | --- |
> |   |   |   |   |   |   |   |
> | --- | --- | --- | --- | --- | --- | --- |
> | **X** | Zero | Zero | Zero | Zero | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> 
> *   最初，**X = 0 0 0 0 0**，在**第 0 个位置设置(1)** 位为奇数，因此为了使设置的位为偶数，翻转**第 0 个位置的位。**因此，要翻转位，只需将**(0 0 0 0 1)**添加到 **arr[]** 和 **X 中的所有元素中**
> *   现在，该表将如下所示:
> 
> <figure class="table">
> 
> |   | 第 5 | 第四 | 第三 | 第二 | 第一 | 第 0 次 |
> | --- | --- | --- | --- | --- | --- | --- |
> |   |   |   |   |   |   |   |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[0] | Zero | Zero | Zero | Zero | one | one |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[1] | Zero | Zero | Zero | one | Zero | one |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[2] | Zero | Zero | Zero | one | one | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> |   |   |   |   |   |   |   |
> | --- | --- | --- | --- | --- | --- | --- |
> | 异或 | Zero | Zero | Zero | Zero | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> | X | Zero | Zero | Zero | Zero | Zero | one |
> | --- | --- | --- | --- | --- | --- | --- |
> 
> </figure>
> 
> *   现在，将**(arr[0]+x)^(arr[1]+x)^ arr[2]+x)= 0 的**异或**，结果将为 0。所以，打印分辨率= X.**
> 
> </figure>

当没有可能的 X 时，采取以下措施

> **Case-2:** 举个例子:arr[] = { 4，5，13 }**T4】**
> 
> |   | 第 5 | 第四 | 第三 | 第二 | 第一 | 第 0 次 |
> | --- | --- | --- | --- | --- | --- | --- |
> |   |   |   |   |   |   |   |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[0] | Zero | Zero | Zero | one | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[1] | Zero | Zero | Zero | one | Zero | one |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[2] | Zero | Zero | one | one | Zero | one |
> | --- | --- | --- | --- | --- | --- | --- |
> |   |   |   |   |   |   |   |
> | --- | --- | --- | --- | --- | --- | --- |
> | 异或 | Zero | Zero | one | one | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> | X | Zero | Zero | Zero | Zero | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> 
> ****xor = arr[0]^ arr[1]^ arr[2]= 1 1 0 0，**这里在第 2 和第 3 位有奇数个的 **1** 。**
> 
> *   **因此，将 **arr** 的所有元素加上**2 ow(第二个)**，在 **X、**中再次进行**异或**，之后元素变为:**
> 
> <figure class="table">
> 
> |   | 第 5 | 第四 | 第三 | 第二 | 第一 | 第 0 次 |
> | --- | --- | --- | --- | --- | --- | --- |
> |   |   |   |   |   |   |   |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[0] | Zero | Zero | one | Zero | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[1] | Zero | Zero | one | Zero | Zero | one |
> | --- | --- | --- | --- | --- | --- | --- |
> | arr[2] | Zero | one | Zero | Zero | Zero | one |
> | --- | --- | --- | --- | --- | --- | --- |
> | 异或 | Zero | one | Zero | Zero | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> | X | Zero | Zero | Zero | one | Zero | Zero |
> | --- | --- | --- | --- | --- | --- | --- |
> 
> </figure>
> 
> **如果继续这样，异或运算中最左边的 1 会继续向左移动。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find required result
long long solve(vector<long long>& a,
                int n)
{
    long long res = 0, j = 0, one = 1;

    // For 64 Bit
    while (j < 64) {
        // j is traversing each bit
        long long Xor = 0;
        long long powerOf2 = one << j;

        for (auto x : a)
            Xor ^= x;

        if (j == 63 && (Xor & powerOf2))
            return -1;

        if (Xor & powerOf2) {
            res += powerOf2;
            for (int i = 0; i < n; i++)
                a[i] += powerOf2;
        }
        j++;
    }
    return res;
}

// Driver Code
int main()
{

    // Size of arr[]
    int N = 3;
    vector<long long> arr = { 2, 4, 5 };

    cout << solve(arr, N) << '\n';

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
class GFG{

// Function to find required result
static long solve(int[] a,
                int n)
{
    long res = 0, j = 0, one = 1;

    // For 64 Bit
    while (j < 64)
    {

        // j is traversing each bit
        long Xor = 0;
        long powerOf2 = one << j;

        for (int x : a)
            Xor ^= x;

        if (j == 63 && (Xor & powerOf2)!=0)
            return -1;

        if ((Xor & powerOf2)!=0) {
            res += powerOf2;
            for (int i = 0; i < n; i++)
                a[i] += powerOf2;
        }
        j++;
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Size of arr[]
    int N = 3;
    int[] arr = { 2, 4, 5 };

    System.out.print(solve(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## **蟒蛇 3**

```
# python program for above approach

# Function to find required result
def solve(a, n):

    res = 0
    j = 0
    one = 1

    # For 64 Bit
    while (j < 64):
                # j is traversing each bit
        Xor = 0
        powerOf2 = one << j

        for x in a:
            Xor ^= x

        if (j == 63 and (Xor & powerOf2)):
            return -1

        if (Xor & powerOf2):
            res += powerOf2
            for i in range(0, n):
                a[i] += powerOf2

        j += 1

    return res

# Driver Code
if __name__ == "__main__":

        # Size of arr[]
    N = 3
    arr = [2, 4, 5]

    print(solve(arr, N))

    # This code is contributed by rakeshsahni
```

## **C#**

```
// C# program for above approach
using System;
class GFG
{

    // Function to find required result
    static long solve(int[] a, int n)
    {
        int res = 0, j = 0, one = 1;

        // For 64 Bit
        while (j < 64)
        {

            // j is traversing each bit
            long Xor = 0;
            long powerOf2 = one << j;

            foreach (int x in a)
                Xor ^= x;

            if (j == 63 && (Xor & powerOf2) != 0)
                return -1;

            if ((Xor & powerOf2) != 0)
            {
                res += (int)powerOf2;
                for (int i = 0; i < n; i++)
                    a[i] += (int)powerOf2;
            }
            j++;
        }
        return res;
    }

    // Driver Code
    public static void Main()
    {

        // Size of arr[]
        int N = 3;
        int[] arr = { 2, 4, 5 };

        Console.Write(solve(arr, N));
    }
}

// This code is contributed by gfgking
```

## **java 描述语言**

```
<script>

// JavaScript program for above approach

// Function to find required result
function solve(a, n)
{
    let res = 0, j = 0, one = 1;

    // For 64 Bit
    while (j < 64)
    {

        // j is traversing each bit
        let Xor = 0;
        let powerOf2 = one << j;

        for(let x of a)
            Xor ^= x;

        if (j == 63 && (Xor & powerOf2))
            return -1;

        if (Xor & powerOf2)
        {
            res += powerOf2;
            for(let i = 0; i < n; i++)
                a[i] += powerOf2;
        }
        j++;
    }
    return res;
}

// Driver Code

// Size of arr[]
let N = 3;
let arr = [ 2, 4, 5 ];

document.write(solve(arr, N) + '<br>');

// This code is contributed by Potta Lokesh

</script>
```

****Output**

```
1
```** 

****时间复杂度:**O(N * logN)
T3】辅助空间: O(1)**