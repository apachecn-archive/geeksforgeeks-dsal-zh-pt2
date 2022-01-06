# 元素在范围[0]内的 n 大小数组的计数，(2^K)-1)具有最大和&位和 0

> 原文:[https://www . geesforgeks . org/带范围内元素的 n 大小数组计数-0-2k-1-具有最大按位和-0/](https://www.geeksforgeeks.org/count-of-arrays-of-size-n-with-elements-in-range-0-2k-1-having-maximum-sum-bitwise-and-0/)

给定两个整数 **N** 和 **K** ，任务是找到所有元素的最大和&**为 0 的所有可能大小数组 **N** 的计数。另外，元素应该在 **0** 到 **2 <sup>K</sup> -1** 的范围内。**

****示例:****

> ****输入:** *N = 3，K = 2*
> T5】输出: 9
> **说明:**2<sup>2</sup>–1 = 3，所以数组的元素应该在 0 到 3 之间。所有可能的数组都是- [3，3，0]，[1，2，3]，[3，0，3]，[0，3，3]，[1，3，2]，[2，1，3]，[2，3，1]，[3，1，2]，[3，2，1]所有数组的按位“与”都是 0 &并且总和= 6 是最大值**
> 
> ****输入** : N = 2，K = 2
> **输出** : 4
> **解释**:所有可能的数组都是–[ 3，0]，[0，3]，[1，2]，[2，1]**

****进场:**为了更好地理解进场，请参考以下步骤:**

*   **由于最大可能元素是**(2<sup>K</sup>–1)**，数组的大小是 **N** ，所以如果数组的所有元素都等于最大元素，那么总和将是**最大**，即**N *(2<sup>K</sup>–1)**=**N *(2<sup>0</sup>+2<sup>1</sup>+………..+2<sup>K–1</sup>)**。请记住，在(2<sup>K</sup>–1)中有 K 位，并且所有位都已设置。**
*   **所以现在要使所有元素的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 0，我们必须**至少在一个元素中取消设置**位。此外，我们**不能在超过 1 个元素**中取消相同的位，因为在这种情况下**和**将不是**最大值**。**
*   **将一个元素中的每个位清零后，最大可能总和= N *(2<sup>0</sup>+2<sup>1</sup>+……+2<sup>K–1</sup>)–(2<sup>0</sup>+2<sup>1</sup>+……。+2<sup>K–1</sup>)=(N * 2<sup>K-1</sup>)–2<sup>K–1</sup>=**(N–1)*(2<sup>K</sup>–1)**。**
*   **现在的目标是找到所有的**方法**，通过这些方法我们可以**至少在**一个元素中取消**所有的 **K 位**。您可以看到，对于取消设置单个位，您有 N 个选项，即您可以在 N 个元素中的任何一个元素中取消设置它。因此**解除 K 位的总方式为 N <sup>K</sup>** 。这是我们的最终答案。****

**插图:**

> **设 N = 3，K = 3**
> 
> *   **使数组的所有元素等于 2<sup>3</sup>–1 = 7。数组将是[7，7，7]。取所有元素的二进制表示:[111，111，111]。**
> *   **恰好在一个元素中取消设置每个位。假设我们取消第一个元素的第三位和第二个元素的前两位。数组变成[110，001，111] = [6，1，7]。这是有效数组之一。您可以用这种方式生成所有数组。**
> *   **数组总数为 3 <sup>3</sup> = 27。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Iterative Function to calculate
// (x^y) in O(log y)
int power(int x, int y)
{

    // Initialize answer
    int res = 1;

    // Check till the number becomes zero
    while (y) {

        // If y is odd, multiply x with result
        if (y % 2 == 1)
            res = (res * x);

        // y = y/2
        y = y >> 1;

        // Change x to x^2
        x = (x * x);
    }
    return res;
}

// Driver Code
int main()
{
    int N = 3, K = 2;
    cout << power(N, K);
    return 0;
}
```

****Output**

```
9
```** 

*****时间复杂度*** : O(logK)
***辅助空间*** : O(1)**