# 在一定的约束条件下将白色和黑色的物体分成最大的组

> 原文:[https://www . geeksforgeeks . org/在一定限制下将黑白对象分配到最大组/](https://www.geeksforgeeks.org/distribute-the-white-and-black-objects-into-maximum-groups-under-certain-constraints/)

给定 **W** 白色物体和 **B** 黑色物体以及一个数字 **D，**任务是找出是否有可能将白色和黑色物体分配到最大数量的组中，使得每个组包含每种类型物体中的至少一个，并且每个组中不同类型物体的数量之间的差异不超过 **D.**

**示例:**

> **输入:** W=2，B=5，D=2
> **输出:**
> YES
> **说明:**
> 分布可以如下:{W，B，B，B}和{W，B，B}。
> 每组至少包含一个 W 和至少一个 B，每组的差值不超过 d。
> 
> **输入:** W=2，B=7，D = 2
> T3】输出:T5】否

**方法:**最大可能组数为**分钟(W，B)。**我们考虑一下， **W < B** ，那么，最多可以有 **W** 组，每组只有一个 **W** 。每组 **B** 的最大数量为 **D+1** 。因此 **B** 的最大值应小于 **W*(D+1)。**这是唯一的必要条件。按照以下步骤解决问题:

*   如果 **W** 大于 **B** ，则交换 **W** 和 **B** 。(交换不会改变答案)
*   检查 **B** 是否大于 **W*(D+1)** ，打印否
*   否则，打印是。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to check if it is possible to distribute W and B
// into maximum groups possible
void isPossible(int W, int B, int D)
{
    // If W is greater than B, swap them
    if (W > B)
        swap(W, B);
    // Distribution is not possible
    if (B > W * (D + 1))
        cout << "NO" << endl;
    // Distribution is possible
    else
        cout << "YES" << endl;
}
// Driver code
int main()
{
    // Input
    int W = 2;
    int B = 5;
    int D = 2;

    // Function call
    isPossible(W, B, D);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to check if it is possible to distribute W
  // and B
  // into maximum groups possible
  public static void isPossible(int W, int B, int D)
  {

    // If W is greater than B, swap them
    if (W > B) {
      int temp = W;
      W = B;
      B = temp;
    }

    // Distribution is not possible
    if (B > W * (D + 1))
      System.out.println("NO");

    // Distribution is possible
    else
      System.out.println("YES");
  }

  // Driver code
  public static void main(String[] args)
  {

    // Input
    int W = 2;
    int B = 5;
    int D = 2;

    // Function call
    isPossible(W, B, D);

  }
}

 // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if it is possible to distribute W and B
# into maximum groups possible
def isPossible(W, B, D):
    # If W is greater than B, swap them
    if (W > B):
        temp = W
        W = B
        B = temp

    # Distribution is not possible
    if (B > W * (D + 1)):
        print("NO")
    # Distribution is possible
    else:
        print("YES")

# Driver code
if __name__ == '__main__':
    # Input
    W = 2
    B = 5
    D = 2

    # Function call
    isPossible(W, B, D)

    # This code is contributed by bgangwar59.

```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to check if it is possible to distribute W
    // and B
    // into maximum groups possible
    static void isPossible(int W, int B, int D)
    {

        // If W is greater than B, swap them
        if (W > B) {
            int temp = W;
            W = B;
            B = temp;
        }

        // Distribution is not possible
        if (B > W * (D + 1))
            Console.WriteLine("NO");

        // Distribution is possible
        else
            Console.WriteLine("YES");
    }

    // Driver code
    public static void Main()
    {

        // Input
        int W = 2;
        int B = 5;
        int D = 2;

        // Function call
        isPossible(W, B, D);
    }
}

// This code is contributed by rishavmahato348.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to check if it is possible to distribute W and B
      // into maximum groups possible
      function isPossible(W, B, D)
      {

          // If W is greater than B, swap them
          if (W > B)
          {
              let temp = W;
              W = B;
              B = temp;
          }

          // Distribution is not possible
          if (B > W * (D + 1))
              document.write("NO");

          // Distribution is possible
          else
              document.write("YES");
      }
      // Driver code

      // Input
      let W = 2;
      let B = 5;
      let D = 2;

      // Function call
      isPossible(W, B, D);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
YES
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)