# N 个元素可以组成两个不同集合的方式数，每个集合包含 N/2 个元素

> 原文:[https://www . geesforgeks . org/count-of-way-n-elements-can-form-两个不同的集合-包含-n-2-elements-每个/](https://www.geeksforgeeks.org/count-of-ways-n-elements-can-form-two-different-sets-containing-n-2-elements-each/)

给定一个数字 **N** ，代表元素的个数，等于 **2K** ，任务是找出这些元素可以组成 2 个集合的方式数，每个集合包含 **K** 个元素。

**示例:**

> ***输入:N =** 4*
> ***输出:** 3*
> ***解释:**由 2 (= N/2)个元素组成的 3 个集合是:*
> *【1，2】、【3，4】*
> *【1，3】、【2，4】*
> *【1，4】、【2，3】*
> 
> ***输入:N =**20*
> T5**输出:** 12164510040883200

**方法:**需要注意的是，为了选择每组的元素，必须应用组合的概念。
众所周知，从总共 **n 个**事物中选择 **r** 事物的方法的数量由下式给出:

> <sup>nC</sup> <sub><sup>r = n！/(n-r)！*r！</sup></sub>

现在，可以修改上面的公式来解决给定的问题:

*   这里，必须从 **N** 元素中选择 **N/2** 元素来形成每一组。因此， **r** = **N/2** 。
*   需要注意的是，同一元素不能同时出现在两组中。所以，**<sup>n</sup>C<sub>r</sub>**<sub>的公式必须除以 2。</sub>
*   另外，每组中出现的元素可以在**中自行排列(N/2-1)！**方式。由于有两个集合，公式将乘以这个因子两次。

得到的修正公式由下式给出:

> **路数= ((N！/(N–r)！*r！)/2)*(N/2–1)！*(N/2–1)！**其中 **r = N / 2**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the factorial
// of values
long long int fact(long long int N)
{
    // Factorial of 0 is 1
    if (N == 0) {
        return 1;
    }
    else {

        // Recursive function call
        return N * fact(N - 1);
    }
}

// Driver Code
int main()
{

    // Given input
    int N = 20;

    // Function Call
    cout << (fact(N) / (fact(N / 2)
                        * fact(N - N / 2)))
                / 2
                * fact(N / 2 - 1)
                * fact(N / 2 - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
class GFG
{

    // Function to find the factorial
    // of values
    static long fact(long N)
    {

        // Factorial of 0 is 1
        if (N == 0) {
            return 1;
        }
        else {

            // Recursive function call
            return N * fact(N - 1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given input
        int N = 20;

        // Function Call
        System.out.println(
            (fact(N) / (fact(N / 2) * fact(N - N / 2))) / 2
            * fact(N / 2 - 1) * fact(N / 2 - 1));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the factorial
# of values
def fact(N):

    # Factorial of 0 is 1
    if (N == 0):
        return 1

    else:

        # Recursive function call
        return N * fact(N - 1)

# Driver Code
if __name__ == "__main__":

    # Given input
    N = 20

    # Function Call
    print(int((fact(N) / (fact(N / 2) * fact(N - N / 2))) /
              2 * fact(N / 2 - 1) * fact(N / 2 - 1)))

# This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
public class GFG
{

    // Function to find the factorial
    // of values
    static long fact(long N)
    {

        // Factorial of 0 is 1
        if (N == 0) {
            return 1;
        }
        else {

            // Recursive function call
            return N * fact(N - 1);
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // Given input
        int N = 20;

        // Function Call
        Console.WriteLine(
            (fact(N) / (fact(N / 2) * fact(N - N / 2))) / 2
            * fact(N / 2 - 1) * fact(N / 2 - 1));
    }
}

// This code is contributed AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the factorial
// of values
function fact(N)
{

    // Factorial of 0 is 1
    if (N == 0) {
        return 1;
    }
    else {

        // Recursive function call
        return N * fact(N - 1);
    }
}

// Driver Code

// Given input
let N = 20;

// Function Call
document.write((fact(N) / (fact(N / 2)
                * fact(N - N / 2)))
            / 2
            * fact(N / 2 - 1)
            * fact(N / 2 - 1));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
12164510040883200
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)