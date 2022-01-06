# 对不同的可能对进行计数，使得来自 A 的元素大于来自 B 的元素

> 原文:[https://www . geeksforgeeks . org/count-of-distinct-可能的对-这样-a 中的元素大于 b 中的元素/](https://www.geeksforgeeks.org/count-of-distinct-possible-pairs-such-that-the-element-from-a-is-greater-than-the-element-from-b/)

给定两个相等长度的给定数组 **A** 和 **B** ，任务是找到可以选择的不同元素对的最大数量，使得来自 A 的元素严格大于来自 B 的元素

**示例:**

> **输入:**
> A[]={20，30，50}，B[]={25，60，40}
> **输出:** 2
> **解释:**
> (30，25)和(50，40)是两个可能的对。
> 
> **输入:**
> A[]={20，25，60}，B[]={25，60，40}
> **输出:** 1
> **说明:**
> (60，25)或(60，40)可以是所需的对。

**方法:**为了解决这个问题，我们需要采用以下方法:

*   对两个数组进行排序。
*   遍历数组 A 的整个长度，检查 A 中的当前元素是否大于 B 中当前指向 B 的元素
*   如果是，指向两个数组中的下一个元素。否则，移动到 A 中的下一个元素，检查它是否大于当前指向 b 的元素。
*   在数组 A 的整个遍历之后，数组 B 中遍历的元素数量给出了所需的答案。

> **图解:**
> 让我们考虑以下两个数组:
> A[] = {30，28，45，22}，B[] = {35，25，22，48}
> 排序后，数组看起来是
> A[] = {22，28，30，45}，B[] = {22，25，35，48}
> 第一次迭代后，由于 A[0]不大于 B[0]，我们移到 A
> 第二次迭代后，我们移到 B[1]，因为 A[1]大于 B[0]。
> 第三次迭代后，我们移到 B[2]，因为 A[2]大于 B[1]。
> 同样，A[3]大于 B[2]，我们移至 B[3]。
> 因此，B 中遍历的元素数，即 3，就是最终答案。
> 可能的配对是(28，22)，(30，25)，(45，35)。

下面是上述方法的实现:

## C++

```
// C++ Program to count number of distinct
// pairs possible from the two arrays
// such that element selected from one array is
// always greater than the one selected from
// the other array

#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of pairs
int countPairs(vector<int> A,
                    vector<int> B)
{
    int n = A.size();

    sort(A.begin(),A.end());
    sort(B.begin(),B.end());

    int ans = 0, i;
    for (int i = 0; i < n; i++) {
        if (A[i] > B[ans]) {
            ans++;
        }
    }

    return ans;
}

// Driver code
int main()
{
    vector<int> A = { 30, 28, 45, 22 };
    vector<int> B = { 35, 25, 22, 48 };

    cout << countPairs(A,B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of distinct
// pairs possible from the two arrays such
// that element selected from one array is
// always greater than the one selected from
// the other array
import java.util.*;

class GFG{

// Function to return the count
// of pairs
static int countPairs(int [] A,
                      int [] B)
{
    int n = A.length;
    int ans = 0;

    Arrays.sort(A);
    Arrays.sort(B);

    for(int i = 0; i < n; i++)
    {
       if (A[i] > B[ans])
       {
           ans++;
       }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int [] A = { 30, 28, 45, 22 };
    int [] B = { 35, 25, 22, 48 };

    System.out.print(countPairs(A, B));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to count number of distinct
# pairs possible from the two arrays
# such that element selected from one array is
# always greater than the one selected from
# the other array

# Function to return the count
# of pairs
def countPairs(A, B):

    n = len(A)

    A.sort()
    B.sort()

    ans = 0
    for i in range(n):
        if(A[i] > B[ans]):
            ans += 1

    return ans

# Driver code
if __name__ == '__main__':
    A = [30, 28, 45, 22]
    B = [35, 25, 22, 48]

    print(countPairs(A, B))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to count number of distinct
// pairs possible from the two arrays such
// that element selected from one array is
// always greater than the one selected from
// the other array
using System;
class GFG{

// Function to return the count
// of pairs
static int countPairs(int [] A,
                      int [] B)
{
    int n = A.Length;
    int ans = 0;

    Array.Sort(A);
    Array.Sort(B);

    for(int i = 0; i < n; i++)
    {
        if (A[i] > B[ans])
        {
            ans++;
        }
    }
    return ans;
}

// Driver code
public static void Main()
{
    int []A = { 30, 28, 45, 22 };
    int []B = { 35, 25, 22, 48 };

    Console.Write(countPairs(A, B));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to count number of distinct
// pairs possible from the two arrays such
// that element selected from one array is
// always greater than the one selected from
// the other array

// Function to return the count
// of pairs
function countPairs(A, B)
{
    let n = A.length;
    let ans = 0;

    A.sort();
    B.sort();

    for(let i = 0; i < n; i++)
    {
       if (A[i] > B[ans])
       {
           ans++;
       }
    }
    return ans;
}

// Driver Code

    let A = [ 30, 28, 45, 22 ];
    let B = [ 35, 25, 22, 48 ];

    document.write(countPairs(A, B));

</script>
```

**Output:** 

```
3
```

时间复杂度:O(n * log n)

辅助空间:0(1)