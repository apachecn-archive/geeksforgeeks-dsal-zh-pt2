# 范围乘积为正整数的数组中索引对的计数

> 原文:[https://www . geeksforgeeks . org/数组中范围乘积为正整数的索引对计数/](https://www.geeksforgeeks.org/count-of-index-pairs-in-array-whose-range-product-is-a-positive-integer/)

给定一个非零整数的数组 **A** ，任务是找到对的数量 **(l，r)** 其中(l < = r)使得 **A[l]*A[l+1]*A[l+2]…。A[r]** 为正。
**举例:**

> **输入:** A = {5，-3，3，-1，1}
> **输出:** 7
> **解释:**
> 第一对， **(1，1)** = 5 为正
> 第二对， **(3，3)** = 3 为正
> 第三对， **(1，4)**= 5 *-3 *-1 = 45 为正
> **(1，5)** = 5 * -3 * 3 * -1 * 1 = 45 为正
> 第六对， **(2，5)** = -3 * 3 * -1 * 1 = 9 为正
> 第七对， **(5，5)** = 1 为正
> 所以，有 7 对带正积。
> **输入:** A = {4，2，-4，3，1，2，-4，3，2，3}
> **输出:** 27

**方法:**
想法是检查每个数组元素可能的数字对。

*   迭代数组，对数组中的每个元素执行以下步骤。
*   记录前面有偶数个负元素的元素数量**(作为偶数计数)**和前面有奇数个负元素的元素数量**(作为奇数计数)**。
*   存储到现在的负元素总数**(作为 total_count)** 。
*   如果**总计数**为偶数，则在答案中加上**偶数计数**。否则添加**奇数 _ 计数**。

以下是上述方法的实现:

## C++

```
// C++ Program to find the
// count of index pairs
// in the array positive
// range product

#include <bits/stdc++.h>
using namespace std;

void positiveProduct(int arr[], int n)
{
    int even_count = 0;
    int odd_count = 0;
    int total_count = 0;
    int ans = 0;

    for (int i = 0; i < n; i++) {

        // Condition if number of
        // negative elements is even
        // then increase even_count
        if (total_count % 2 == 0)
            even_count++;

        // Otherwise increase odd_count
        else
            odd_count++;

        // Condition if current element
        // is negative
        if (arr[i] < 0)
            total_count++;

        // Condition if number of
        // negative elements is even
        // then add even_count
        // in answer
        if (total_count % 2 == 0)
            ans += even_count;

        // Otherwise add odd_count
        // in answer
        else
            ans += odd_count;
    }

    cout << ans << "\n";
}

// Driver Code
int main()
{
    int A[] = { 5, -3, 3, -1, 1 };

    int size = sizeof(A) / sizeof(A[0]);

    positiveProduct(A, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// index pairs in the array positive
// range product
class GFG{

public static void positiveProduct(int arr[],
                                   int n)
{
    int even_count = 0;
    int odd_count = 0;
    int total_count = 0;
    int ans = 0;

    for(int i = 0; i < n; i++)
    {

       // Condition if number of
       // negative elements is even
       // then increase even_count
       if (total_count % 2 == 0)
       {
           even_count++;
       }

       // Otherwise increase odd_count
       else
       {
           odd_count++;
       }

       // Condition if current element
       // is negative
       if (arr[i] < 0)
       {
           total_count++;
       }

       // Condition if number of
       // negative elements is even
       // then add even_count
       // in answer
       if (total_count % 2 == 0)
           ans += even_count;

       // Otherwise add odd_count
       // in answer
       else
           ans += odd_count;
    }
    System.out.println(ans);

}

// Driver Code   
public static void main(String[] args)
{
    int A[] = { 5, -3, 3, -1, 1 };
    int size = A.length;

    positiveProduct(A, size);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the count
# of index pairs in the array
# positive range product
def positiveProduct(arr, n):

    even_count = 0
    odd_count = 0
    total_count = 0
    ans = 0

    for i in range(n):

        # Condition if number of
        # negative elements is even
        # then increase even_count
        if(total_count % 2 == 0):
            even_count += 1

        # Otherwise increase odd_count
        else:
            odd_count += 1

        # Condition if current element
        # is negative
        if(arr[i] < 0):
            total_count += 1

        # Condition if number of
        # negative elements is even
        # then add even_count
        # in answer
        if(total_count % 2 == 0):
            ans += even_count

        # Otherwise add odd_count
        # in answer
        else:
            ans += odd_count

    print(ans)

# Driver Code
if __name__ == '__main__':

    A = [ 5, -3, 3, -1, 1 ]
    size = len(A)

    positiveProduct(A, size)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to find the count of
// index pairs in the array positive
// range product
using System;

class GFG{

public static void positiveProduct(int []arr,
                                   int n)
{
    int even_count = 0;
    int odd_count = 0;
    int total_count = 0;
    int ans = 0;

    for(int i = 0; i < n; i++)
    {

       // Condition if number of
       // negative elements is even
       // then increase even_count
       if (total_count % 2 == 0)
       {
           even_count++;
       }

       // Otherwise increase odd_count
       else
       {
           odd_count++;
       }

       // Condition if current element
       // is negative
       if (arr[i] < 0)
       {
           total_count++;
       }

       // Condition if number of
       // negative elements is even
       // then add even_count
       // in answer
       if (total_count % 2 == 0)
           ans += even_count;

       // Otherwise add odd_count
       // in answer
       else
           ans += odd_count;
    }
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 5, -3, 3, -1, 1 };
    int size = A.Length;

    positiveProduct(A, size);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the count of
// index pairs in the array positive
// range product
function positiveProduct(arr,n)
{
    let even_count = 0;
    let odd_count = 0;
    let total_count = 0;
    let ans = 0;

    for(let i = 0; i < n; i++)
    {

    // Condition if number of
    // negative elements is even
    // then increase even_count
    if (total_count % 2 == 0)
    {
        even_count++;
    }

    // Otherwise increase odd_count
    else
    {
        odd_count++;
    }

    // Condition if current element
    // is negative
    if (arr[i] < 0)
    {
        total_count++;
    }

    // Condition if number of
    // negative elements is even
    // then add even_count
    // in answer
    if (total_count % 2 == 0)
        ans += even_count;

    // Otherwise add odd_count
    // in answer
    else
        ans += odd_count;
    }
    document.write(ans);

}

// Driver Code   

    let A = [5, -3, 3, -1, 1 ];
    let size = A.length;

    positiveProduct(A, size);

// This code is contributed by sravan kumar Gottumukkala

</script>
```

**Output:** 

```
7
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(1)*