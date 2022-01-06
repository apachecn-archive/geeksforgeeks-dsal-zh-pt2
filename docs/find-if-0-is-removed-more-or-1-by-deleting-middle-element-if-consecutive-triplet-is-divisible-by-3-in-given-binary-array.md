# 在给定的二进制数组中，如果连续三元组可被 3 整除，则通过删除中间元素来查找 0 是否被移除更多或 1

> 原文:[https://www . geeksforgeeks . org/find-if-0-is-removed-more-or-1-by-deleting-middle-element-if-continuous-triple-is-除尽-in-3-给定二进制数组/](https://www.geeksforgeeks.org/find-if-0-is-removed-more-or-1-by-deleting-middle-element-if-consecutive-triplet-is-divisible-by-3-in-given-binary-array/)

给定一个二进制[数组](https://www.geeksforgeeks.org/array-data-structure/) **一个大小为 **N** 的 **1 的**和 **0 的**。如果 **a[i-1]+a[i]+a[i+1]** 可被 **3** 整除，则任务是移除一个元素。如果 **1 的**比 **0 的**多，则打印 **1** ，否则打印 **0** 。**

**示例:**

> **输入** : a[] = { 1，1，1，0，1，0，0}
> **输出** : 1
> **解释:**从左边去掉第二个 1，因为那是唯一一个(a[i]+a[i-1]+a[i+1])为%3==0 的‘1’。所以打印 1。
> 
> **输入** : a[] = { 1，1}
> **输出** : 0
> **解释**:无法移除，所以打印 0。

**方法:**这个想法是基于这样的观察:如果两个邻居都等于当前元素，因为如果 **(a[i]=a[i-1]=a[i+1])** 那么总和将总是被 **3** 整除。假设 **A** 存储 **1 的**被移除的数量， **B** 存储 **0 的**被移除的数量。如果具有元素的**等于邻居，那么如果 **a[i] =1** ，则增加 **A** ，否则增加 **B** 。如果 **A** 的计数大于 **B** ，则打印 **1** ，否则打印 **2=0** 。按照以下步骤解决问题:**

*   将变量 **A** 和 **B** 初始化为 **0** ，以存储删除的 **1** 和 **0** 的数量。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N)** ，并执行以下步骤:
    *   如果**A【I-1】、A【I】**和**A【I+1】**相等，那么如果**A【I】**等于 **1、**那么将 **A** 的值增加 **1** 否则 **B** 增加 **1。**
*   如果 **A** 大于 **B，**则打印 **1** 否则打印 **0。**

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to if more number of
// 1's are removed or 0's
void solution(vector<int> a)
{

    // Stores count of 1's removes
    int A = 0;

    // Stores count of 0's removes
    int B = 0;

    // Traverse the array
    for (int i = 1; i < a.size() - 1; i++) {

        // Check the divisibility
        if (a[i] == a[i - 1] && a[i] == a[i + 1]) {

            // Check for 1 or 0
            if (a[i] == 1)
                A++;
            else
                B++;
        }
    }

    // Print the result
    if (A > B)
        cout << ("1");
    else
        cout << ("0");
}

// Driver Code
int main()
{

    vector<int> a = { 1, 1, 1, 0, 1, 0, 0 };
    solution(a);
    return 0;
}

// This code is contributed by lokeshpotta20.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to if more number of
    // 1's are removed or 0's
    public static void solution(int[] a)
    {

        // Stores count of 1's removes
        int A = 0;

        // Stores count of 0's removes
        int B = 0;

        // Traverse the array
        for (int i = 1; i < a.length - 1; i++) {

            // Check the divisibility
            if (a[i] == a[i - 1]
                && a[i] == a[i + 1]) {

                // Check for 1 or 0
                if (a[i] == 1)
                    A++;
                else
                    B++;
            }
        }

        // Print the result
        if (A > B)
            System.out.println("1 ");
        else
            System.out.println("0 ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = { 1, 1, 1, 0, 1, 0, 0 };
        solution(a);
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to if more number of
# 1's are removed or 0's
def solution(a) :

    # Stores count of 1's removes
    A = 0;

    # Stores count of 0's removes
    B = 0;

    # Traverse the array
    for i in range(1 , len(a)- 1) :

        # Check the divisibility
        if (a[i] == a[i - 1] and a[i] == a[i + 1]) :

            # Check for 1 or 0
            if (a[i] == 1) :
                A += 1;
            else :
                B += 1;

    # Print the result
    if (A > B) :
        print("1");
    else :
        print("0");

# Driver Code
if __name__ == "__main__" :

    a = [ 1, 1, 1, 0, 1, 0, 0 ];
    solution(a);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for above approach
using System;
public class GFG {

    // Function to if more number of
    // 1's are removed or 0's
    public static void solution(int[] a)
    {

        // Stores count of 1's removes
        int A = 0;

        // Stores count of 0's removes
        int B = 0;

        // Traverse the array
        for (int i = 1; i < a.Length - 1; i++) {

            // Check the divisibility
            if (a[i] == a[i - 1]
                && a[i] == a[i + 1]) {

                // Check for 1 or 0
                if (a[i] == 1)
                    A++;
                else
                    B++;
            }
        }

        // Print the result
        if (A > B)
            Console.WriteLine("1 ");
        else
            Console.WriteLine("0 ");
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int []a = { 1, 1, 1, 0, 1, 0, 0 };
        solution(a);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Function to if more number of
// 1's are removed or 0's
function solution(a) {

  // Stores count of 1's removes
  let A = 0;

  // Stores count of 0's removes
  let B = 0;

  // Traverse the array
  for (let i = 1; i < a.length - 1; i++) {

    // Check the divisibility
    if (a[i] == a[i - 1] && a[i] == a[i + 1]) {

      // Check for 1 or 0
      if (a[i] == 1)
        A++;
      else
        B++;
    }
  }

  // Prlet the result
  if (A > B)
    document.write(("1"));
  else
    document.write(("0"));
}

// Driver Code

let a = [1, 1, 1, 0, 1, 0, 0];
solution(a);

// This code is contributed by Saurabh Jaiswal.
</script>
```

**Output**

```
1 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)