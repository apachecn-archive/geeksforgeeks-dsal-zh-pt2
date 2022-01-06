# 用最少的步数找到一个数字

> 原文:[https://www . geesforgeks . org/find-a-number-in-mini-steps/](https://www.geeksforgeeks.org/find-a-number-in-minimum-steps/)

给定一条从-INFINITY 到+INFINITY 的无限数线，我们在零上。我们每次可以向两边移动 n 步。

**方法 1:使用树**

```
1st time; we can move only 1 step to both ways, means -1 1;

2nd time we can move 2 steps  from -1 and 1;
-1 :  -3 (-1-2)  1(-1+2)
 1 :  -1 ( 1-2)  3(1+2)

3rd time we can move 3 steps either way from -3, 1, -1, 3 
-3:  -6(-3-3) 0(-3+3)
1:   -2(1-3)   4(1+3)
-1:  -4(-1-3)  2(-1+3)
3:     0(0-3)   6(3+3) 

Find the minimum number of steps to reach a given number n.
```

示例:

```
Input : n = 10
Output : 4
We can reach 10 in 4 steps,  1, 3, 6, 10 

Input : n = 13
Output : 5
We can reach 10 in 4 steps,  -1, 2, 5, 9, 14
```

这个问题可以建模为树。我们把初始点 0 放在根，1 和-1 作为根的子。下一级包含距离 2 的值，依此类推。

```
              0
            /   \
         -1       1  
        /  \     /  \
       1   -3   -1   3
     /  \  / \  / \  / \
```

现在的问题是找到值为 n 的接近根的节点。想法是对树进行[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)来找到最近的节点。请注意，对最近的节点使用 DFS 从来都不是一个好主意(我们最终可能会降低许多不必要的级别)。

下面是 C++、Python 实现的上述思路。

## C++

```
// C++ program to find a number in minimum steps
#include <bits/stdc++.h>
using namespace std;
#define InF 99999

// To represent data of a node in tree
struct number {
    int no;
    int level;

public:
    number() {}
    number(int n, int l)
        : no(n), level(l)
    {
    }
};

// Prints level of node n
void findnthnumber(int n)
{
    // Create a queue and insert root
    queue<number> q;
    struct number r(0, 1);
    q.push(r);

    // Do level order traversal
    while (!q.empty()) {
        // Remove a node from queue
        struct number temp = q.front();
        q.pop();

        // To avoid infinite loop
        if (temp.no >= InF || temp.no <= -InF)
            break;

        // Check if dequeued number is same as n
        if (temp.no == n) {
            cout << "Found number n at level "
                 << temp.level - 1;
            break;
        }

        // Insert children of dequeued node to queue
        q.push(number(temp.no + temp.level, temp.level + 1));
        q.push(number(temp.no - temp.level, temp.level + 1));
    }
}

// Driver code
int main()
{
    findnthnumber(13);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a number in minimum steps
import java.util.*;
class GFG
{
  static final int InF = 99999;

  // To represent data of a node in tree
  static class number
  {
    int no;
    int level;
    number() {}
    number(int n, int l)
    {
      this.no = n;
      this.level = l;
    }
  };

  // Prints level of node n
  static void findnthnumber(int n)
  {

    // Create a queue and insert root
    Queue<number> q = new LinkedList<>();
    number r = new number(0, 1);
    q.add(r);

    // Do level order traversal
    while (!q.isEmpty())
    {

      // Remove a node from queue
      number temp = q.peek();
      q.remove();

      // To astatic void infinite loop
      if (temp.no >= InF || temp.no <= -InF)
        break;

      // Check if dequeued number is same as n
      if (temp.no == n)
      {
        System.out.print("Found number n at level "
                         + (temp.level - 1));
        break;
      }

      // Insert children of dequeued node to queue
      q.add(new number(temp.no + temp.level, temp.level + 1));
      q.add(new number(temp.no - temp.level, temp.level + 1));
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    findnthnumber(13);
  }
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
from collections import deque

# Python program to find a number in minimum steps
InF = 99999

# To represent data of a node in tree
class number:
    def __init__(self,n,l):
        self.no = n
        self.level = l

# Prints level of node n
def findnthnumber(n):
    # Create a queue and insert root
    q = deque()
    r = number(0, 1)
    q.append(r)

    # Do level order traversal
    while (len(q) > 0):
        # Remove a node from queue
        temp = q.popleft()
        # q.pop()

        # To avoid infinite loop
        if (temp.no >= InF or temp.no <= -InF):
            break

        # Check if dequeued number is same as n
        if (temp.no == n):
            print("Found number n at level", temp.level - 1)
            break

        # Insert children of dequeued node to queue
        q.append(number(temp.no + temp.level, temp.level + 1))
        q.append(number(temp.no - temp.level, temp.level + 1))

# Driver code
if __name__ == '__main__':
    findnthnumber(13)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find a number in minimum steps
using System;
using System.Collections.Generic;
public
class GFG
{
  static readonly int InF = 99999;

  // To represent data of a node in tree
  public
 class number
  {
    public
 int no;
    public
 int level;
    public
 number() {}
    public
 number(int n, int l)
    {
      this.no = n;
      this.level = l;
    }
  };

  // Prints level of node n
  static void findnthnumber(int n)
  {

    // Create a queue and insert root
    Queue<number> q = new Queue<number>();
    number r = new number(0, 1);
    q.Enqueue(r);

    // Do level order traversal
    while (q.Count != 0)
    {

      // Remove a node from queue
      number temp = q.Peek();
      q.Dequeue();

      // To astatic void infinite loop
      if (temp.no >= InF || temp.no <= -InF)
        break;

      // Check if dequeued number is same as n
      if (temp.no == n)
      {
        Console.Write("Found number n at level "
                         + (temp.level - 1));
        break;
      }

      // Insert children of dequeued node to queue
      q.Enqueue(new number(temp.no + temp.level, temp.level + 1));
      q.Enqueue(new number(temp.no - temp.level, temp.level + 1));
    }
  }

  // Driver code
  public static void Main(String[] args)
  {
    findnthnumber(13);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to find a number in minimum steps

  var InF = 99999;

  // To represent data of a node in tree
 class number
  {
    constructor(n, l)
  {
    this.no = n;
    this.level = l;
  }
  };

  // Prints level of node n
  function findnthnumber(n)
  {

    // Create a queue and insert root
    var q = [];
    var r = new number(0, 1);
    q.push(r);

    // Do level order traversal
    while (q.length != 0)
    {

      // Remove a node from queue
      var temp = q[0];
      q.shift();

      // To astatic void infinite loop
      if (temp.no >= InF || temp.no <= -InF)
        break;

      // Check if dequeued number is same as n
      if (temp.no == n)
      {
        document.write("Found number n at level "
                         + (temp.level - 1));
        break;
      }

      // Insert children of dequeued node to queue
      q.push(new number(temp.no + temp.level, temp.level + 1));
      q.push(new number(temp.no - temp.level, temp.level + 1));
    }
  }

  // Driver code

 findnthnumber(13);

</script>
```

**输出:**

```
Found number n at level 5
```

以上解决方案由**慕 Ven** 贡献。

**方法 2:使用** [**矢量**](https://www.geeksforgeeks.org/vector-in-cpp-stl/)

上面的解决方案对第 n 次实例使用二叉树，即-n 和 n。但是随着树的级别增加，这变得低效。对于像 abs(200)或更高的值，上述程序给出分段错误。
下面的解决方案并不构成一棵树，其复杂度等于所需的精确步骤数。此外，所需的步骤会打印在数组中，该数组等于所需的精确总和。

**主旨:**

*   +n 和-n 之间的距离是 2*n。所以如果你对一个从+ve 到-ve 的数求反，它将会和之前的和产生 2*n 的差。
*   如果对于任何 n，一个数位于 n(n+1)/2 和(n+1)(n+2)/2 之间，那么我们转到步骤(n+1)(n+2)/2，并尝试使用上面讨论的思想将和减少到差。
*   如果我们转到 n(n+1)/2，然后尝试增加，它最终会引导你达到相同的步数。
    由于你不能从 n(n+1)/2 中求任何数的反(因为和已经小于所需的和)，这证明了它需要的步数最少。

## C++

```
// C++ program to Find a
// number in minimum steps
#include <bits/stdc++.h>
using namespace std;

vector<int> find(int n)
{
    // Steps sequence
    vector<int> ans;

    // Current sum
    int sum = 0;
    int i;

    // Sign of the number
    int sign = (n >= 0 ? 1 : -1);
    n = abs(n);

    // Basic steps required to get
    // sum >= required value.
    for (i = 1; sum < n; i++) {
        ans.push_back(sign * i);
        sum += i;
    }

    // If we have reached ahead to destination.
    if (sum > sign * n) {
        /*If the last step was an odd number,
         then it has following mechanism for
         negating a particular number and
         decreasing the sum to required number
         Also note that it may require
         1 more step in order to reach the sum. */
        if (i % 2) {
            sum -= n;
            if (sum % 2) {
                ans.push_back(sign * i);
                sum += i++;
            }
            ans[(sum / 2) - 1] *= -1;
        }
        else {
            /* If the current time instance is even
            and sum is odd than it takes
            2 more steps and few
            negations in previous elements
            to reach there. */
            sum -= n;
            if (sum % 2) {
                sum--;
                ans.push_back(sign * i);
                ans.push_back(sign * -1 * (i + 1));
            }
            ans[(sum / 2) - 1] *= -1;
        }
    }
    return ans;
}

// Driver Program
int main()
{
    int n = 20;
    if (n == 0)
        cout << "Minimum number of Steps: 0\nStep sequence:\n0";
    else {
        vector<int> a = find(n);
        cout << "Minimum number of Steps: " << a.size() << "\nStep sequence:\n";
        for (int i : a)
            cout << i << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find a
// number in minimum steps
import java.util.*;
class GFG
{
  static Vector<Integer> find(int n)
  {

    // Steps sequence
    Vector<Integer> ans = new Vector<>();

    // Current sum
    int sum = 0;
    int i = 1;

    // Sign of the number
    int sign = (n >= 0 ? 1 : -1);
    n = Math.abs(n);

    // Basic steps required to get
    // sum >= required value.
    for (; sum < n;)
    {
      ans.add(sign * i);
      sum += i;
      i++;
    }

    // If we have reached ahead to destination.
    if (sum > sign * n)
    {

      /*If the last step was an odd number,
         then it has following mechanism for
         negating a particular number and
         decreasing the sum to required number
         Also note that it may require
         1 more step in order to reach the sum. */
      if (i % 2 != 0)
      {
        sum -= n;
        if (sum % 2 != 0)
        {
          ans.add(sign * i);
          sum += i;
          i++;
        }
        int a = ans.get((sum / 2) - 1);
        ans.remove((sum / 2) - 1);
        ans.add(((sum / 2) - 1), a*(-1));
      }
      else
      {

        /* If the current time instance is even
            and sum is odd than it takes
            2 more steps and few
            negations in previous elements
            to reach there. */
        sum -= n;
        if (sum % 2 != 0)
        {
          sum--;
          ans.add(sign * i);
          ans.add(sign * -1 * (i + 1));
        }
        ans.add((sum / 2) - 1, ans.get((sum / 2) - 1) * -1);
      }
    }
    return ans;
  }

  // Driver Program
  public static void main(String[] args)
  {
    int n = 20;
    if (n == 0)
      System.out.print("Minimum number of Steps: 0\nStep sequence:\n0");
    else
    {
      Vector<Integer> a = find(n);
      System.out.print("Minimum number of Steps: " + 
                       a.size()+ "\nStep sequence:\n");
      for (int i : a)
        System.out.print(i + " ");
    }
  }
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program to Find a
# number in minimum steps
def find(n):

    # Steps sequence
    ans = []

    # Current sum
    Sum = 0
    i = 0

    # Sign of the number
    sign = 0

    if (n >= 0):
        sign = 1
    else:
        sign = -1

    n = abs(n)
    i = 1

    # Basic steps required to get
    # sum >= required value.
    while (Sum < n):
        ans.append(sign * i)
        Sum += i
        i += 1

    # If we have reached ahead to destination.
    if (Sum > sign * n):

        # If the last step was an odd number,
        # then it has following mechanism for
        # negating a particular number and
        # decreasing the sum to required number
        # Also note that it may require
        # 1 more step in order to reach the sum.
        if (i % 2!=0):
            Sum -= n

            if (Sum % 2 != 0):
                ans.append(sign * i)
                Sum += i
                i += 1

            ans[int(Sum / 2) - 1] *= -1
        else:

            # If the current time instance is even
            # and sum is odd than it takes
            # 2 more steps and few
            # negations in previous elements
            # to reach there.
            Sum -= n

            if (Sum % 2 != 0):
                Sum -= 1
                ans.append(sign * i)
                ans.append(sign * -1 * (i + 1))

            ans[int((sum / 2)) - 1] *= -1

    return ans

# Driver code
n = 20

if (n == 0):
    print("Minimum number of Steps: 0\nStep sequence:\n0")
else:
    a = find(n)
    print("Minimum number of Steps:", len(a))
    print("Step sequence:")
    print(*a, sep = " ")

# This code is contributed by rag2127
```

## C#

```
// C# program to Find a
// number in minimum steps
using System;
using System.Collections.Generic;
public class GFG
{
  static List<int> find(int n)
  {

    // Steps sequence
    List<int> ans = new List<int>();

    // Current sum
    int sum = 0;
    int i = 1;

    // Sign of the number
    int sign = (n >= 0 ? 1 : -1);
    n = Math.Abs(n);

    // Basic steps required to get
    // sum >= required value.
    for (; sum < n;)
    {
      ans.Add(sign * i);
      sum += i;
      i++;
    }

    // If we have reached ahead to destination.
    if (sum > sign * n)
    {

      /*If the last step was an odd number,
         then it has following mechanism for
         negating a particular number and
         decreasing the sum to required number
         Also note that it may require
         1 more step in order to reach the sum. */
      if (i % 2 != 0)
      {
        sum -= n;
        if (sum % 2 != 0)
        {
          ans.Add(sign * i);
          sum += i;
          i++;
        }
        int a = ans[((sum / 2) - 1)];
        ans.RemoveAt((sum / 2) - 1);
        ans.Insert(((sum / 2) - 1), a*(-1));
      }
      else
      {

        /* If the current time instance is even
            and sum is odd than it takes
            2 more steps and few
            negations in previous elements
            to reach there. */
        sum -= n;
        if (sum % 2 != 0)
        {
          sum--;
          ans.Add(sign * i);
          ans.Add(sign * -1 * (i + 1));
        }
        ans.Insert((sum / 2) - 1, ans[(sum / 2) - 1] * -1);
      }
    }
    return ans;
  }

  // Driver Program
  public static void Main(String[] args)
  {
    int n = 20;
    if (n == 0)
      Console.Write("Minimum number of Steps: 0\nStep sequence:\n0");
    else
    {
      List<int> a = find(n);
      Console.Write("Minimum number of Steps: " + 
                    a.Count+ "\nStep sequence:\n");
      foreach (int i in a)
        Console.Write(i + " ");
    }
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to Find a
    // number in minimum steps

    function find(n)
    {

      // Steps sequence
      let ans = [];

      // Current sum
      let sum = 0;
      let i = 1;

      // Sign of the number
      let sign = (n >= 0 ? 1 : -1);
      n = Math.abs(n);

      // Basic steps required to get
      // sum >= required value.
      for (; sum < n;)
      {
        ans.push(sign * i);
        sum += i;
        i++;
      }

      // If we have reached ahead to destination.
      if (sum > sign * n)
      {

        /*If the last step was an odd number,
           then it has following mechanism for
           negating a particular number and
           decreasing the sum to required number
           Also note that it may require
           1 more step in order to reach the sum. */
        if (i % 2 != 0)
        {
          sum -= n;
          if (sum % 2 != 0)
          {
            ans.push(sign * i);
            sum += i;
            i++;
          }
          ans[parseInt(sum / 2, 10) - 1] =
          ans[parseInt(sum / 2, 10) - 1]*(-1);
        }
        else
        {

          /* If the current time instance is even
              and sum is odd than it takes
              2 more steps and few
              negations in previous elements
              to reach there. */
          sum -= n;
          if (sum % 2 != 0)
          {
            sum--;
            ans.push(sign * i);
            ans.push(sign * -1 * (i + 1));
          }
          ans[parseInt(sum / 2, 10) - 1] =
          ans[parseInt(sum / 2, 10) - 1] * -1;
        }
      }
      return ans;
    }

    let n = 20;
    if (n == 0)
      document.write("Minimum number of Steps: 0" +
      "</br>" + "Step sequence:" + "</br>" + "0");
    else
    {
      let a = find(n);
      document.write("Minimum number of Steps: " +
                       a.length + "</br>" + "Step sequence:" +
                       "</br>");
      for (let i = 0; i < a.length; i++)
        document.write(a[i] + " ");
    }

</script>
```

**输出:**

```

Minimum number of Steps: 7
Step sequence:
1 2 3 -4 5 6 7
```

如果 n 是所需步骤的总和，s 是最小步骤，那么:
n = (s+1)*(s+2)/2 + 1(或+2)
因此 n = O(s*s)
因此 s = O(sqrt(n))
空间复杂度:O(sqrt(n))
时间复杂度:O(sqrt(n))
https://youtu.be/GcrapHAFnLg
如果您发现任何不正确的地方，或者您想分享关于上述主题的更多信息，请写评论。