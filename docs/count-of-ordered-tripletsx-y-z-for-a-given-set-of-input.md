# 给定一组输入的有序三元组(x，y，z)的计数

> 原文:[https://www . geeksforgeeks . org/给定输入集的有序三重计数 x-y-z/](https://www.geeksforgeeks.org/count-of-ordered-tripletsx-y-z-for-a-given-set-of-input/)

给定三个整数 N，M 和 p，任务是计算形式(x，y，z)的可能的**有序三元组**的数量，其中

> 1 ≤ x ≤ N，1 ≤ y ≤ M 和 1 ≤ z ≤ P

由于此计数可能非常大，请以 **10 <sup>9</sup> + 7** 为模返回答案。

**示例:**

> **输入:** N = 3，M = 3，P = 3
> **输出:** 6
> **解释:**可能的三胞胎是:
> (1，2，3)，(1，3，2)，(2，1，3)，(2，3，1)，(3，1，2)，(3，2)，(3，2，2，1)
> 
> **输入:** N = 1，M = 2，P = 3
> **输出:** 1
> **说明:**只能有一个三元组(1，2，3)

**方法:**解决方案基于以下观察。

> *   After sorting these three numbers in ascending order, say that they are A, B and C respectively.
> *   So there's a to choose the element first.
> *   This choice is not suitable for choosing the second one now. For the second one, there are (b–1) options.
> *   Now these two options are not available for the last one. Therefore, there are only (c–2) options for the third option.
> *   Therefore, the total number of possibilities is a * (b–1) * (c–2).

按照下面提到的步骤来实现上述观察。

*   按升序对三个输入进行排序。让排序顺序为(N1、N2、N3)。
*   现在应用从观察中导出的公式来得到最终答案。
*   返回最终答案模 10 <sup>9</sup> + 7。

下面是上述方法的实现。

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;
const unsigned int mod = 1000000007;

// Function to count the
// total number of possible triplets
long long int solve(int N, int M, int P)
{
    int nums[] = { N, M, P };
    sort(nums, nums + 3);
    long long int ans = ((nums[0] *
                         (nums[1] - 1)) % mod
                         * (nums[2] - 2) %
                         mod)% mod;
    return ans;
}

// Driver code
int main()
{
    int N = 3, M = 3, P = 3;
    long long int ans = solve(N, M, P);
    cout << ans << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach

// Importing Arrays class from the utility class
import java.util.Arrays;
class GFG
{

  public static long mod = 1000000007;

  // Function to count the
  // total number of possible triplets
  static long solve(int N, int M, int P)
  {
    int nums[] = { N, M, P };
    Arrays.sort(nums);
    long ans = ((nums[0] * (nums[1] - 1)) % mod
                * (nums[2] - 2) % mod)
      % mod;
    return ans;
  }

  // Driver method
  public static void main(String[] args)
  {
    int N = 3, M = 3, P = 3;
    long ans = solve(N, M, P);

    System.out.println(ans);

  }
}

// This code is contributed by rakeshsahni
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the total number of
# possible triplets
def solve(N, M, P):

    mod = 1000000007
    nums = [ N, M, P ]
    nums.sort()
    ans = ((nums[0] * (nums[1] - 1)) % mod *
           (nums[2] - 2) % mod) % mod

    return ans

# Driver Code
if __name__ == "__main__":

    N, M, P = 3, 3, 3

    ans = solve(N, M, P)
    print(ans)

# This code is contributed by Abhishek Thakur.
```

## java 描述语言

```
  <script>
      // JavaScript code for the above approach

      let mod = 1000000007;

      // Function to count the
      // total number of possible triplets
      function solve(N, M, P) {
          let nums = [N, M, P];
          nums.sort(function (a, b) { return a - b })
          let ans = ((nums[0] *
              (nums[1] - 1)) % mod
              * (nums[2] - 2) %
              mod) % mod;
          return ans;
      }

      // Driver code
      let N = 3, M = 3, P = 3;
      let ans = solve(N, M, P);
      document.write(ans + '<br>')

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
6
```

***时间复杂度:*** O(1)
***辅助空间:*** O(1)