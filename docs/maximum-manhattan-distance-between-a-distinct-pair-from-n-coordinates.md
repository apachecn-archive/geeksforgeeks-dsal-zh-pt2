# N 坐标下不同对之间的最大曼哈顿距离

> 原文:[https://www . geeksforgeeks . org/max-Manhattan-distinct-pair-from-n-coordinates/](https://www.geeksforgeeks.org/maximum-manhattan-distance-between-a-distinct-pair-from-n-coordinates/)

给定一个由 **N** 整数坐标组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出任意两对不同坐标之间的最大[曼哈顿距离](https://en.wikipedia.org/wiki/Taxicab_geometry)。

> 两点 **(X1，Y1)** 和 **(X2，Y2)** 之间的**曼哈顿距离**由**| X1–X2 |+| Y1–Y2 |**给出。

**示例:**

> **输入:** arr[] = {(1，2)，(2，3)，(3，4)}
> **输出:** 4
> **解释:**
> 最大曼哈顿距离在(1，2)和(3，4)之间，即| 3–1 |+| 4-2 | = 4。
> 
> **输入:** arr[] = {(-1，2)、(-4，6)、(3，-4)、(-2，-4)}
> **输出:** 17
> **解释:**
> 最大曼哈顿距离在(-4，6)和(3，-4)之间，即|-4–3 |+| 6 –(-4)| = 17。

**天真方法:**最简单的方法是迭代数组，对于每个坐标，计算它与所有剩余点的曼哈顿距离。不断更新每次计算后获得的最大距离。最后，打印获得的最大距离。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the maximum
// Manhattan distance
void MaxDist(vector<pair<int, int> >& A, int N)
{
    // Stores the maximum distance
    int maximum = INT_MIN;

    for (int i = 0; i < N; i++) {

        int sum = 0;

        for (int j = i + 1; j < N; j++) {

            // Find Manhattan distance
            // using the formula
            // |x1 - x2| + |y1 - y2|
            sum = abs(A[i].first - A[j].first)
                  + abs(A[i].second - A[j].second);

            // Updating the maximum
            maximum = max(maximum, sum);
        }
    }

    cout << maximum;
}

// Driver Code
int main()
{
    int N = 3;

    // Given Co-ordinates
    vector<pair<int, int> > A
        = { { 1, 2 }, { 2, 3 }, { 3, 4 } };

    // Function Call
    MaxDist(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Pair class
    public static class Pair {
        int x;
        int y;

        Pair(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // Function to calculate the maximum
    // Manhattan distance
    static void MaxDist(ArrayList<Pair> A, int N)
    {

        // Stores the maximum distance
        int maximum = Integer.MIN_VALUE;

        for (int i = 0; i < N; i++) {
            int sum = 0;

            for (int j = i + 1; j < N; j++) {

                // Find Manhattan distance
                // using the formula
                // |x1 - x2| + |y1 - y2|
                sum = Math.abs(A.get(i).x - A.get(j).x)
                      + Math.abs(A.get(i).y - A.get(j).y);

                // Updating the maximum
                maximum = Math.max(maximum, sum);
            }
        }
        System.out.println(maximum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 3;

        ArrayList<Pair> al = new ArrayList<>();

        // Given Co-ordinates
        Pair p1 = new Pair(1, 2);
        al.add(p1);

        Pair p2 = new Pair(2, 3);
        al.add(p2);

        Pair p3 = new Pair(3, 4);
        al.add(p3);

        // Function call
        MaxDist(al, n);
    }
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to calculate the maximum
# Manhattan distance

def MaxDist(A, N):

    # Stores the maximum distance
    maximum = - sys.maxsize

    for i in range(N):
        sum = 0

        for j in range(i + 1, N):

            # Find Manhattan distance
            # using the formula
            # |x1 - x2| + |y1 - y2|
            Sum = (abs(A[i][0] - A[j][0]) +
                   abs(A[i][1] - A[j][1]))

            # Updating the maximum
            maximum = max(maximum, Sum)

    print(maximum)

# Driver code
N = 3

# Given co-ordinates
A = [[1, 2], [2, 3], [3, 4]]

# Function call
MaxDist(A, N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Pair class
    public class Pair {
        public int x;
        public int y;

        public Pair(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // Function to calculate the maximum
    // Manhattan distance
    static void MaxDist(List<Pair> A, int N)
    {

        // Stores the maximum distance
        int maximum = int.MinValue;

        for (int i = 0; i < N; i++) {
            int sum = 0;

            for (int j = i + 1; j < N; j++) {

                // Find Manhattan distance
                // using the formula
                // |x1 - x2| + |y1 - y2|
                sum = Math.Abs(A[i].x - A[j].x)
                      + Math.Abs(A[i].y - A[j].y);

                // Updating the maximum
                maximum = Math.Max(maximum, sum);
            }
        }
        Console.WriteLine(maximum);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 3;

        List<Pair> al = new List<Pair>();

        // Given Co-ordinates
        Pair p1 = new Pair(1, 2);
        al.Add(p1);

        Pair p2 = new Pair(2, 3);
        al.Add(p2);

        Pair p3 = new Pair(3, 4);
        al.Add(p3);

        // Function call
        MaxDist(al, n);
    }
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
4
```

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为给定数组的大小。*
***辅助空间:** O(N)*

**高效方法:**思路是利用存储 X 和 Y 坐标之间的和与差，通过对这些差进行排序来找到答案。以下是对上述问题陈述的观察:

*   任意两点之间的曼哈顿距离 **(X <sub>i</sub> 、Y <sub>i</sub> )** 和 **(X <sub>j</sub> 、Y <sub>j</sub> )** 可以写成:

> **| x<sub>【I】</sub>–x<sub>【j】</sub>|+| y<sub>【I】</sub>–y<sub>【j】</sub>**=<sub>最大值(X <sub>**—x<sub>【I】</sub>+x<sub>【j】</sub>–y<sub>【I】</sub>+y<sub>【j】</sub>，**</sub></sub>

*   上述表达式可以重新排列为:

> **| x<sub>【I】</sub>–x<sub>【j】</sub>|+| y<sub>【I】</sub>–y<sub>【j】</sub>| =最大值(【x<sub>【I】</sub>】y【t】**
> **(-x<sub>【I】</sub>–y<sub>【I】</sub>)--(-x<sub>【j】<sub>、</sub></sub>**)t

*   从上面的表达式可以看出，通过存储坐标的和与差可以找到答案。

按照以下步骤解决问题:

1.  初始化两个数组 **sum[]** 和 **diff[]** 。
2.  将 **X** 和 **Y** 坐标之和即**X<sub>I</sub>+Y<sub>I</sub>T9】存储在**sum【】**中，将它们的差即**X<sub>I</sub>–Y<sub>I</sub>T17】存储在**diff【】**中。****
3.  将**和[]** 和**差[]** 按升序排序。
4.  值的最大值(**sum[N-1]–sum[0])**和**(diff[N-1]–diff[0])**是要求的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the maximum
// Manhattan distance
void MaxDist(vector<pair<int, int> >& A, int N)
{
    // Vectors to store maximum and
    // minimum of all the four forms
    vector<int> V(N), V1(N);

    for (int i = 0; i < N; i++) {
        V[i] = A[i].first + A[i].second;
        V1[i] = A[i].first - A[i].second;
    }

    // Sorting both the vectors
    sort(V.begin(), V.end());
    sort(V1.begin(), V1.end());

    int maximum
        = max(V.back() - V.front(), V1.back() - V1.front());

    cout << maximum << endl;
}

// Driver Code
int main()
{
    int N = 3;

    // Given Co-ordinates
    vector<pair<int, int> > A
        = { { 1, 2 }, { 2, 3 }, { 3, 4 } };

    // Function Call
    MaxDist(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Pair class
    public static class Pair {
        int x;
        int y;

        Pair(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // Function to calculate the maximum
    // Manhattan distance
    static void MaxDist(ArrayList<Pair> A, int N)
    {

        // ArrayLists to store maximum and
        // minimum of all the four forms
        ArrayList<Integer> V = new ArrayList<>();
        ArrayList<Integer> V1 = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            V.add(A.get(i).x + A.get(i).y);
            V1.add(A.get(i).x - A.get(i).y);
        }

        // Sorting both the ArrayLists
        Collections.sort(V);
        Collections.sort(V1);

        int maximum
            = Math.max((V.get(V.size() - 1) - V.get(0)),
                       (V1.get(V1.size() - 1) - V1.get(0)));

        System.out.println(maximum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 3;

        ArrayList<Pair> al = new ArrayList<>();

        // Given Co-ordinates
        Pair p1 = new Pair(1, 2);
        al.add(p1);
        Pair p2 = new Pair(2, 3);
        al.add(p2);
        Pair p3 = new Pair(3, 4);
        al.add(p3);

        // Function call
        MaxDist(al, n);
    }
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the maximum
# Manhattan distance

def MaxDist(A, N):

    # List to store maximum and
    # minimum of all the four forms
    V = [0 for i in range(N)]
    V1 = [0 for i in range(N)]

    for i in range(N):
        V[i] = A[i][0] + A[i][1]
        V1[i] = A[i][0] - A[i][1]

    # Sorting both the vectors
    V.sort()
    V1.sort()

    maximum = max(V[-1] - V[0],
                  V1[-1] - V1[0])

    print(maximum)

# Driver code
if __name__ == "__main__":

    N = 3

    # Given Co-ordinates
    A = [[1, 2],
         [2, 3],
         [3, 4]]

    # Function call
    MaxDist(A, N)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Pair class
    class Pair {
        public int x;
        public int y;

        public Pair(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // Function to calculate the maximum
    // Manhattan distance
    static void MaxDist(List<Pair> A, int N)
    {

        // Lists to store maximum and
        // minimum of all the four forms
        List<int> V = new List<int>();
        List<int> V1 = new List<int>();

        for (int i = 0; i < N; i++) {
            V.Add(A[i].x + A[i].y);
            V1.Add(A[i].x - A[i].y);
        }

        // Sorting both the Lists
        V.Sort();
        V1.Sort();

        int maximum = Math.Max((V[V.Count - 1] - V[0]),
                               (V1[V1.Count - 1] - V1[0]));

        Console.WriteLine(maximum);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 3;

        List<Pair> al = new List<Pair>();

        // Given Co-ordinates
        Pair p1 = new Pair(1, 2);
        al.Add(p1);
        Pair p2 = new Pair(2, 3);
        al.Add(p2);
        Pair p3 = new Pair(3, 4);
        al.Add(p3);

        // Function call
        MaxDist(al, n);
    }
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*