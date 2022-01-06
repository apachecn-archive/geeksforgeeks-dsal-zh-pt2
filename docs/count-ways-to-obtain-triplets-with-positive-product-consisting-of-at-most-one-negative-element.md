# 计数获得正乘积至多由一个负元素组成的三元组的方法

> 原文:[https://www . geeksforgeeks . org/count-获得正积三元组的方法-最多由一个负元素组成/](https://www.geeksforgeeks.org/count-ways-to-obtain-triplets-with-positive-product-consisting-of-at-most-one-negative-element/)

给定一个大小为**N**(*1≤N≤10<sup>5</sup>*)的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到选择三元组 **i、j** 和 **k** 的方法数，使得 **i < j < k** 和产品 **arr[i] * arr[j] * arr[k]**
***注:**每个三元组最多可由**一个负元素组成。*

**示例:**

> ***输入:** arr[] = {2，5，-9，-3，6}*
> ***输出:** 1*
> ***解释:**获得满足给定条件的三元组 I、j 和 k 的方法总数为 1 {0，1，4}。*
> 
> ***输入:** arr[] = {2，5，6，-2，5}*
> ***输出:** 4*
> ***解释:**获得满足给定条件的三元组 I、j 和 k 的方法总数为 4 {0，1，2}、{0，1，4}、{1，2，4}和{0，2，4}。*

**方法:**三元组的所有可能组合如下:

*   #负元素或 2 个负元素和 1 个正元素。这两种组合都不能被认为是三元组中最大允许的负元素是 1。
*   2 个负( *-ve* )元素和 1 个正( *+ve)* 元素。因为三重态的乘积将是负的，所以不能考虑三重态。
*   3 个积极因素。

按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)统计正数组元素的频率，说 **freq** 。
*   使用公式[PnC](https://www.geeksforgeeks.org/mathematics-pnc-binomial-coefficients/)=<sup>N</sup>C<sub>3</sub>**=(N *(N–1)*(N–2))/6**从数组元素的数量中选择有效三元组的方法计数。将获得的计数加到答案上。
*   打印获得的计数。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// possible number of triplets
long long int possibleTriplets(int arr[], int N)
{
    int freq = 0;
    // counting frequency of positive numbers
    // in array

    for (int i = 0; i < N; i++) {

        // If current array
        // element is positive
        if (arr[i] > 0) {

            // Increment frequency
            freq++;
        }
    }

    // Select a triplet from freq
    // elements such that i < j < k.
    return (freq * 1LL * (freq - 1)
            * (freq - 2))
           / 6;
}

// Driver Code
int main()
{
    int arr[] = { 2, 5, -9, -3, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << possibleTriplets(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to calculate
// possible number of triplets
static int possibleTriplets(int arr[], int N)
{
    int freq = 0;

    // counting frequency of positive numbers
    // in array
    for (int i = 0; i < N; i++)
    {

        // If current array
        // element is positive
        if (arr[i] > 0)
        {

            // Increment frequency
            freq++;
        }
    }

    // Select a triplet from freq
    // elements such that i < j < k.
    return (int) ((freq * 1L * (freq - 1)
            * (freq - 2))
           / 6);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 5, -9, -3, 6 };
    int N = arr.length;
    System.out.print(possibleTriplets(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to calculate
# possible number of triplets
def possibleTriplets(arr, N):
    freq = 0

    # counting frequency of positive numbers
    # in array
    for i in range(N):

        # If current array
        # element is positive
        if (arr[i] > 0):

            # Increment frequency
            freq += 1

    # Select a triplet from freq
    # elements such that i < j < k.
    return (freq * (freq - 1) * (freq - 2)) // 6

# Driver Code
if __name__ == '__main__':
    arr = [2, 5, -9, -3, 6]
    N = len(arr)

    print(possibleTriplets(arr, N))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# Program to implement
// the above approach
using System;

public class GFG
{

// Function to calculate
// possible number of triplets
static int possibleTriplets(int []arr, int N)
{
    int freq = 0;

    // counting frequency of positive numbers
    // in array
    for (int i = 0; i < N; i++)
    {

        // If current array
        // element is positive
        if (arr[i] > 0)
        {

            // Increment frequency
            freq++;
        }
    }

    // Select a triplet from freq
    // elements such that i < j < k.
    return (int) ((freq * 1L * (freq - 1)
            * (freq - 2)) / 6);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 5, -9, -3, 6 };
    int N = arr.Length;
    Console.Write(possibleTriplets(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to calculate
// possible number of triplets
function possibleTriplets(arr, N)
{
    var freq = 0;
    // counting frequency of positive numbers
    // in array

    for (var i = 0; i < N; i++) {

        // If current array
        // element is positive
        if (arr[i] > 0) {

            // Increment frequency
            freq++;
        }
    }

    // Select a triplet from freq
    // elements such that i < j < k.
    return (freq * 1 * (freq - 1)
            * (freq - 2))
        / 6;
}

// Driver Code
var arr = [ 2, 5, -9, -3, 6 ];
var N = arr.length;
document.write( possibleTriplets(arr, N));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)