# 尽量减少获得所有可能值所需的硬币，直到 N

> 原文:[https://www . geesforgeks . org/minimum-coins-需要获取所有可能的值-高达 n/](https://www.geeksforgeeks.org/minimize-coins-required-to-obtain-all-possible-values-up-to-n/)

给定一个整数 **N** ，任务是找到 **{1，2，5}** 值硬币的最小数量，以便可以形成范围**【1，N】**中所有可能值的变化，并且不可能获得值 **N** 。

**示例:**

> **输入:** N = 8
> **输出:**
> 5 值硬币计数:0
> 2 卢比硬币计数:3
> 1 卢比硬币计数:2
> **说明:**
> 1 分钱所需硬币= 1
> 2 分钱所需硬币= 1
> 3 分钱所需硬币= 2
> 4 分钱所需硬币= 2
> 5 分钱所需硬币= 3
> 6 分钱所需硬币
> 
> **输入:**N = 17
> T3】输出:T5】5 卢比硬币计数:2
> 2 卢比硬币计数:3
> 1 卢比硬币计数:1

**方法:**使用贪婪技术可以解决问题。这一想法基于以下观察:

> 范围[1，N]中的任何数字 X 都可以表示为
> X = 5 *(整数)+ Y *(整数)
> Y 是范围[0，4]
> 中的值之一

按照以下步骤解决问题:

*   初始化三个变量，比如 **F、**T、 **O** ，存储 **5** 、 **2** 和 **1** 价值硬币的计数。
*   使用**F =(N–4)/5 计算 **5** 值硬币的数量。**
*   如果(N–5 * F)为偶数，则一枚有价硬币的计数可计算为 **O = 1** 。
*   否则，一枚有价硬币的计数可计算为 **O = 2** 。
*   计算两个有价硬币的计数可以计算为**T =(N–5 * F–O)/2。**
*   最后，打印 **F、**T、 **O、**的值

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of {1, 2, 5}
// valued coins required to make a change of
// all values in the range [1, N]
void find(int N)
{
  int T, F, O;

  // Number of 5 valueds coins required
  F = int((N - 4) / 5);

  // Number of 1 valued coins required
  if (((N - 5 * F) % 2) == 0)
  {
    O = 2;
  }

  else
  {
    O = 1 ;
  }

  // Number of 2 valued coins required
  T = floor((N - 5 * F - O)/2);

  cout<< "Count of 5 valueds coins: " << F << endl;
  cout<< "Count of 2 valueds coins: " << T<< endl;
  cout<< "Count of 1 valueds coins: " << O << endl;
}

// Driver Code
int main()
{
  int N = 8;
  find(N);
  return 0;
}

// This code is contributed by Jana_sayantan.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find minimum count of {1, 2, 5}
// valued coins required to make a change of
// all values in the range [1, N]
static void find(int N)
{
  int T, F, O;

  // Number of 5 valueds coins required
  F = (int)((N - 4) / 5);

  // Number of 1 valued coins required
  if (((N - 5 * F) % 2) == 0)
  {
    O = 2;
  }

  else
  {
    O = 1 ;
  }

  // Number of 2 valued coins required
  T = (int)Math.floor((N - 5 * F - O)/2);

   System.out.println("Count of 5 valueds coins: " + F);
   System.out.println("Count of 2 valueds coins: " + T);
   System.out.println("Count of 1 valueds coins: " + O);
}

// Driver Code
public static void main(String args[])
{
    int N = 8;
    find(N);
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to find minimum count of {1, 2, 5}
# valued coins required to make a change of
# all values in the range [1, N]
def find(N):

    # Number of 5 valueds coins required
    F = int((N - 4) / 5)

    # Number of 1 valued coins required
    if ((N - 5 * F) % 2) == 0:
        O = 2

    else:
        O = 1

    # Number of 2 valued coins required
    T = (N - 5 * F - O)//2

    print("Count of 5 valueds coins: ", F)
    print("Count of 2 valueds coins: ", T)
    print("Count of 1 valueds coins: ", O)

if __name__ == '__main__':

    N = 8
    find(N)
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

// Function to find minimum count of {1, 2, 5}
// valued coins required to make a change of
// all values in the range [1, N]
static void find(int N)
{
  int T, F, O;

  // Number of 5 valueds coins required
  F = (int)((N - 4) / 5);

  // Number of 1 valued coins required
  if (((N - 5 * F) % 2) == 0)
  {
    O = 2;
  }

  else
  {
    O = 1 ;
  }

  // Number of 2 valued coins required
  T = (int)Math.Floor((double)(N - 5 * F - O)/2);

   Console.WriteLine("Count of 5 valueds coins: " + F);
   Console.WriteLine("Count of 2 valueds coins: " + T);
   Console.WriteLine("Count of 1 valueds coins: " + O);
}

// Driver Code
public static void Main(String []args)
{
    int N = 8;
    find(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find minimum count of {1, 2, 5}
// valued coins required to make a change of
// all values in the range [1, N]
function find(N)
{
  var T, F, O;

  // Number of 5 valueds coins required
  F = parseInt((N - 4) / 5);

  // Number of 1 valued coins required
  if (((N - 5 * F) % 2) == 0)
  {
    O = 2;
  }

  else
  {
    O = 1 ;
  }

  // Number of 2 valued coins required
  T = Math.floor((N - 5 * F - O)/2);

  document.write( "Count of 5 valueds coins: " + F + "<br>");
  document.write( "Count of 2 valueds coins: " + T + "<br>");
  document.write( "Count of 1 valueds coins: " + O + "<br>");
}

var N = 8;
find(N);

// This code is contributed by SoumikMondal.
</script>
```

**Output:** 

```
Count of 5 valueds coins:  0
Count of 2 valueds coins:  3
Count of 1 valueds coins:  2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)