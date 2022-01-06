# 与下一个较大元素的距离

> 原文:[https://www . geeksforgeeks . org/距下一个更大元素的距离/](https://www.geeksforgeeks.org/distance-from-next-greater-element/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印每个数组元素与其下一个更大元素[的距离。对于没有下一个更大元素的数组元素，打印 0。](https://www.geeksforgeeks.org/next-greater-element/)

**示例:**

> **输入:** arr[] = {73，74，75，71，69，72，76，73}
> **输出:** {1，1，4，2，1，1，0，0}
> **解释:**
> 73 的下一个较大元素是 74，位于位置 1。距离= 1–0 = 1
> 74 的下一个较大元素是 75，位于位置 2。距离= 2–1 = 1
> 75 的下一个较大元素是 76，位于位置 6。距离= 6–2 = 4
> 71 的下一个较大元素是 72，位于位置 5。距离= 5–3 = 2
> 69 的下一个较大元素是 72，位于位置 5。距离= 5–4 = 1
> 72 的下一个较大元素是 76，位于位置 6。距离= 6–5 = 1
> 否，下一个更大的元素为 76。距离= 0
> 否，下一个更大的元素为 73。距离= 0
> 
> **输入:** arr[] = {5，4，3，2，1}
> **输出:** {0，0，0，0，0}

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，遍历其右侧以获得其[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)，并计算索引之间的差异。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效法:**对上述方法进行优化，思路是使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)寻找下一个更大的元素。
以下是步骤:

1.  维护一个**堆栈**，该堆栈将包含非递增顺序的元素。
2.  检查当前元素**arr【I】**是否大于堆栈顶部[的元素](https://www.geeksforgeeks.org/stack-top-c-stl/)。
3.  继续从顶部一个接一个地弹出堆栈中所有小于**arr【I】**的元素，并计算每个元素的距离，作为当前索引和弹出元素的索引之差。
4.  将当前元素推入堆栈，并重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include<bits/stdc++.h>
using namespace std;

vector<int> mindistance(vector<int> arr)
{
    int N = arr.size();

    // Stores the required distances
    vector<int> ans(N);
    int st = 0;

    // Maintain a stack of elements
    // in non-increasing order
    for(int i = 0; i < N - 1; i++)
    {
        if (arr[i] < arr[i + 1])
        {
            ans[i] = 1;
        }
        else
        {
            st = i + 1;
            while (st <= N - 1)
            {
                if (arr[i] < arr[st])
                {
                    ans[i] = st - i;
                    break;
                }
                else
                {
                    st++;
                }
            }
        }
    }
    return ans;
}

// Driver code
int main()
{
    vector<int> arr = { 73, 74, 75, 71,
                        69, 72, 76, 73 };

    vector<int> x = mindistance(arr);

    cout << "[";
    for(int i = 0; i < x.size(); i++)
    {
        if (i == x.size() - 1)
            cout << x[i];
        else
          cout << x[i] << ", ";
    }
    cout << "]";
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.io.*;

class GFG{

public static int[] mindistance(int[] arr)
{
    int N = arr.length;

    // Stores the required distances
    int[] ans = new int[N];
    int st = 0;

    // Maintain a stack of elements
    // in non-increasing order
    for(int i = 0; i < N - 1; i++)
    {
        if (arr[i] < arr[i + 1])
        {
            ans[i] = 1;
        }
        else
        {
            st = i + 1;
            while (st <= N - 1)
            {
                if (arr[i] < arr[st])
                {
                    ans[i] = st - i;
                    break;
                }
                else
                {
                    st++;
                }
            }
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = new int[]{ 73, 74, 75, 71,
                           69, 72, 76, 73 };

    int x[] = mindistance(arr);

    System.out.print("[");
    for(int i = 0; i < x.length; i++)
        System.out.print(x[i]+", ");

    System.out.print("]");
}
}

// This code is contributed by sai-sampath mahajan
// and ramprasad kondoju
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

def mindistance(arr, N):

    if N <= 1:
        return [0]

    # Stores the required distances
    ans = [0 for i in range(N)]
    st = [0]

    # Maintain a stack of elements
    # in non-increasing order
    for i in range(1, N): 

        # If the current element exceeds
        # the element at the top of the stack
        while(st and arr[i] > arr[st[-1]]): 
            pos = st.pop()
            ans[pos] = i - pos

        # Push the current index to the stack
        st.append(i)

    return ans

# Given array
arr = [73, 74, 75, 71, 69, 72, 76, 73]
N = len(arr)

# Function call
print(mindistance(arr, N))
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

public static int[] mindistance(int[] arr)
{
    int N = arr.Length;

    // Stores the required distances
    int[] ans = new int[N];
    int st = 0;

    // Maintain a stack of elements
    // in non-increasing order
    for(int i = 0; i < N - 1; i++)
    {
        if (arr[i] < arr[i + 1])
        {
            ans[i] = 1;
        }
        else
        {
            st = i + 1;
            while (st <= N - 1)
            {
                if (arr[i] < arr[st])
                {
                    ans[i] = st - i;
                    break;
                }
                else
                {
                    st++;
                }
            }
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = new int[]{ 73, 74, 75, 71,
                           69, 72, 76, 73 };

    int []x = mindistance(arr);

    Console.Write("[");
    for(int i = 0; i < x.Length; i++)
        Console.Write(x[i]+", ");

    Console.Write("]");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

function mindistance(arr)
{
    let N = arr.length;

    // Stores the required distances
    let ans = [];
    let st = 0;

    // Maintain a stack of elements
    // in non-increasing order
    for(let i = 0; i < N - 1; i++)
    {
        if (arr[i] < arr[i + 1])
        {
            ans[i] = 1;
        }
        else
        {
            st = i + 1;
            while (st <= N - 1)
            {
                if (arr[i] < arr[st])
                {
                    ans[i] = st - i;
                    break;
                }
                else
                {
                    st++;
                }
            }
        }
    }
    return ans;
}

// Driver code

    let arr = [ 73, 74, 75, 71,
                           69, 72, 76, 73 ];

    let x = mindistance(arr);

    document.write("[");
    for(let i = 0; i < x.length; i++)
        document.write(x[i]+", ");

    document.write("]");

// This code is contributed by target_2.
</script>
```

**Output:** 

```
[1, 1, 4, 2, 1, 1, 0, 0]
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)