# 计算生成的大小为 N * N 的矩阵中元素的出现次数，以使每个元素等于其索引的乘积| Set-2

> 原文:[https://www . geeksforgeeks . org/count-size-n-n 矩阵中元素的出现次数-生成-每个元素等于其索引的乘积-set-2/](https://www.geeksforgeeks.org/count-occurrences-of-an-element-in-a-matrix-of-size-n-n-generated-such-that-each-element-is-equal-to-product-of-its-indices-set-2/)

-给定两个正整数 **N** 和 **X** ，任务是在生成的**N**-长度 [<u>正方形矩阵</u>](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) 中计算给定整数 **X** 的出现次数，使得矩阵的每个元素都等于其行和列索引的乘积(*基于 1 的索引*)。

**示例:**

> ***输入:** N = 5，X = 6*
> ***输出:** 2*
> ***解释:***
> *形成的 2D 阵等于:*
> *1 2 3 4 5*
> T21】2 4 6 8 10
> *3 6 9 12 15*
> 
> ****输入:** N = 7，X = 12*
> T5**输出:** 4*

***天真法:**参考本文[](https://www.geeksforgeeks.org/count-occurrences-of-an-element-in-a-matrix-of-size-n-n-generated-such-that-each-element-is-equal-to-product-of-its-indices/)<u>最简单的解决问题的方法是通过将行索引和列索引相乘来构造给定的矩阵，以获得每个矩阵元素，并计算 **X.** 的出现次数</u>*

*<u>***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*</u>*

*<u>**高效方法:**这个想法是基于这样的观察:第 **i <sup>第</sup>T5<sup>T7】行包含了**【1，N】**范围内的所有 **i** 的倍数。因此， **X** 出现在 **i <sup>第</sup>** 行，当且仅当 **X** 正好可被 **i** 整除，且 **X / i** 应小于或等于 **N** 。如果发现为真，则将计数增加 1。按照以下步骤解决问题:</sup>**</u>*

*   *<u>初始化一个变量，比如**计数**，将 **X** 的出现次数存储在生成的矩阵中。</u>*
*   *<u>[<u>使用变量 **i** 迭代范围</u>](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:

    *   如果 **X** 可以被 **i** 整除，将 **X** / **i** 的商存储在一个变量中，比如说 **b** 。
    *   如果 **b** 的值落在**【1，N】**的范围内，那么将**计数**增加 **1** 。</u>* 
*   *<u>完成上述步骤后，打印**计数**的值作为结果。</u>*

*<u>下面是上述方法的实现:</u>*

## *<u>C++</u>*

```
*<u>// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the occurrences
// of X in the generated square matrix
int countOccurrences(int n, int x)
{
    // Store the required result
    int count = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= n; i++) {

        // Check if x is a
        // multiple of i or not
        if (x % i == 0) {

            // Check if the other multiple
            // exists in the range or not
            if (x / i <= n)
                count++;
        }
    }

    // Print the result
    cout << count;
}

// Driver Code
int main()
{
    int N = 7, X = 12;
    countOccurrences(N, X);

    return 0;
}</u>*
```

## *<u>Java 语言(一种计算机语言，尤用于创建网站)</u>*

```
*<u>// Java program for the above approach

class GFG{

// Function to count the occurrences
// of X in the generated square matrix
static void countOccurrences(int n, int x)
{
    // Store the required result
    int count = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= n; i++) {

        // Check if x is a
        // multiple of i or not
        if (x % i == 0) {

            // Check if the other multiple
            // exists in the range or not
            if (x / i <= n)
                count++;
        }
    }

    // Print the result
    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
    int N = 7, X = 12;
    countOccurrences(N, X);

}
}

// This code contributed by shikhasingrajput</u>*
```

## *<u>蟒蛇 3</u>*

```
*<u># Python3 program for the above approach

# Function to count the occurrences
# of X in the generated square matrix
def countOccurrences(n, x):

    # Store the required result
    count = 0

    # Iterate over the range [1, N]
    for i in range(1, n + 1):

        # Check if x is a
        # multiple of i or not
        if (x % i == 0):

            # Check if the other multiple
            # exists in the range or not
            if (x // i <= n):
                count += 1

    # Print the result
    print(count)

# Driver Code
if __name__ == "__main__":

    N = 7
    X = 12

    countOccurrences(N, X)

# This code is contributed by ukasp</u>*
```

## *<u>C#</u>*

```
*<u>// C# program for the above approach
using System;
class GFG
{

  // Function to count the occurrences
  // of X in the generated square matrix
  static void countOccurrences(int n, int x)
  {
    // Store the required result
    int count = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= n; i++) {

      // Check if x is a
      // multiple of i or not
      if (x % i == 0) {

        // Check if the other multiple
        // exists in the range or not
        if (x / i <= n)
          count++;
      }
    }

    // Print the result
    Console.WriteLine(count);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 7, X = 12;
    countOccurrences(N, X);
  }
}

// This code is contributed by splevel62.</u>*
```

## *<u>java 描述语言</u>*

```
*<u><script>

// Javascript program for the above approach

// Function to count the occurrences
// of X in the generated square matrix
function countOccurrences(n, x)
{
    // Store the required result
    var count = 0;

    // Iterate over the range [1, N]
    for (var i = 1; i <= n; i++) {

        // Check if x is a
        // multiple of i or not
        if (x % i == 0) {

            // Check if the other multiple
            // exists in the range or not
            if (x / i <= n)
                count++;
        }
    }

    // Print the result
    document.write( count);
}

// Driver Code
var N = 7, X = 12;
countOccurrences(N, X);

</script></u>*
```

*<u>**Output:** 

```
4
```</u>* 

*<u>***时间复杂度:**O(N)*
T5**辅助空间:** O(1)</u>*